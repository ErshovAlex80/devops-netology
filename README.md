Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?


1 Гб ОЗУ
2 процессора
1,74 Гб жесткого диска (64 Гб  виртуального пространства)




Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: документация. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?


прописать в VagrantFile необходимые параметры для Виртуальной машины,  например:

Vagrant.configure("2") do |config|
 	config.vm.box = "bento/ubuntu-20.04"
        config.vm.box_check_update = false
        config.vm.memory = 2048
     # количество ядер процессора
        config.vm.cpus = 1
 end




Команда vagrant ssh из директории, в которой содержится Vagrantfile, позволит вам оказаться внутри виртуальной машины без каких-либо дополнительных настроек. Попрактикуйтесь в выполнении обсуждаемых команд в терминале Ubuntu.

Ознакомиться с разделами man bash, почитать о настройках самого bash:

какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?


  HISTSIZE shell variable.  If an attempt is made to set history-size to a non-numeric value, the maximum
       the  list  of commands previously typed.  The value of the HISTSIZE variable is used as the number of commands
       to save in a history list.  The text of the last HISTSIZE commands (default 500) is saved.  The  shell  stores
       FORMAT variable.  When a shell with history enabled exits, the last $HISTSIZE lines are copied from  the  his‐

export HISTSIZE=10000

export HISTFILESIZE=10000

HISTSIZE — количество команд, которые необходимо запоминать в списке истории (по умолчанию — 500)

HISTFILESIZE — максимальное количество строк, содержащееся в файле истории ~/.bash_history (по умолчанию — 500)




что делает директива ignoreboth в bash?


Существует два флага, ignoredups и ignorespace.

ignoredups-  отключить вывод одинковых команд.

ignorespace  указывает, что нужно игнорировать команды, начинающиеся с пробела. 

ignoreboth  - включить срахзу оба флага.  export HISTCONTROL=ignoreboth




В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?


применяются для обособления списка  команд, т.е.  получается вложенный блок, самостоятельная конструкция.
так же-  для перечисления символов, чисел, файлов,  разделенных запятой.


Brace Expansion
       Brace  expansion  is  a  mechanism  by which arbitrary strings may be generated.  This mechanism is similar to
       pathname expansion, but the filenames generated need not exist.  Patterns to be brace expanded take  the  form
       of  an  optional preamble, followed by either a series of comma-separated strings or a sequence expression be‐
       tween a pair of braces, followed by an optional postscript.  The preamble is prefixed to each string contained
       within the braces, and the postscript is then appended to each resulting string, expanding left to right.

       Brace  expansions  may  be nested.  The results of each expanded string are not sorted; left to right order is
       preserved.  For example, a{d,c,b}e expands into `ade ace abe'.

       A sequence expression takes the form {x..y[..incr]}, where x and y are either integers or  single  characters,
       and  incr,  an  optional increment, is an integer.  When integers are supplied, the expression expands to each
       number between x and y, inclusive.  Supplied integers may be prefixed with 0 to force each term  to  have  the
       same width.  When either x or y begins with a zero, the shell attempts to force all generated terms to contain
       the same number of digits, zero-padding where necessary.  When characters are supplied, the expression expands
       to  each character lexicographically between x and y, inclusive, using the default C locale.  Note that both x
       and y must be of the same type.  When the increment is supplied, it is used as  the  difference  between  each
       term.  The default increment is 1 or -1 as appropriate.

       Brace  expansion  is performed before any other expansions, and any characters special to other expansions are
       preserved in the result.  It is strictly textual.  Bash does not apply any  syntactic  interpretation  to  the
       context of the expansion or the text between the braces.

       A correctly-formed brace expansion must contain unquoted opening and closing braces, and at least one unquoted
       comma or a valid sequence expression.  Any incorrectly formed brace expansion is left unchanged.  A { or , may
       be  quoted  with  a  backslash to prevent its being considered part of a brace expression.  To avoid conflicts
       with parameter expansion, the string ${ is not considered eligible for brace expansion, and inhibits brace ex‐
       pansion until the closing }.

       This  construct is typically used as shorthand when the common prefix of the strings to be generated is longer
       than in the above example:

              mkdir /usr/local/src/bash/{old,new,dist,bugs}
       or
              chown root /usr/{ucb/{ex,edit},lib/{ex?.?*,how_ex}}

       Brace expansion introduces a slight incompatibility with historical versions of sh.  sh does not treat opening
       or  closing  braces  specially when they appear as part of a word, and preserves them in the output.  Bash re‐
       moves braces from words as a consequence of brace expansion.  For example, a word entered to sh  as  file{1,2}
       appears identically in the output.  The same word is output as file1 file2 after expansion by bash.  If strict
       compatibility with sh is desired, start bash with the +B option or disable brace expansion with the +B  option
       to the set command (see SHELL BUILTIN COMMANDS below).





Основываясь на предыдущем вопросе, как создать однократным вызовом touch 100000 файлов? А получилось ли создать 300000?


touch {1..100001}

при попытке создать 300000 (touch {1..300001})-  ошибка: -bash: /usr/bin/touch: Argument list too long
можно сделать, вручную изменив максимальный размер стека.




В man bash поищите по /\[\[. Что делает конструкция [[ -d /tmp ]]


проверяет- существует ли каталог с именем tmp.  если существует-  возвращает 1.




Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:


bash is /tmp/new_path_directory/bash
bash is /usr/local/bin/bash
bash is /bin/bash
(прочие строки могут отличаться содержимым и порядком)

mkdir /tmp/new_path_directory2/bash/

cp /bin/bash /tmp/new_path_directory2/bash/

PATH=$PATH:/tmp/new_path_directory2/bash/

echo $PATH

export PATH="/tmp/new_path_directory2/bash:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin"

 type -a bash





Чем отличается планирование команд с помощью batch и at?


at      executes commands at a specified time.

batch   executes commands when system load levels permit; in other words, when the load  average  drops  below
               1.5, or the value specified in the invocation of atd.
               
at  - выполняет команды в заданное время

batch -выполняет команды, когда позволяет уровень загрузки системы

