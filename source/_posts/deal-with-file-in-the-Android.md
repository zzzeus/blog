---
title: deal with files in a Android app
date: 2017-05-20 18:41:50
tags:
---


## how to work when a app run

A app need to save some data After it achieve information and need to save something when user changed some settings.

## the functions the app need

* create app directory and some kinds of directories such as images,text and so on.
* save some data when we download some data which will not be changed temporarily.And we should use individual names to distinguish the kind of data.
* check whether the data has saved.If it has been saved, get it from the storage and deal with it.If it does not exist,download and save it.

## Detail

### permission
{% codeblock  permission %}
// app should ask for the permission
 <manifest ...>    
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> 
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" /> 
 </manifest> 
{% endcodeblock %}

***
To get external storage:  ```Environment.getExternalStorageDirectory();```
To create a file       :  
```
new File(String parent,String name), 
f.createNewFile()//check is existed and if existed delete it 
```

```
//To write file,use         
fos=new  FileOutputStream(File)
bw=new OutputStreamWriter(fos,"UTF-8");
bw.write(content);

//To read file, use         
fis=new FileInputStream(f);
fis.read(bs);

//To be effective,we should read the whole content from a small size file.And then decode the bytes to strings.
byte[] bs=new byte[(int) f.length()];
fis=new FileInputStream(f);
fis.read(bs);//we need close it.
String content= new String(bs,"UTF-8");
```