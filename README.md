<h1 align="center">FixVim</h1>

FixVim — это конфигурация NeoVim для Linux, написанная на Lua, цель которой — предоставить разумную конфигурацию по умолчанию с  невероятно быстрым временем запуска. Если вам понравится данная сборка, то поставьте :star2: этому репозиторию!

## Особенности FixVim
 1. Используется удобная модульная структура, благодаря которой очень легко поддерживать работоспособность сборки.
 2. Ориентированность на русскоговорящих пользователей.
 3. Имеет разумный набор расширений и параметров, которые можно легко настроить под себя.
 4. Огромное количество поясняющих комментариев, благодаря которым очень легко разобраться в функционале.
 5. FixVim по умолчанию полностью настроен для работы с Python и Lua, включая удобную работу с NeoVim API, благодаря чему очень удобно улучшать FixVim под свои нужды. Также имеются расширения для лучшего опыта работы с CSS (различные взаимодействия с цветовыми кодами и их отображение). Со временем будет добавляться поддержка других инструментов для программирования по умолчанию, но вы можете не дожидаться этого момента, а добавить нужное самостоятельно.

## Установка

### Предварительные условия
Для того чтобы FixVim работал корректно, требуется удовлетворить его зависимости. (Учтите что одним из требований является использование последней стабильной версии NeoVim!) В данном примере используется команда для Arch Linux, поэтому вам придется заменить ее на аналогичную для вашего дистрибутива! Чтобы установить необходимые пакеты, выполните следующую команду:
```bash
sudo pacman -Syu --needed git neovim xclip wl-clipboard nodejs npm
```
Данная команда выполнит полное обновление системы, после чего установит недостающие пакеты. Все пакеты, указанные выше, рекомендуются к установке по умолчанию для лучшей совместимости и избежания потенциальных проблем. Однако вы можете пренебречь некоторыми пакетами. Например если вы не используете Wayland, то нет необходимости в установке пакета `wl-clipboard`. Но все же стоит отметить, что если вы соберетесь его использовать, то без указанного пакета вы не сможете использовать глобальный буфер обмена системы, поэтому вы будете ограничены функциями копировать/вставить только внутри FixVim.

Краткое объяснение назначения пакетов:
 - `neovim` - программа, к которой будет применена конфигурация
 - `git` - необходим для установки FixVim
 - `xclip` - поддержка буфера обмена на X11
 - `wl-clipboard` - поддержка буфера обмена на Wayland
 - `nodejs` и `npm` - зависимости для Mason (менеджер пакетов для NeoVim)

Помимо этого, требуется наличие терминала с поддержкой True Color, а также в нем должен использоваться один из шрифтов коллекции [Nerd Fonts](https://www.nerdfonts.com/). Также необходимо удовлетворить зависимости актуальной версии NeoVim и используемых в FixVim расширений. (Например для nvim-treesitter необходимо наличие gcc в системе.)

**P.S:** Если вы до этого не настраивали NeoVim, то можете смело приступать к установке FixVim. Если же вы использовали собственные настройки или любой другой дистрибутив, то выполните действия, указанные ниже:

 1. Сохраните копию своей конфигурации, если вам это нужно. Данную процедуру можно выполнить следующей командой:
	 ```bash
	 mv ~/.config/nvim ~/.config/oldnvim
	 ```
 2. После выполнения первого пункта следуйте действиям, описанным в разделе `"Удаление FixVim"`. (Несмотря на название раздела, указанные в нем инструкции подходят как для стандартного NeoVim, так и для его дистрибутивов.) Если вы все же решили сохранить свою конфигурацию, то перед выполнением команды из указанного выше раздела удалите в ней часть `~/.config/nvim` в конце во избежания ошибки, связанной с отсутствием данного каталога по причине того, что он был переименован, поэтому его попросту не существует.

*Теперь вы готовы к следующему этапу!*

###  Установка FixVim
Есть несколько способов установки FixVim на ваш ПК. Выбирайте тот, который лучше покроет ваши потребности!

Для установки последней версии данной сборки выполните команду ниже:
```bash
git clone --depth 1 https://github.com/krator3/fixvim ~/.config/nvim && rm -rf ~/.config/nvim/lazy-lock.json ~/.config/nvim/.git
```
Также для корректной работы FixVim не требуются файлы LICENSE и README.md, поэтому можете удалить их, если они вам не нужны.

Если же вы желаете установить какую-то конкретную версию FixVim, то перейдите в раздел "Releases", выберите нужную вам версию и найдите в ее описании команду для установки, которая будет располагаться в конце. **Учтите, что не рекомендуется устанавливать слишком старые версии, так как они могут быть несовместимы с новыми выпусками NeoVim!**

**P.S:** Команда клонирует FixVim на ваш ПК по пути `~/.config/nvim/` и удаляет лишние файлы, не требующиеся для его работы.

### Действия после установки
После выполнения предыдущих шагов остается последний штрих. Запустите следующую команду в своем терминале:
```bash
nvim
```
Благодаря этой команде запустится NeoVim с конфигурацией FixVim, далее автоматически активируется `Lazy`(менеджер плагинов), который установит все расширения, предложенные данной сборкой, а также подключит их файлы конфигурации. После завершения установки нажмите клавишу `q`, которая закроет окно `Lazy`. При следующих запусках  `NeoVim` окно `Lazy` больше не будет запускаться автоматически! Далее, убедитесь, что все предусмотренные treesitter были установлены(прогресс отображается внизу программы), а также проконтролируйте установку LSP и других инструментов через команду `:Mason`. Данное окно также закрывается при помощи клавиши `q` и оно тоже не будет автоматически отображаться при следующих запусках программы. (Указанный процесс может занять немного больше времени, чем остальные процессы!) По окончанию финальной настройки FixVim перезапустите программу и начинайте получать удовольствие от ее использования!

P.S: Дополнительно рекомендуется запустить команду `:checkhealth` после запуска NeoVim для проверки корректности установки FixVim.

Для установки дополнительных LSP используйте одну из предложенных команд:
 1. `:LspInstall <language>`
 2. `:MasonInstall <language>`. (Данная команда позволяет устанавливать не только LSP, но и другие полезные инструменты для программирования.)

Для установки дополнительных TreeSitter используется команда `:TSInstall <language>`. Обычно недостающие TreeSitter устанавливаются автоматически, но вы можете изменить данное поведение в настройках сборки.

P.S: Обратите внимание, что комбинации клавиш FixVim могут конфликтовать с системными сочетаниями клавиш. В таком случае вам придется вручную изменить их либо в настройках FixVim, либо в системе. Помните, что системные сочетания обладают более высоким приоритетом, поэтому в сложившейся ситуации вместо сочетаний FixVim будут выполнены системные.

## Удаление FixVim
Для того чтобы полностью удалить FixVim из вашей системы и вернуть стандартный NeoVim необходимо выполнить следующую команду:
```
rm -rf ~/.cache/nvim ~/.local/share/nvim ~/.local/state/nvim ~/.config/nvim
```
После этого переустановите пакет `neovim`.

## Дорожная карта
Здесь вы можете узнать ближайшие планы по разработке FixVim. Учтите, что планы могут меняться, поэтому нет никаких гарантий, что все из этого списка будет добавлено!

 - [ ] Улучшить производительность FixVim
	 - [ ] Заменить vim-vsnip на LuaSnip в расширении nvim-cmp
	 - [ ] Добавить активацию раширений по событиям
 - [ ] Добавить новые полезные плагины
 - [ ] Улучшисть файловую структуру FixVim
 - [x] Усовершенствовать документацию FixVim

Предлагаемые функции и известные проблемы, найденные сообществом, можно посмотреть в разделе [открытых проблем](https://github.com/krator3/fixvim/issues).

## Содействие
Любая помощь со стороны сообщества категорически приветствуется! Если вы хотите сообщить о найденных ошибках или предложить нововведение без готового решения, то просто откройте новую проблему с соответствующей темой. Если же вы хотите внести изменения в сборку, например, исправить найденную ошибку, улучшить документацию или сделать что-то другое, то не стесняйтесь и смело предлагайте свои изменения! Если ваш вклад будет достаточно качественным и востребованным, то он будет объединен с проектом FixVim, а вы станете одним из немногих соавторов, на чьем труде основывается успех проекта. В независимости от того, какую помощь вы решили оказать, важно подробно описать аспекты того, о чем вы решили сообщить, или о том, что вы решили улучшить. Чем детальнее и понятнее вы сможете выразить свои мысли, тем больше шансов, что вам смогут помочь.

**P.S:** Учтите, что изменения не должны быть основаны на том, что находится во вкладке `"Releases"` так как есть вероятность того, что ваши предложения или замечания уже были учтены в последнем изменении FixVim, которое еще не успело попасть в новый выпуск!

## Авторы
<u>Разработчики:</u>
* **Остапенко Максим** - [Krator3](https://github.com/krator3)
* **Новгородцев Кирилл** - [Dev-cmyser](https://github.com/Dev-cmyser)
* **Алексеев Бронислав** - [Alexeev-engineer](https://github.com/alexeev-engineer)

<u>Тестировщики</u>:
*  **Поворознюк Михаил** - [archer7717](https://github.com/archer7717)

См. также список [соавторов](https://github.com/krator3/fixvim/contributors), принявших участие в этом проекте.

## Лицензия
Этот проект лицензируется по лицензии GNU GPL — подробности см. в файле [LICENSE](LICENSE)

## ЧаВо (FAQ)
- Что делать, если Python не видит сторонние файлы и библиотеки?

  По умолчанию Pyright (LSP для Python) запускается в однофайловом режиме работы. Чтобы переключить режим работы на многофайловый следует ознакомиться со следующей настройкой:
  ```lua
  root_dir = lsputil.root_pattern('.git', 'pyrightconfig.json', 'setup.py', 'setup.cfg', 'requirements.txt', 'Pipfile', 'pyproject.toml'),
  ```
  Данный параметр определяет файлы и директории, которые переводят Pyright в многофайловый режим работы. При обнаружении чего-либо указанного в параметре Pyright будет видеть все содержимое данного каталога, поэтому вам требуется создать что-либо из представленных вариантов в директории вашего проекта. Чтобы Pyright смог обнаружить сторонние библиотеки нужно использовать виртуальное окружение. Для того чтобы его создать выполните следующую команду в терминале в нужной вам директории **до запуска** NeoVim!
  ```bash
  python3 -m venv venv
  ```
  После активируйте его командой ниже:
  ```bash
  source venv/bin/activate
  ```
  Теперь запустите Neovim командой `nvim` в этом же каталоге. После всех проведенных манипуляций FixVim будет видеть как сторонние файлы, так и сторонние библиотеки.

  P.S: Если вы собираетесь устанавливать расширения для Python через встроенный терминал NeoVim или через терминал-расширение (рекомендуемый способ), не забудьте вновь активировать виртуальную среду в данном терминале! Также после установки новых библиотек выполняйте команду  `:LspRestart` в NeoVim для того, чтобы Pyright принял все внесенные изменения! (Естественно, вам никто не запрещает сначала установить нужные библиотеки и только после этого зайти в NeoVim. Если вы уверены, что вам больше ничего не придется доустановить, то нет необходимости проделывать действия из этого блока.)

- Как сохранить существующую конфигурацию параллельно с FixVim?
  Для этого вы можете использовать функцию псевдонимов от вашей командной оболочки + встроенную возможность Nvim. Например, вы можете установить FixVim в `~/.config/fixvim`и создать псевдоним:
  ```bash
  alias fixvim='NVIM_APPNAME="fixvim" nvim'
  ```

   Благодаря этому вы сможете запускать собственную конфигурацию при помощи команды `nvim`, а сборку FixVim при помощи команды `fixvim`. Также вы можете изменить псевдоним на любой другой. Дополнительно стоит отметить, что данный способ должен быть совместим с любой другой конфигурацией NeoVim.

  P.S: Учтите, что данная инструкция не была проверена мной лично! Данная информация была взята из документации к kickstart.nvim и адаптирована под данный проект!
