# YuluDimension

Android Native Dimensions for all mobile devices 

**Installation**

Add the Following to your gradle file.

***Add it in your root build.gradle at the end of repositories:***

```java
         allprojects {
            repositories {
              ...
              maven { url 'https://jitpack.io' }
            }
         }
```

***Add the dependency***

```java
          implementation 'com.github.saurabhYulu:YuluDimension:1.0.0'
```

***Android introduced the “Smallest Width (SW)” qualifier in Android 3.2.***

The Smallest-width qualifier allows to target screens that have a certain minimum width given in dp.

Lets take three layout folders named res/layout, res/layout-sw600dp and res/layout-sw720dp. We also have some layouts named main.xml, details.xml and item.xml in base layout folder. We override details.xml, item.xml in res/layout-sw600dp folder and item.xml in res/layout-sw720dp folder.

```java

                  res/layout
                     main.xml
                     details.xml
                     item.xml

                  res/layout-sw600dp       // 7.0”  tablet 1024x600 mdpi
                     details.xml
                     item.xml
                  res/layout-sw720dp       // 10.1” tablet 1280x800 mdpi
                     item.xml
                     
```                     
**On a device with dimensions 640 x 360 dp.**

Between 640 and 360 the smallest width is 360 dp. Now the device will compare this smallest width with the folder name. As 360dp is less than 600dp and less than 720dp. So all the layout will come from res/layout folder.
All the layout will come from res/layout folder.

**On a device with dimensions 1024 x 600 dp.**

Here, Between 1024dp and 600dp the smaller one is 600dp. Now compare this value agains the folder name. 600dp is equal to the 2nd folder res/layout-sw600dp. So details.xml and item.xml will come from this folder. But notice that main.xml is not declared in this folder. So it fall back to a less specific folder which is base folder. So main.xml will come from res/layout folder.

details.xml and item.xml will come from res/layout-sw600dp
main.xml will come from res/layout folder.

**On a device with dimensions 1280 x 800 dp.**

Here between 1280 and 800 dp the smaller one is 800 dp. If you compare this value you will see it satisfies all the folders. However, the device will choose most specific folder first which is res/layout-sw720dp. So item.xml will come from res/layout-sw720dp folder. But details.xml and main.xml is defined in this folder. So now the device will fall back to less specific folder which is res/layout-sw600dp. So detail.xml will come from this folder. But main.xml is not also defined here. So main.xml will come from base layout folder. item.xml will come from res/layout-sw720dp detail.xml will come from res/layout-sw600dp. main.xml will come from res/layout folder.
