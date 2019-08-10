---
layout: post
title: Right Click and Open The Folder With VSCODE.
subtitle: How to Create Your Right Click Menu in Windows10？
image: /img/2019-08-04_23.18.15.jpg
tags: [Win10]
bigimg: /img/2019-08-04_23.18.15.jpg
gh-repo: CreatorZZY
gh-badge: [follow]
comments: true
---

# I heared that you hate the Mess menu.
## Would you like to deal with it?

### BackGround

May be your menu have something usually not used.
just like this:

![IMG](/img/2019-08-10-Right-Click-and-Open-The-Folder-With-VSCODE/IMG.png){: .center-block :}

How to Hide something usually not used but actually useful?

Actually i find Something Interesting when i search how i can open the folder in cmd as soon as i right click the free space in the explorer. I find that pass press the left shift and right click and there will be an interesting option: Open PowerShell windows here.

If the option Open Here in VS Code hide in the left shift, **will it be better**?

### How to Achieve it?

{: .box-note}
**Code Here:**
{: .box-note}
**Save as the .reg file. And `Run as Admin account`**
~~~
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shell\Open Here In VS Code]
@="Open Here In VS Code"
"HasLUAShield-"=""
"Extended"=""
"Icon"="ICON File Path\\ico.ico"

[HKEY_CLASSES_ROOT\Directory\Background\shell\Open Here In VS Code\command]
@="Program File Path\\Code.exe %V"
~~~

#### First Step

Open the `regedit` and locate the postion `HKEY_CLASSES_ROOT\Directory\Background\shell\`.
Create a new Key under the `shell`. The name of the Key is random if you like. As the example, I named it `Open Here In VS Code`
Create a new Key under the `Open Here In VS Code` with the name `command`.

![IMG](/img/2019-08-10-Right-Click-and-Open-The-Folder-With-VSCODE/IMG2.png){: .center-block :}

#### Second Step

Go into the Key: `Open Here In VS Code` and **Modify** the Default Data: `Open Here In VS Code`.
![IMG](/img/2019-08-10-Right-Click-and-Open-The-Folder-With-VSCODE/IMG3.png){: .center-block :}

#### Third Step

Go into the Key: `command` and **Modify** the Default Data: `Program File Path\Code.exe %V`.
`%V` means that where you are. 

Now, you can try to right click where you want. 
![IMG](/img/2019-08-10-Right-Click-and-Open-The-Folder-With-VSCODE/IMG4.png){: .center-block :}

**OH NO! I have not press left shift yet!**

#### Fourth Step

Go into the Key: `Open Here In VS Code`, add a new String value and name it `Extended`.
Now, It just appear when you press left shift.

#### Fifth Step

How to ADD ICON to the option?
Go into the Key: `Open Here In VS Code`, add a new String value and name it `Icon`.
**Modify** the Data: `ICON File Path\ico.ico`.
![IMG](/img/2019-08-10-Right-Click-and-Open-The-Folder-With-VSCODE/IMG5.png){: .center-block :}

**OK! Get it!**

#### Sixth Step

If you want to run in admin account?
Go into the Key: `Open Here In VS Code`, add a new String value and name it `HasLUAShield`.
![IMG](/img/2019-08-10-Right-Click-and-Open-The-Folder-With-VSCODE/IMG6.png){: .center-block :}

### What about the Menu `Create New file` `Right Click the Folder Items` `Right Click the Items` ?
| Create New file               |HKEY_CLASSES_ROOT\Directory\Background\shellex\ContextMenuHandlers |
| Right Click the Items         |HKEY_CLASSES_ROOT\\*\shellex\ContextMenuHandlers                   |
| Right Click the Folder Items  |HKEY_CLASSES_ROOT\Directory\shellex\ContextMenuHandlers            |