---
title: EndNote Mac--Error while reading serialized data in Word
tags:
  - Endnote
  - Mac
url: archives/703.html
id: 703
categories:
  - Default Category
date: 2014-03-03 09:25:12
---

Mac下的Endnote从X6换成X7后，word中的插入工具还是X6，插入文献时提示"Error while reading serialized data"

After upgrading the EndNote software, Word still shows older version of EndNote tools and displays an "Error while reading serialized data". This problem may happen if the older version of EndNote was not uninstalled properly using Customizer and that the older version CWYW tools are loading in Word.
1 Make sure to close all Office programs and then open your hard drive.
2 Navigate to your Word startup folder. This path is usually [Applications: Microsoft Office 2011: Office: Startup: Word].
3 Take any files from this 'Word' folder and drag them out to the Desktop.
4 Open EndNote.
5 In EndNote, click on the EndNote menu and choose "Customizer..."
6 On the Customizer window, make sure "Cite While You Write" is checked.
7 Click the "Next" button twice and then press "Done" to close the Customizer window.
8 Open Word again to see if the latest EndNote tools are now loading.<!--more-->

If a previous version EndNote is found on the computer, you would need to uninstall any previous version by following the below steps,
1 Open EndNote from Applications: EndNote.
2 Go to the Endnote Menu and select Customizer.
3 Click the Uninstall button and follow the prompts.
When this is done, open a Finder window and go into your Applications folder. Drag the EndNote folder to the Trash and then empty the Trash. This should completely remove the older version of EndNote from the computer. You can then run the Customizer for the latest version installed to install the tools in Word.

If the steps described above do not resolve the problem the next step is to reset some of the Word preferences.

Quit Word.

For Word 2011 go to ~/Library/Application Support/Microsoft/Office/User Templates. Move Normal.dotm to the Desktop.

Next go to ~/Library/Application Support/Microsoft/Office/Preferences/Office 2011. Move Office Registration Cache and OLE Registration Database to the Desktop.

Next go to ~/Library/Preferences. Move com.microsoft.Word.plist and com.microsoft.visual_basic.plist to the Desktop. If there is a file called com.microsoft.visualbasic.plist move it to the Desktop.

Finally go to ~/Library/Preferences/Microsoft/Office 2011. If Office Registration Cache and OLE Registration Database are in this folder move them to the Trash.

For Word 2008 go to ~/Library/Application Support/Microsoft/Office/User Templates. Move Normal.dotm to the Desktop.

Next go to ~/Library/Preferences. Move com.microsoft.Word.plist to the Desktop.

Finally go to ~/Library/Preferences/Microsoft/Office 2008. Move OLE Registration Database 2008 and OLE Registration Database 2008 to the Desktop.

After the preference files have been removed, start Word and click on Word > Preferences > File Locations > Startup > Modify. For Word 2008 set the location of startup to /Applications/Microsoft Office 2008/Office/StartupWord For Word 2011 set the location of startup to Applications/Microsoft Office 2011/Office/StartupWord

Click on OK to close the preferences, quit Word, reopen Word and try to use the EndNote commands.

origin from: http://kbportal.thomson.com/display/2/index.aspx?tab=browse&c=&cpc=&cid=&cat=&catURL=&r=0.1051736