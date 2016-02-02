---
id: 70
title: 'Using Tasker to Record the Location of an Android Device [Part 2]'
date: 2011-04-01T18:54:38+00:00
author: William S Godfrey
layout: post
guid: http://www.williamsgodfrey.com/?p=70
permalink: /using-tasker-to-record-the-location-an-android-device-part-2/
dsq_thread_id:
  - 2021358279
categories:
  - Tasker
tags:
  - Android
  - Droid X
  - GPS
  - Location
  - Stolen Phone
  - Tasker
---
<span style="color: #999999;"><em>[This is Part 2 of a 2 part series discussing the use of the Tasker application to record the location of a device running Google&#8217;s Android mobile OS. This part discusses <em><em>how to set up the Tasker profile </em>and my first impressions</em>; <a href="http://www.williamsgodfrey.com/using-tasker-to-record-the-location-an-android-device-part-1/">Part 1</a> discusses <em>what lead me to use the Tasker application</em>.]</em></span>

In the writeup that follows, I assume that the reader is familiar with the [Tasker for Android](http://tasker.dinglisch.net/) application. If something doesn&#8217;t seem to make sense, please feel free to leave a comment or contact me via Twitter or email.

### <span style="color: #000000;">Setting Up the Profile in Tasker</span>

  1. <div style="float: right;">
      <a href="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/firstcontexttime.png"><img class="aligncenter size-medium wp-image-79" title="firstcontexttime" alt="" src="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/firstcontexttime-300x241.png" width="300" height="241" srcset="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/firstcontexttime-300x241.png 300w, http://www.williamsgodfrey.com/wp-content/uploads/2011/04/firstcontexttime-1024x824.png 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </div>
    
    Begin by setting up a new profile, I named mine &#8220;Tweet Loca.&#8221;</li> 
    
      * We want the profile to run continuously in the background whenever the phone is on. Therefore, we want a time context so after naming the profile we will select **Time** from the &#8216;First Context&#8217; menu that pops up. As shown in the figure to the right, I used the current time for the &#8216;From:&#8217; time and one minute _before_ the current time for the &#8216;To:&#8217; time. I also set the profile to repeat every 15 minutes in the &#8216;Repeat:&#8217; section.</ol> 
    
    ### Defining the Actions in Tasker (aka Tasks)
    
      1. <div style="float: right;">
          <a href="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/firsttasklocation.png"><img class="size-large wp-image-88 alignright" title="firsttasklocation" alt="" src="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/firsttasklocation-1024x567.png" width="445" height="246" srcset="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/firsttasklocation-300x166.png 300w, http://www.williamsgodfrey.com/wp-content/uploads/2011/04/firsttasklocation-1024x567.png 1024w, http://www.williamsgodfrey.com/wp-content/uploads/2011/04/firsttasklocation.png 1540w" sizes="(max-width: 445px) 100vw, 445px" /></a>
        </div>
        
        The first task to be run will update the value currently stored in the Tasker variable _%LOC_ if the most recent GPS fix occurred more than 15 minutes prior. This is done because I found that often the phone has not had a reason to find its GPS position recently, making any current values stored in _%LOC_ outdated and useless. So for the first Task, first select from the &#8216;Select Action Category&#8217; menu and then **Get Location** from the &#8216;Select Misc Action&#8217; menu. For &#8216;Source&#8217; we will select GPS, and we&#8217;ll check the &#8216;If&#8217; box and enter _%GPS_AGE,_ >, and &#8216;5&#8217; in the &#8216;If&#8217; input boxes. See the image to the right. Don&#8217;t worry about the _%GPS_AGE_ variable, we&#8217;ll define it soon enough.</li> 
        
          * <div style="float: right;">
              <a href="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/GPSAGEdefine.png"><img class="aligncenter size-large wp-image-97" title="GPSAGEdefine" alt="" src="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/GPSAGEdefine-1024x567.png" width="445" height="246" srcset="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/GPSAGEdefine-300x166.png 300w, http://www.williamsgodfrey.com/wp-content/uploads/2011/04/GPSAGEdefine-1024x567.png 1024w, http://www.williamsgodfrey.com/wp-content/uploads/2011/04/GPSAGEdefine.png 1540w" sizes="(max-width: 445px) 100vw, 445px" /></a>
            </div>
            
            The next few Tasks will define the variables we&#8217;ll need for the profile to properly report the locations of the phone. Add another Task (push the &#8216;+&#8217; button in the lower left corner of the profile window), select **Variable** from the &#8216;Select Action Category&#8217; menu  and then **Variable Set** from the &#8216;Select Variable Action&#8217; menu. For &#8216;Name,&#8217; enter _%GPS\_AGE\_SEC_, for &#8216;To,&#8217; enter _%TIMES &#8211; %LOCTMS_, and check the &#8216;Do Maths&#8217; box. See image at right. This defines a variable for the time since the last GPS fix in seconds, _%GPS\_AGE\_SEC,_ as the time of the last GPS fix in seconds, _%LOCTMS_, subtracted from the current time in seconds, _%TIMES_.</li> 
            
              * Select **Variable Set** again. This time for &#8216;Name,&#8217; enter _%GPS_AGE_, for &#8216;To,&#8217; enter _%GPS\_AGE\_SEC / 60_, and check the &#8216;Do Maths&#8217; box. This converts _%GPS\_AGE\_SEC_ to units of minutes, which is what we&#8217;ll use to report the GPS fix age.
              * Select **Variable Set** again. This time for &#8216;Name,&#8217; enter _%NET\_AGE\_SEC_, for &#8216;To,&#8217; enter _%TIMES &#8211; %LOCNTMS_, and check the &#8216;Do Maths&#8217; box. This defines a variable for the time since the last wifi location fix in seconds, _%NET\_AGE\_SEC,_ as the time of the last wifi fix in seconds, _%LOCNTMS_, subtracted from the current time in seconds, _%TIMES_. We do this because we&#8217;lll report our net location as well, as a backup to determine the reliability of our GPS data.
              * Select **Variable Set** again. This time for &#8216;Name,&#8217; enter _%NET_AGE_, for &#8216;To,&#8217; enter _%NET\_AGE\_SEC / 60_, and check the &#8216;Do Maths&#8217; box. This converts _%NET\_AGE\_SEC_ to units of minutes, which is what we&#8217;ll use to report the wifi location fix age.
              * Select **Variable Set** again. This time for &#8216;Name,&#8217; enter _%LOCACC_FT,_ for &#8216;To,&#8217; enter ___%LOCACC * 3.281__,_ and check the &#8216;Do Maths&#8217; box. This defines a variable used to store the accuracy of the last GPS fix in feet, _%LOCACC_FT_, by converting the built in Tasker variable, ___%LOCACC___, from units of meters to units of feet.
              * Select **Variable Set** again (last variable!). This time for &#8216;Name,&#8217; enter _%LOCNACC_FT,_ for &#8216;To,&#8217; enter ___%LOCNACC * 3.281__,_ and check the &#8216;Do Maths&#8217; box. This defines a variable used to store the accuracy of the last wifi location fix in feet, _%LOCNACC_FT_, by converting the built-in Tasker variable, ___%LOCNACC___, from units of meters to units of feet.
              * So all our variables are now set up and the only thing left to do is report them. I found having the phone automatically tweet it&#8217;s location to [a &#8216;locked&#8217; Twitter account](http://twitter.com/#!/wsglocation) works best for me. I was originally storing the phone&#8217;s location to a local text file but, after leaving my phone at work one night, realized that when I do that, all the data is on the phone. If the phone were to be lost or stolen, there would be no way of tracking it using this Tasker Profile. By tweeting to a locked twitter account, I can log in and see where the phone is, remotely, while still keeping the data private.
              * [<img class="alignright size-large wp-image-111" title="SendSMSdefine" alt="" src="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/SendSMSdefine-1024x567.png" width="445" height="246" srcset="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/SendSMSdefine-300x166.png 300w, http://www.williamsgodfrey.com/wp-content/uploads/2011/04/SendSMSdefine-1024x567.png 1024w, http://www.williamsgodfrey.com/wp-content/uploads/2011/04/SendSMSdefine.png 1540w" sizes="(max-width: 445px) 100vw, 445px" />](http://www.williamsgodfrey.com/wp-content/uploads/2011/04/SendSMSdefine.png) Select **Phone** from the &#8216;Select Action Category&#8217; menu and then **Send SMS** from the &#8216;Select Phone Action.&#8217; In the &#8216;Number&#8217; field enter &#8220;40404&#8221;. This is Twitters number for mobile tweets. I will go into more depth in a future post about integrating Twitter and your mobile device. In the &#8216;Message&#8217; field enter &#8220;GPS Loc: _%LOC_, GPS Acc: _%LOCACC_ ft, GPS Age: _%GPS_AGE_ min&#8221;. See photo at right.
              * And finally, select **Phone** from the &#8216;Select Action Category&#8217; menu and then**Send SMS** from the &#8216;Select Phone Action&#8217; again. In the &#8216;Number&#8217; field enter &#8220;40404&#8221;, in the &#8216;Message&#8217; field enter &#8220;Wifi Loc: _%LOCN_, Wifi Loc Acc: _%LOCNACC_ ft, Wifi fix Age: _%NET_AGE_ min&#8221;.</ol> 
            
            ### Using the Profile
            
            <div style="float: right;">
              <a href="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/sampletweets.png"><img class="alignright size-full wp-image-120" title="sampletweets" alt="" src="http://www.williamsgodfrey.com/wp-content/uploads/2011/04/sampletweets.png" width="230" height="291" /></a>
            </div>
            
            I&#8217;ve had the profile running for a few days now and it appears to be working really well! As the image to the right shows, both the location from the GPS and wifi signals (for an explanation of how a location can be determined see this [Google Mobile Blog post](http://googlemobile.blogspot.com/2008/10/my-location-now-with-wi-fi.html)) are reported. The GPS accuracy typically bounces between 96 and 68 ft; the wifi accuracy is typically around 100ft. The GPS fix age ranges from 30 second to 15 minutes and the wifi location fix age is typically less than 30 seconds old. The wifi location fix age, obviously, is much older when the phone is not picking up a wifi signal. Note, though, that the phone does not need to be connected to the wifi signal and transmitting data to use it to determine location. The phone only needs to pick up and identify the wifi signal, i.e. location can be &#8220;pulled&#8221; from a locked wifi signal.
            
            Battery drain appears to be minimal. The Tasker profile was running for a 20 hour period and the battery was only down to about 15% when the phone was plugged into the charger. This is typically of my battery life.
            
            I&#8217;ll report further as I tweak/fix the system.