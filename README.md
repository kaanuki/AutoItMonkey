AutoIt Monkey
============

AutoIt Monkey provides an [AutoIt] interface for working with the Android [Monkey] tool.
This work is inspired by the [CyberAgent-adbkit-monkey] project a [Node.js] interface for working with the monkey tool.


## Monkey

The Monkey is a program that runs on your emulator or device and generates pseudo-random streams of user events such as clicks, touches, or gestures, as well as a number of system-level events but also Monkey program can be started in TCP mode with the --port argument. In this mode, it accepts a [range of commands] that can be used to interact with the UI in a non-random manner.

AutoItMonkey provides an interface for write an [AutoIt] script that control an Android device or emulator from outside of Android code. 


## Examples

The following examples assume that monkey is already running (via adb shell monkey --port 1088) and a port forwarding (adb forward tcp:1088 tcp:1088) has been set up.


#### Drag out the notification bar
```autoit
#include "monkey.au3"

Local $iMonkeyPort = 1088
Local $iSocket = _Monkey_Connect($iMonkeyPort)

;Drag out the notification bar
_Monkey_Touch_Down($iSocket,100, 0)
_Monkey_Sleep($iSocket,5)
_Monkey_Touch_Move($iSocket,100, 20)
_Monkey_Sleep($iSocket,5)
_Monkey_Touch_Move($iSocket,100, 40)
_Monkey_Sleep($iSocket,5)
_Monkey_Touch_Move($iSocket,100, 60)
_Monkey_Sleep($iSocket,5)
_Monkey_Touch_Move($iSocket,100, 80)
_Monkey_Sleep($iSocket,5)
_Monkey_Touch_Move($iSocket,100, 100)
_Monkey_Sleep($iSocket,5)
_Monkey_Touch_Up($iSocket,100, 100)
_Monkey_Sleep($iSocket,5)

_Monkey_Shutdown($iSocket)
```

#### Get display size, width and height
```autoit
#include "monkey.au3"

Local $iMonkeyPort = 1088
Local $iSocket = _Monkey_Connect($iMonkeyPort)

;Get display information
_ConsoleLog("Display density " & _Monkey_Get_DisplayDensity($iSocket))
_ConsoleLog("Display height " & _Monkey_Get_DisplayHeight($iSocket))
_ConsoleLog("Display width " & _Monkey_Get_DisplayWidth($iSocket))

_Monkey_Shutdown($iSocket)

Func _ConsoleLog($sText)
	ConsoleWrite($sText & @CRLF)
EndFunc
```


#### Type text
```autoit
#include "monkey.au3"

Local $iMonkeyPort = 1088
Local $iSocket = _Monkey_Connect($iMonkeyPort)

;Note that you should manually focus a text field first.
_Monkey_Type($iSocket,"Hello Monkey!!")

_Monkey_Shutdown($iSocket)
```

## Documentation

Check out the documentation: See [doc](https://github.com/ohtejera/AutoItMonkey/tree/master/doc)
generated by [Natural Docs](http://www.naturaldocs.org)


## Test 
See [Micro unit testing framework]

## Miscellaneous
This project use the excellent [ISN AutoIt Studio] IDE by Christian Faderl. 

## Contribution Guidelines

Please submit issues to *ohtejera/AutoItMonkey* and pull requests to *-dev branches.

![gauchoiwantyou2w](https://cloud.githubusercontent.com/assets/3797402/6205550/11ec108e-b559-11e4-8496-60e99d953dec.gif)

## License

Copyright © 2014 Henry Tejera <henrytejera@gmail.com>

This work is free. It comes without any warranty, to
the extent permitted by applicable law. You can redistribute it
and/or modify it under the terms of the Do What The Fuck You Want
To Public License, Version 2, as published by Sam Hocevar. See
[WTFPL] for more details

[AutoIt]: <www.autoitscript.com/site/autoit/>
[CyberAgent-adbkit-monkey]: <https://github.com/CyberAgent/adbkit-monkey>
[Node.js]: <http://nodejs.org/>
[Monkey]: <http://developer.android.com/tools/help/monkey.html>
[range of commands]: <https://github.com/android/platform_development/blob/master/cmds/monkey/README.NETWORK.txt>
[WTFPL]: <http://www.wtfpl.net/>
[Micro unit testing framework]: <http://htejera.users.sourceforge.net/micro/>
[ISN AutoIt Studio]:<http://www.isnetwork.at>

