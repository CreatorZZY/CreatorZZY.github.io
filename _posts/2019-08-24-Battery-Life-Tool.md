---
layout: post
title: Battery Life Tool.
subtitle: Story of the Application.
image: /img/2019-08-24-Battery-Life-Tool/BatteryIcon.png
tags: [Win10,C++]
bigimg: img/2019-08-24-Battery-Life-Tool/Big.jpg
gh-repo: CreatorZZY/BatteryLifeTool
gh-badge: [star,fork,follow]
comments: true
---

# BatteryLifeTool
*Time: 8-24-19 12:36:36*
## Download
[Battery Life Tool.msi(x86)](https://raw.githubusercontent.com/CreatorZZY/BatteryLifeTool/master/Battery%20Life%20Tool.msi)

[BatteryLifeTool.exe(x86)](https://raw.githubusercontent.com/CreatorZZY/BatteryLifeTool/master/BatteryLifeTool.exe)

## Configuration settings

```json
{
    "version": "1.0",
    // 90%
    "MaxBatteryLevelPercent": "90",
    // 15%
    "MinBatteryLevelPercent": "15",
    // Scan Interval. 1000 means 1 second.
    "ScanInterval": "30000"
}
```

## Background 

Lenovo computers have such a feature: Maintain the powerlevel at 55% to 60%, known as the `Power conservation mode`.
It is benefit to someone using the computer only at their office or home. But When you suddenly want to go out for business, 60% of the power is seen to be not enough.

If Charging threshold can set to 80% or above, it will be helpful. But I learn that only the Thinkpad laptops have this feature.

So I think if I can charge the scheduled power in the normal charging mode, then switch to the power conservation mode, then I can achieve what I want, maintain the high power conservation mode.

But I don’t know the API of the Lenovo Battery Driver. Maybe this program is not as good as I expected.

## Code Core

### Windows API

```c++
#include <windows.h>
//Freq : The voice Freq.
//Duration ： Duration of the voice.
Beep(Freq, Duration);

//MilliSecond : unsigned long
Sleep(MilliSecond);

// typedef struct _SYSTEM_POWER_STATUS {
//     BYTE ACLineStatus;
//     BYTE BatteryFlag;
//     BYTE BatteryLifePercent;
//     BYTE Reserved1;
//     DWORD BatteryLifeTime;
//     DWORD BatteryFullLifeTime;
// };
// BYTE : char / short.
typedef struct _SYSTEM_POWER_STATUS SYSTEM_POWER_STATUS, *LPSYSTEM_POWER_STATUS;
SYSTEM_POWER_STATUS sysPower = { 0 };
GetSystemPowerStatus(&sysPower);
```

### cJSON

cJSON [Click Here](https://github.com/DaveGamble/cJSON).
```c++
cjsondb = cJSON_Parse(jsondb.c_str());
cJSON_Print(cjsondb);
char* val = cJSON_GetObjectItem(cjsondb, "version");
```

## What I learn in this experience

### Add an icon to the program 

Create a New file and name it: *resource.rc*. Edit the file with a text editor. File content:
```
id ICON “/path to icon file (.ico)”
```

Open the Folder in the `powershell`.

Command:
```
windres resource.rc resource.o
```

And then link the resource.o to the executable output.

### Package installation package(.msi)
Download the application: `Advanced installer`.

### Git Problem
An error: `warning: LF will be replaced by CRLF` was raised when executing the command: `git add .`.
Command:
```
git config --global core.autocrlf true
```

### How to push the Project to Github?

Command:
```
git add .
git commit -m "Info"
git pull
git push
```

### Hide the console windows
```c++
HWND hwndDOS = GetForegroundWindow();
ShowWindow(hwndDOS, SW_HIDE);
// ShowWindow(hwndDOS, SW_SHOW);
```

## Full Code

[Click me](https://github.com/CreatorZZY/BatteryLifeTool).