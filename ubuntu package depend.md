# Ubuntu Package depends and rdepends

* apt-cache

  - 查询依赖关系：

    `apt-cache depends packagename`

  - 查询反向依赖关系：

    `apt-cache rdepends packagename`

  - 正反向依赖同时查看

    `apt-cache showpkg packagename`

* aptitude

  * `aptitude why packagename`

    默认情况下，它只列出了"。最多安装，最强，最紧凑，最短"原因，但是可以使用 `aptitude -v why` 来输出它所发现的所有。

  * `aptitude install apt-rdepends`

    `apt-rdepends -r packagename`

* ``sudo apt -s remove packagename``

  ( `-s` 执行"模拟"删除操作。 )

  移除命令通常会列出任何受影响的dependencies/programs/libraries，或者可以将( 孤立的) 除以指定的fram。

* dpkg

  * `dpkg -I packagename`

     如果你从源列表之外的`.deb` 包中进行源代码，则 `apt-cache showpkg [Package-Name] && apt-cache depends [Package-Name]` 可能显示过时信息，或者与实际安装的软件包不同步，因此 `dpkg -I [Package-Name]` 在这种情况下最好。