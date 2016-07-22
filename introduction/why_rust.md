为什么 Rust ？
=========

为什么写在 Rust 的操作系统？为什么即使在 Rust 写？

Rust 具有巨大的优势，因为操作系统_safety matters_。很多，其实。

由于操作系统是计算机的这样的一个组成部分，他们是一个非常安全的重要组成部分。

已经有无数的bug和漏洞的Linux，BSD，Glibc，Bash，X等整个时间，只是由于缺乏记忆和类型安全。 Rust 由静态强制内存安全。

设计事做，但这样做的实现。 Rust 试图避免这些意外的内存不安全状况（这是安全的关键错误的主要来源）。设计是问题的非常透明的来源。你知道是怎么回事，你知道的意图是什么，什么不是。

内核/用户空间分离的基本设计是非常相似，真正的类Unix系统，在这一点上。这个想法是大致相同的：内核，管理内存和其他重要资源，你单独的内核和用户空间，通过严格的执法。

但是，我们有一个优势：强制记忆和类型安全。这是 Rust 的坚强的一面，大量的“意外的错误”（例如，不确定的行为）被淘汰。

Linux和BSD的设计是安全的。该

- [Linux kernel vulnerabilities]

- [Glibc vulnerabilities]

- [Bash vulnerabilities]

- [X vulnerabilities]

点击上面的链接。你可能会注意到，很多都来源于不安全的条件下（其中 Rust 有效地消除），如缓冲区溢出，没有整体设计错误。

我们希望用Rust，最终产生一个更安全的操作系统。

> TODO Rust 不会使你的代码设计的正确的; 这不可能。但是，它是可能的正式证明设计是合理的（如SEL4所做的那样），这是我们正在努力的东西。

[Linux kernel vulnerabilities]: https://www.cvedetails.com/vulnerability-list.php?vendor_id=33&product_id=47&version_id=&page=1&hasexp=0&opdos=0&opec=0&opov=0&opcsrf=0&opgpriv=0&opsqli=0&opxss=0&opdirt=0&opmemc=0&ophttprs=0&opbyp=0&opfileinc=0&opginf=0&cvssscoremin=7&cvssscoremax=7.99&year=0&month=0&cweid=0&order=3&trc=269&sha=27cc1be095dd1cc4189b3d337cc787289500c13e

[Glibc vulnerabilities]: https://www.cvedetails.com/vulnerability-list.php?vendor_id=72&product_id=767&version_id=&page=1&hasexp=0&opdos=0&opec=0&opov=0&opcsrf=0&opgpriv=0&opsqli=0&opxss=0&opdirt=0&opmemc=0&ophttprs=0&opbyp=0&opfileinc=0&opginf=0&cvssscoremin=0&cvssscoremax=0&year=0&month=0&cweid=0&order=3&trc=62&sha=5e0c40399ffafd65f77e6b537bcc0f50474eeed3

[Bash vulnerabilities]: http://www.cvedetails.com/vulnerability-list.php?vendor_id=72&product_id=21050&version_id=&page=1&hasexp=0&opdos=0&opec=0&opov=0&opcsrf=0&opgpriv=0&opsqli=0&opxss=0&opdirt=0&opmemc=0&ophttprs=0&opbyp=0&opfileinc=0&opginf=0&cvssscoremin=0&cvssscoremax=0&year=0&month=0&cweid=0&order=3&trc=10&sha=b7da5775428a703fdead6c27fbca76cd40b7c596

[X vulnerabilities]: https://www.cvedetails.com/vulnerability-list.php?vendor_id=8216&product_id=&version_id=&page=1&hasexp=0&opdos=0&opec=0&opov=0&opcsrf=0&opgpriv=0&opsqli=0&opxss=0&opdirt=0&opmemc=0&ophttprs=0&opbyp=0&opfileinc=0&opginf=0&cvssscoremin=0&cvssscoremax=0&year=0&month=0&cweid=0&order=3&trc=55&sha=a68a1ced1b67444749733b7fa9e1438ff0c42810

