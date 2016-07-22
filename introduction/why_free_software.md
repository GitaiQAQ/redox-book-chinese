为什么自由软件？
=======

Redox 操作系统将仅与兼容自由软件被包装，以确保整个缺省分布可以*检查*，*修改*和*再分发*。软件不允许这些功能，即专有软件，是违反安全和自由的目标，不会被 Redox 操作系统的认可。因此，我们遵守[GNU自由系统发行指南（http://www.gnu.org/distros/free-system-distribution-guidelines.html）。

要查看全部兼容的许可证列表，请参阅[许可证GNU列表]（http://www.gnu.org/licenses/license-list.html）。

有关自由软件的更多信息，[请浏览此页]（http://www.gnu.org/philosophy/free-sw.html）。

自由软件更安全
-------------------------------------
Redox 操作系统是MIT为主X11风格许可证在内的所有软件，文档和字体。目前只有少数例外情况：
- GNU UNIFONT，这是GPLv2许可
- Fira字体，这是SIL开放字体许可1.1
- 从OxygenKDE图标，这是LGPLv3
- Newlib C库，[这是一些免费的软件许可，大多是BSD]()https://github.com/bminor/newlib/blob/master/COPYING.NEWLIB)
- NASM，这是BSD2子句

MIT X11风格的许可证具有以下属性：
- 它给你的软件的用户，完整，无拘无束访问软件，这样你可以检查*修改*,*重新发布*和*更改*
   - *检查* 任何人都可以检查是否有安全漏洞的软件
   - *修改* 任何人都可以修改软件来修复安全漏洞
   - *再分布* 任何人都可以重新发布软件补丁的安全漏洞
- 这是与GPL兼容的许可 - 许可为GPL项目可以与 Redox OS分发
- 它允许GPL不兼容的自由软件的结合，如OpenZFS，这是CDDL行货
- 微内核架构意味着驱动程序可以维护者选择自己的自由软件许可证，以满足他们的需求

专有软件是不是安全
----------------------------------
考虑下面的条款，从 [Microsoft Windows 10's EULA](https://www.microsoft.com/en-us/Useterms/Retail/Windows/10/UseTerms_Retail_Windows_10_English.htm):
```
c.  Restrictions. The manufacturer or installer and Microsoft reserve all
    rights (such as rights under intellectual property laws) not expressly
    granted in this agreement. For example, this license does not give you
    any right to, and you may not:

(i)     use or virtualize features of the software separately;

(ii)    publish, copy (other than the permitted backup copy), rent, lease, or
        lend the software;

(iii)   transfer the software (except as permitted by this agreement);

(iv)    work around any technical restrictions or limitations in the software;

(v)     use the software as server software, for commercial hosting, make the
        software available for simultaneous use by multiple users over a
        network, install the software on a server and allow users to access it
        remotely, or install the software on a device for use only by remote
        users;

(vi)    reverse engineer, decompile, or disassemble the software, or attempt to
        do so, except and only to the extent that the foregoing restriction is
        permitted by applicable law or by licensing terms governing the use of
        open-source components that may be included with the software; and

(vii)   when using Internet-based features you may not use those features in any
        way that could interfere with anyone else’s use of them, or to try to
        gain access to or use any service, data, account, or network, in an
        unauthorized manner.
```

这些都是典型的条款私有软件许可证，但在自由软件许可证不允许的。这些子句它使微软起诉和谁试图*检查*，*修改*或*再分发*，他们已经安装了该软件的个人寻求损害赔偿。 Redox OS痛恨你的自由的限制。Redox OS专注于安全性，请记住以下几点：
- *检查*  软件是不合法，不能被社会所确定的安全漏洞。骇客将利用这一点，因为他们没有问题，违反了法律，并且将识别安全漏洞，并利用它们为自己的收益。
- *修改* 软件是不合法，不能有由社区修复的安全漏洞。同样，这将导致识别安全漏洞被留不固定的很长一段时间。
- *分发* 软件是不合法，不能由社区修补安全漏洞。这将导致一些弱势的安装，一个确定的安全漏洞已修复后还是一样。
