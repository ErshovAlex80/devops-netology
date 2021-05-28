-Найдите полный хеш и комментарий коммита, хеш которого начинается на aefea.

    git show aefea
   aefead2207ef7e2aa5dc81a34aedf0cad4c32545 
    Update CHANGELOG.md

-Какому тегу соответствует коммит 85024d3?

    git show 85024d3
    tag: v0.12.23


-Сколько родителей у коммита b8d720? Напишите их хеши.
   git log -1 b8d720
   commit b8d720f8340221f2146e4e4870bf2ee0bc48f2d5
   Merge: 56cd7859e   9ea88f22f


-Перечислите хеши и комментарии всех коммитов которые были сделаны между тегами v0.12.23 и v0.12.24.

  git log --pretty=format:"%H %s" v0.12.23..v0.12.24
33ff1c03bb960b332be3af2e333462dde88b279e v0.12.24
b14b74c4939dcab573326f4e3ee2a62e23e12f89 [Website] vmc provider links
3f235065b9347a758efadc92295b540ee0a5e26e Update CHANGELOG.md
6ae64e247b332925b872447e9ce869657281c2bf registry: Fix panic when server is unreachable
5c619ca1baf2e21a155fcdb4c264cc9e24a2a353 website: Remove links to the getting started guide's old location
06275647e2b53d97d4f0a19a0fec11f6d69820b5 Update CHANGELOG.md
d5f9411f5108260320064349b757f55c09bc4b80 command: Fix bug when using terraform login on Windows
4b6d06cc5dcb78af637bbb19c198faff37a066ed Update CHANGELOG.md
dd01a35078f040ca984cdd349f18d0b67e486c35 Update CHANGELOG.md
225466bc3e5f35baa5d07197bbc079345b77525e Cleanup after v0.12.23 release


-Найдите коммит в котором была создана функция func providerSource, ее определение в коде выглядит так func providerSource(...) (вместо троеточего перечислены аргументы).
git log -S "func providerSource"
git show 8c928e83589d90a031f811fae52a81be7153e82f
git show 5af1e6234ab6da412fb8637393c5a17a1b293663
   создана в 8c928e83589d90a031f811fae52a81be7153e82f
   изменена в 5af1e6234ab6da412fb8637393c5a17a1b293663 


-Найдите все коммиты в которых была изменена функция globalPluginDirs.
    git log -S globalPluginDirs --oneline
 выдает 3 записи:
  35a058fb3 main: configure credentials from the CLI config file
  c0b176109 prevent log output during init
  8364383c3 Push plugin discovery down into command package

однако анализ файла, в котором производились изменения:
git log -L :globalPluginDirs:plugins.go
говорит нам, что в действительности ф-я изменялась только в одном коммите:
8364383c3
8364383c359a6b738a436d1b7745ccdce178df47
в остальных случаях она либо упоминается в комменарии, либо используется как аргумент.


-Кто автор функции synchronizedWriters?
  git log -S"synchronizedWriters"
  Author: Martin Atkins <mart@degeneration.co.uk>



