+++
title = "Developing for Google Glass"
date = "2014-01-16T15:25:17"
+++



Some caveats to a good glass app
Inspired by the good principals of a good web app.


+ follows similar style and UX principals in other apps
+ natural usage in day to day life.
+ GDK on the client, voice recognition and translate avaliable on the client.
+ Standard Android API and Paradigms

+ Types  		- invocation  - elements
  GDK     		OK GLASS
  MIRROR  		MENU ITEM
  GDK + Mirror  Timeline card
Gesture Detector - touch pad movement
Voice Trigger - specify use
Card Scroller & Cards(builder)- build timeline cards and arrange to scroll through them
Live Card - real time info


GDK
----
Live card -> real time updates
Static Card -> moment in time
Immersion - "word lens "
Service  - "settings"

Four Development patterns
- Sharing
- Periodic Notification
New Patterns
- on going tasks - information or interaction:
- Immersion  -Enter into a specific experience and then getting back into it


Tips
====
Add flag to keep the screen on,


```java
public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_flag);
        getWindow().addFlags(WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON);
}


//can be removed with
getWindow().clearFlags(WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON);
```

Start the camera intent
```java
startActivity();

		//camera pic taking
Intent cameraIntent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE, null);
startActivityForResult(cameraIntent, 1);

```

keep the  camera unscrambled
 http://stackoverflow.com/questions/19235477/google-glass-preview-image-scrambled-with-new-xe10-release

```java
parameters.setPreviewFpsRange(30000, 30000);
/*
    Camera.Parameters params = camera.getParameters();
    params.setPreviewFpsRange(30000, 30000);
    camera.setParameters(params);
*/

```

open url
```java
		//url opening
		String url = "https://mobile.xtuple.com";
		Intent intent = new Intent(Intent.ACTION_VIEW);
		intent.setData(Uri.parse(url));
		startActivity(intent);

```

trying to build to something shell proprerties
```java
Google Inc.:Glass Development Kit Sneak Peek:15
```

on keydown, emit something
```java
    @Override
    public boolean onKeyDown(int keycode, KeyEvent event) {
        if (keycode == KeyEvent.KEYCODE_DPAD_CENTER) {
            openOptionsMenu();
            Log.v("@@@@","TEST");
            return true;
        }
        return false;
    }
```

Insert a card into the timeline via gdk
```java

		mTimelineManager = TimelineManager.from(this);
		Card card = new Card(this);
		card.setText("Hello World").setFootnote("Footer").addImage(R.drawable.ic_launcher);
		mTimelineManager.insert(card);

```
