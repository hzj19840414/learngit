# DOS Command :  forfiles

- 在win7系统中自带forfiles命令
- 支持以时间的方式遍历文件夹，比如说从7天前修改的文件
- 命令帮助文档如下

FORFILES [/P pathname] [/M searchmask] [/S]
         [/C command] [/D [+ | -] {yyyy/MM/dd | dd}]

描述:
    选择一个文件(或一组文件)并在那个文件上
    执行一个命令。这有助于批处理作业。

参数列表:
    /P    pathname      表示开始搜索的路径。默认文件夹是当前工作的
                        目录 (.)。


    /M    searchmask    根据搜索掩码搜索文件。默认搜索掩码是 '*'。
    
    /S                  指导 forfiles 递归到子目录。像 "DIR /S"。


    /C    command       表示为每个文件执行的命令。命令字符串应该
                        用双引号括起来。


                        默认命令是 "cmd /c echo @file"。下列变量
                        可以用在命令字符串中:
    
                        @file    - 返回文件名。
                        @fname   - 返回不带扩展名的文件名。
    
                        @ext     - 只返回文件的扩展名。
    
                        @path    - 返回文件的完整路径。
                        @relpath - 返回文件的相对路径。
    
                        @isdir   - 如果文件类型是目录，返回 "TRUE"；
                                   如果是文件，返回 "FALSE"。
                        @fsize   - 以字节为单位返回文件大小。
    
                        @fdate   - 返回文件上一次修改的日期。
    
                        @ftime   - 返回文件上一次修改的时间。


                        要在命令行包括特殊字符，字符请以 0xHH
                        形式使用十六进制代码(例如，0x09 为 tab)。
    
                        内部 CMD.exe 命令前面应以 "cmd /c" 开始。


    /D    date          选择文件，其上一次修改日期大于或等于 (+)，
                        或者小于或等于 (-) 用 "yyyy/MM/dd" 格式指定的日
    
                        或选择文件，其上一次修改日期大于或等于 (+)
                        当前日期加 "dd" 天，或者小于或等于 (-) 当前
    
                        日期减 "dd" 天。有效的 "dd" 天数可以是
                        0 - 32768 范围内的任何数字。如果没有指定，
    
                        "+" 被当作默认符号。
    
    /?                  显示此帮助消息。

示例:
    FORFILES /?
    FORFILES
    FORFILES /P C:\WINDOWS /S /M DNS*.*
    FORFILES /S /M *.txt /C "cmd /c type @file | more"
    FORFILES /P C:\ /S /M *.bat
    FORFILES /D -30 /M *.exe
             /C "cmd /c echo @path 0x09 在 30 前就被更改。"
    FORFILES /D 2001/01/01
             /C "cmd /c echo @fname 在 2001年1月1日就是新的。"
    FORFILES /D +2019/8/17 /C "cmd /c echo @fname 今天是新的。"
    FORFILES /M *.exe /D +1
    FORFILES /S /M *.doc /C "cmd /c echo @fsize"
    FORFILES /M *.txt /C "cmd /c if @isdir==FALSE notepad.exe @file"



- 使用示例

  查询C盘（/p c:\）及其子目录（/s ）下的后缀名为xls( /m *.xls) 七天前的修改文件

  `forfiles /p c:\ /s /m *.xls /d -7`

  结果是：

  "加油.xls"
  "c:朋友list.xls"

  只有文件名

  如果现有得到完整的路径包括文件名

  `forfiles /p c:\ /s /m *.xls /d -7 /c "cmd /c ehco &path"`

  结果如下：

  `"c:\Users\hzj\AppData\Local\Kingsoft\WPS Office\11.1.0.8214\office6\mui\zh_CN\templates\newfile.xls"
  "c:\Users\hzj\AppData\Local\Kingsoft\WPS Office\11.1.0.8214\office6\mui\zh_CN\templates\secdoctemplate.xls"
  "c:\Users\hzj\AppData\Local\Kingsoft\WPS Office\11.1.0.8612\office6\mui\zh_CN\templates\newfile.xls"
  "c:\Users\hzj\AppData\Local\Kingsoft\WPS Office\11.1.0.8612\office6\mui\zh_CN\templates\secdoctemplate.xls"
  "c:\Users\hzj\AppData\Local\Kingsoft\WPS Office\11.1.0.8812\office6\mui\zh_CN\templates\newfile.xls"
  "c:\Users\hzj\AppData\Local\Kingsoft\WPS Office\11.1.0.8812\office6\mui\zh_CN\templates\secdoctemplate.xls"
  "c:\Users\hzj\Desktop\加油.xls"
  "c:\朋友list.xls"`

- 时间需求有可能是需要遍历所有盘（C D E F）下面的文件，不限定类型(参数`/m *.*`，或者不写这个参数)，最近8（今天2019/8/16）天中有修改的，导入一个文档check.log,这个时候就需要嵌套一个for循环

  `for %a in (C D E F) do forfiles /p %a:\ /s /m *.* /d +2018/8/8 /c "cmd /c echo @path" >>check.log`

- 如果是需要对筛选出来的文件做其他出来 ，例如是删除  修改 /c后的命令参数 /c "cmd /c del /q @path"

