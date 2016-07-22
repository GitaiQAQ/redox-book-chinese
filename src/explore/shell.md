# Shell
ion 是 Redox 的 [shell](http://linuxcommand.org/lts0010.php) 

当shell是呼叫无 "-c" 参数，它开始主循环可以在里面找到 `Shell.execute()`

```Rust
        self.print_prompt();
        while let Some(command) = readln() {
            let command = command.trim();
            if !command.is_empty() {
                self.on_command(command, &commands);
            }
            self.update_variables();
            self.print_prompt();
        }
```
`self.print_prompt();` 用来打印 shell 提示符。

在 `readln()` 是一个输入读者哪些代码可以在 `crates/ion/src/input_editor`

有关修剪文档都可以找到 [这里](https://doc.rust-lang.org/std/primitive.str.html#method.trim).
如果该命令不为空，则该方法 `on_command` 将被调用。此方法将在以后开发的。
那么shell将更新变量，然后重新打印提示。


```Rust
fn on_command(&mut self, command_string: &str, commands: &HashMap<&str, Command>) {
    self.history.add(command_string.to_string(), &self.variables);

    let mut pipelines = parse(command_string);

    // Execute commands
    for pipeline in pipelines.drain(..) {
        if self.flow_control.collecting_block {
            // TODO move this logic into "end" command
            if pipeline.jobs[0].command == "end" {
                self.flow_control.collecting_block = false;
                let block_jobs: Vec<Pipeline> = self.flow_control
                                               .current_block
                                               .pipelines
                                               .drain(..)
                                               .collect();
                match self.flow_control.current_statement.clone() {
                    Statement::For(ref var, ref vals) => {
                        let variable = var.clone();
                        let values = vals.clone();
                        for value in values {
                            self.variables.set_var(&variable, &value);
                            for pipeline in &block_jobs {
                                self.run_pipeline(&pipeline, commands);
                            }
                        }
                    },
                    Statement::Function(ref name, ref args) => {
                        self.functions.insert(name.clone(), Function { name: name.clone(), pipelines: block_jobs.clone(), args: args.clone() });
                    },
                    _ => {}
                }
                self.flow_control.current_statement = Statement::Default;
            } else {
                self.flow_control.current_block.pipelines.push(pipeline);
            }
        } else {
            if self.flow_control.skipping() && !is_flow_control_command(&pipeline.jobs[0].command) {
                continue;
            }
            self.run_pipeline(&pipeline, commands);
        }
    }
}
```
第一件事 `on_command` 做它的命令添加到用  `self.history.add(command_string.to_string(), &self.variables);`.

然后，该脚本就会被解析。解析器代码是在 `crates/ion/src/peg.rs`

解析将返回一组管线，每条管线包括一组作业。
每个作业代表了其参数的单个命令
你可以在看 `crates/ion/src/peg.rs`
```Rust
pub struct Pipeline {
    pub jobs: Vec<Job>,
    pub stdout: Option<Redirection>,
    pub stdin: Option<Redirection>,
}
pub struct Job {
    pub command: String,
    pub args: Vec<String>,
    pub background: bool,
}
```
什么后会发生在简要介绍：
*如果当前块是一个收集块（一个for循环或函数声明）和当前命令结束时，我们关闭块：
   *如果块是一个循环，我们跑环
   *如果块是一个函数声明，我们推的功能函数列表
*如果当前块是一个收集块，但电流指令没有结束，我们添加当前命令块。
*如果当前块不是收集块，我们只是执行当前命令。

代码块在 `crates/ion/src/flow_control.rs`
```Rust
pub struct CodeBlock {
    pub pipelines: Vec<Pipeline>,
}
```
功能代码在' `crates/ion/src/functions.rs` 定义

管道内容的执行将在 `run_pipeline()`

Command类里面 `crates/ion/src/main.rs` 每个命令映射与描述和方法
被执行。 例如 ：
```Rust
commands.insert("cd",
                Command {
                    name: "cd",
                    help: "Change the current directory\n    cd <path>",
                    main: box |args: &[String], shell: &mut Shell| -> i32 {
                        shell.directory_stack.cd(args, &shell.variables)
                    },
                });
```
`cd` is described by  `"Change the current directory\n    cd <path>"`, and when called the method
`shell.directory_stack.cd(args, &shell.variables)` will be used. you can see its code in `crates/ion/src/directory_stack.rs`
