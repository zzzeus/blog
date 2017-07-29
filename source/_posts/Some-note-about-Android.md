---
title: Some note about Android
date: 2017-05-27 23:26:02
categories:
- Android
tags:
---

### Today's note 2017-05-27

* Floating window in Android (WindowManager,Toast) 
* play m3u8 by Exoplayer
* check installed app
* check the permission
* create a Popwindow
* SharedPreferences

#### Floating window in Android
{% codeblock %}
//1,get a WindowManager by using 
getApplication().getSystemService(Context.WINDOW_SERVICE) 
//or using 
Activity.this.getWindowManager() //it only can be used on the activity it belongs to

//2,set the WindowManager.LayoutParams :type(TYPE_SYSTEM_ALERT),format,flags,gravity and x,y ,width,height (LayoutParams.WRAP_CONTENT)

//3,then add the view  
windowManager.addView(View,LayoutParams)

//4,remove when it no longer needed
windwoManager.removeView(View)
{% endcodeblock %}

#### play m3u8 by Exoplayer
{% codeblock %}
//1,prepare the TrackSelector  ..(BandwidthMeter,) about the newwork
//2,prepare the source         ..()  about the uri ,app which called it   we can find some kind of source
//3,new a ExoPlayer and prepare the source
{% endcodeblock %}

#### check installed packages

#### check permission