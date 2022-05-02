---
title: java block
tags:
  - Java
url: archives/702.html
id: 702
categories:
  - Default Category
date: 2014-07-27 20:22:08
---

目前，我遇到过两种JAVA block的情况.
一种是在建立http流之后，用conn.getInputStream().read()的时候block掉，这种情况通常是流再打开之后，网络出问题或者对方服务器问题等等。

通常写法是

while((is.read(buffer))!=-1){
do something
}

网上通常的解决办法是用socket 来看是否超时，我的解决办法是
循环不要以is.read(buffer)作为判断语句。而是用is.available()做判断，如果availab总是返回0值，那么退出重连，这其实相当于自己判断是否block掉了。

另外一个就是在执行Runtime.getRuntime().exec(script)的时候，由于script报错太多，没有即使读取出来，导致java被block掉。

把网上的解决方案给大家。转自http://saluya.iteye.com/blog/1260347 <!--more-->

```
Process proc = Runtime.getRuntime().exec(strMakePathPath);        
StreamGobbler errorGobbler = new StreamGobbler(proc.getErrorStream(), "Error");        
StreamGobbler outputGobbler = new StreamGobbler(proc.getInputStream(), "Output");        
errorGobbler.start();        
outputGobbler.start();        
proc.waitFor();

public class StreamGobbler extends Thread {       
    InputStream is;        
    String type;        

    public StreamGobbler(InputStream is, String type) {        
            this.is = is;        
            this.type = type;        
    }        

    public void run() {        
            try {        
                    InputStreamReader isr = new InputStreamReader(is);        
                    BufferedReader br = new BufferedReader(isr);        
                    String line = null;        
                    while ((line = br.readLine()) != null) {        
                            if (type.equals("Error")) {        
                                    System.out.println("Error   :" + line);        
                            } else {        
                                    System.out.println("Debug:" + line);        
                            }        
                    }        
            } catch (IOException ioe) {        
                    ioe.printStackTrace();        
            }        
    } 
}  
```

