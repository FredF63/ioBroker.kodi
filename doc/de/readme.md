# Kodi's JSON-RPC-API für ioBroker
Die offizielle Kodi Dokumentation der JSON-RCP-API ist [hier](http://kodi.wiki/view/JSON-RPC_API) und die vollständige Liste der verfügbaren Befehle (für V6) ist [hier](http://kodi.wiki/view/JSON-RPC_API/v6) zu finden.

***Hinweis: Dieser Adapter benötigt Node 0.12+***

## Kodi Konfiguration
Im Hauptmenü von Kodi in der linken Menüspalte ganz oben über das Zahnradsymbol die Systemeinstellungen öffnen. Über Dienste dann Steuerung auswählen und `Steuerung über HTTP erlauben`, `Fernsteuerung durch Anwendungen dieses Rechners erlauben` und `Fernsteuerung durch Anwendungen anderer Rechners erlauben` auswählen.
![Fernsteuerung erlauben.](media/Fernsteuerung.jpg)

Die JSON-RPC-API verwendet den Port 9090. Um diesen Port zu ändern, muss eine Datei advancedsettings.xml erzeugt werden, die Standardmäßig nicht vorhanden ist und Änderungen vornehmen siehe [advancedsettings.xml](http://kodi.wiki/view/AdvancedSettings.xml)

```xml
<jsonrpc>
    <compactoutput>true</compactoutput>
    <tcpport>9999</tcpport>
</jsonrpc>
```
![http enable.](admin/web.jpg)

## Treiberkonfiguration
Die Treibereinstellungen geben die KODI-IP-Adresse und den Port für die JSON-RPC-API an (Standard ist 9090).

## Using
### ShowNotif:
Один важный момент, если используется заголовок сообщения, то он должен всегда находится перед самим текстом сообщения (Внимание;Протечка воды), расположение остальных параметров не критично.

**Image:**
Уровень сообщения
  * 'info' - 0 (default),
  * 'warning' - 1,
  * 'error' - 2.

**displaytime:**
Время отображения сообщения в милисекундах, минимум 1500 макс 30000 мс.

**Beispiel:**
 * 1;Внимание;Протечка воды;15000
 * Внимание;Протечка воды;2;10000
 * Внимание;Протечка воды
 * Протечка воды

Так же сообщения можно отправлять из драйвера javascript:
```js
sendTo("kodi.0", {
    message:  'Возможно протечка воды ', //Текст сообщения
    title:    'ВНИМАНИЕ!!!', //Заголовок сообщения
    image: 'https://raw.githubusercontent.com/instalator/ioBroker.kodi/master/admin/kodi.png', //Ссылка на иконку
    delay: 7000 //Время отображения сообщения милисекундах (минимум 1500 макс 30000 мс)
});
```
### SwitchPVR:
Переключение PVR IPTV каналов по названию канала в плейлисте.
**Пример:**
  ТВ канал - Discovery Science найдет как по полному наименованию так и по discover,

### Youtube:
Для открытия видео с сайта youtube достаточно записать код видео в данный статус. Начиная с версии 0.1.5 и выше можно вставлять прямую ссылку на видео, а также код или полную ссылку на плейлист.
Например: Для открытия этого [видео](https://www.youtube.com/watch?v=Bvmxr24D4TA), необходимо установить в статус - Bvmxr24D4TA

### Open:
Сюда записывается ссылка на медиконтент в сети интернет либо путь до локального медиа файла.
После записи значения начнется воспроизведение на проигрователе KODI.

### Position:
Текущая позиция в плейлисте, так же в этот статус можно записать необходимую позицую и KODI тут же перейдет к воспроизведению этой позиции.

### Seek:
Текущее значение позиции воспроизведения в процентах от 0 до 100.

### Repeat:
Повтор воспроизведения, принимает следующие значения:
* off - повтор воспроизведения отключен
* on - повтор воспроизведения текущего трека
* all - повтор всего плейлиста

### Shuffle:
Перемешивание списка треков в плейлисте для случайного воспроизведения.
Принимает значения true и false

### Play:
Старт воспроизведения (true, false)

### Speed:
Скорость воспроизведения. Фиксированные значения -32, -16, -8, -4, -2, -1, 0, 1, 2, 4, 8, 16, 32, а также increment и decrement

### Directory:
Сюда записывается путь до папки или диска, в ответ в этот статус записывается список каталогов указанной папки или диска.

### ActivateWindow:
Активизирует в проигрывателе окно. Поддерживает следующий список:
```
"home", "programs", "pictures", "filemanager", "files", "settings", "music", "video", "videos", "tv", "pvr", "pvrguideinfo", "pvrrecordinginfo", "pvrtimersetting", "pvrgroupmanager", "pvrchannelmanager", "pvrchannelmanager", "pvrguidesearch", "pvrchannelscan", "pvrupdateprogress", "pvrosdchannels", "pvrosdguide", "pvrosddirector", "pvrosdcutter", "pvrosdteletext", "systeminfo", "testpattern", "screencalibration", "guicalibration", "picturessettings", "programssettings", "weathersettings", "musicsettings", "systemsettings", "videossettings", "networksettings", "servicesettings", "appearancesettings", "pvrsettings", "tvsettings", "scripts", "videofiles", "videolibrary", "videoplaylist", "loginscreen", "profiles", "skinsettings", "addonbrowser", "yesnodialog", "progressdialog", "virtualkeyboard", "volumebar", "submenu", "favourites", "contextmenu", "infodialog", "numericinput", "gamepadinput", "shutdownmenu", "mutebug", "playercontrols", "seekbar", "musicosd", "addonsettings", "visualisationsettings", "visualisationpresetlist", "osdvideosettings", "osdaudiosettings", "videobookmarks", "filebrowser", "networksetup", "mediasource", "profilesettings", "locksettings", "contentsettings", "songinformation", "smartplaylisteditor", "smartplaylistrule", "busydialog", "pictureinfo", "accesspoints", "fullscreeninfo", "karaokeselector", "karaokelargeselector", "sliderdialog", "addoninformation", "musicplaylist", "musicfiles", "musiclibrary", "musicplaylisteditor", "teletext", "selectdialog", "musicinformation", "okdialog", "movieinformation", "textviewer", "fullscreenvideo", "fullscreenlivetv", "visualisation", "slideshow", "filestackingdialog", "karaoke", "weather", "screensaver", "videoosd", "videomenu", "videotimeseek", "musicoverlay", "videooverlay", "startwindow", "startup", "peripherals", "peripheralsettings", "extendedprogressdialog", "mediafilter".
```

### ExecuteAction:
Можно выполнить одно из следующих действий:
```
"left", "right", "up", "down", "pageup", "pagedown", "select", "highlight", "parentdir", "parentfolder", "back", "previousmenu", "info", "pause", "stop", "skipnext", "skipprevious", "fullscreen", "aspectratio", "stepforward", "stepback", "bigstepforward", "bigstepback", "osd", "showsubtitles", "nextsubtitle", "codecinfo", "nextpicture", "previouspicture", "zoomout", "zoomin", "playlist", "queue", "zoomnormal", "zoomlevel1", "zoomlevel2", "zoomlevel3", "zoomlevel4", "zoomlevel5", "zoomlevel6", "zoomlevel7", "zoomlevel8", "zoomlevel9", "nextcalibration", "resetcalibration", "analogmove", "rotate", "rotateccw", "close", "subtitledelayminus", "subtitledelay", "subtitledelayplus", "audiodelayminus", "audiodelay", "audiodelayplus", "subtitleshiftup", "subtitleshiftdown", "subtitlealign", "audionextlanguage", "verticalshiftup", "verticalshiftdown", "nextresolution", "audiotoggledigital", "number0", "number1", "number2", "number3", "number4", "number5", "number6", "number7", "number8", "number9", "osdleft", "osdright", "osdup", "osddown", "osdselect", "osdvalueplus", "osdvalueminus", "smallstepback", "fastforward", "rewind", "play", "playpause", "delete", "copy", "move", "mplayerosd", "hidesubmenu", "screenshot", "rename", "togglewatched", "scanitem", "reloadkeymaps", "volumeup", "volumedown", "mute", "backspace", "scrollup", "scrolldown", "analogfastforward", "analogrewind", "moveitemup", "moveitemdown", "contextmenu", "shift", "symbols", "cursorleft", "cursorright", "showtime", "analogseekforward", "analogseekback", "showpreset", "presetlist", "nextpreset", "previouspreset", "lockpreset", "randompreset", "increasevisrating", "decreasevisrating", "showvideomenu", "enter", "increaserating", "decreaserating", "togglefullscreen", "nextscene", "previousscene", "nextletter", "prevletter", "jumpsms2", "jumpsms3", "jumpsms4", "jumpsms5", "jumpsms6", "jumpsms7", "jumpsms8", "jumpsms9", "filter", "filterclear", "filtersms2", "filtersms3", "filtersms4", "filtersms5", "filtersms6", "filtersms7", "filtersms8", "filtersms9", "firstpage", "lastpage", "guiprofile", "red", "green", "yellow", "blue", "increasepar", "decreasepar", "volampup", "volampdown", "channelup", "channeldown", "previouschannelgroup", "nextchannelgroup", "leftclick", "rightclick", "middleclick", "doubleclick", "wheelup", "wheeldown", "mousedrag", "mousemove", "noop".

```
### System:
 - EjectOpticalDrive - Извлекает или закрывает дисковод оптических дисков (если имеется)
 - Hibernate - включение спящего режима
 - Reboot -  перезагрузка системы
 - Shutdown - выключает систему
 - Suspend - приостанавливает Kodi
