---
title: Getting LibSVM to work with Weka on Mac（reprint）
tags:
  - Weka
url: archives/696/index.html
id: 696
categories:
  - Default Category
date: 2013-06-21 07:47:08
---

Somehow, the only way to use LibSVM with Weka is by using the bash command-line.
I have tried the second method successfully. As for you , etheir is good.

Step 1: Get Weka.Assume the bleeding edge version 3.7.0. Unzip and put in /Applications folder.

Step 2: Get LibSVM.
a. Iowa State site ([http://www.cs.iastate.edu/~yasser/wlsvm/wlsvm.zip](http://www.cs.iastate.edu/~yasser/wlsvm/wlsvm.zip)):
If you use Safari to download, it will be unzipped in the Downloads directory. The files you need are ~/Downloads/WLSVM/lib/wlsvm.jar and /Downloads/WLSVM/lib/libsvm.jar
b. Taiwan site([http://www.csie.ntu.edu.tw/~cjlin/libsvm/libsvm-2.89.zip](http://www.csie.ntu.edu.tw/~cjlin/libsvm/libsvm-2.89.zip)):
Using Safari to download, the file you need is ~/Downloads/libsvm-2.89/java/libsvm.jar

Step 3: Open Terminal and copy to Weka.app. Assume you have privileges to write into Weka.app.
a. Iowa State version:
$ cp ~/Downloads/WLSVM/lib/*.jar /Applications/Weka/weka-3-7-0.app/Contents/Resources/Java
b. Taiwan version:
$ cp ~/Downloads/libsvm-2.89/java/libsvm.jar /Applications/Weka/weka-3-7-0.app/Contents/Resources/Java

Step 4: Set CLASSPATH
$ export CLASSPATH=$CLASSPATH:/Applications/Weka/weka-3-7-0.app/Contents/Resources/Java/
Step 5:Run Weka from Terminal!
$ java -classpath $CLASSPATH:weka.jar:libsvm.jar weka.gui.GUIChooser &

Another method below:
1.copy the libsvm.jar and wvsvm.jar into the app folder like told in the blog

2.edit weka.appinfo.plist file in textedit

After ClassPath 
and the array start tag you'll see
$JAVAROOT/weka.jar within string tags
copy that whole line and make two copies directly below it
edit the new copies to say
$JAVAROOT/libsvm.jar in one 
and 
$JAVAROOT/wlsvm.jar in the other