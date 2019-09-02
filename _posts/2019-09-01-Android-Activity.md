---
layout: post
comments: true
categories: [Java, Android]
---

# Basic ideas here
* FirstActivity -> NextActivity
	* Make Intent
	* Set Extra
	* call startActivity(*Intent*)
* FirstActivity -> NextActivity -> FirstActivity(Back)
	* In FirstActivity
		* Make Intent
		* Set Extra
		* call startActivityForResult(*Intent*, *requestCode*)
			* requestCode has to be an integer greater than zero.
	* In NextActivity
		* Make Intent
		* Set Extra
		* Set resultCode and Intent with setResult(*requestCOde*, *intent*)
		* call finish()

# Simple Activity change
When you want to change screen on your Android app, you need to call another activity.

When you want to change activity, you need to use Intent class and startActivity().
When you want to pass the data, you can put Extra to Intent.

MainActivity.java
```java 
Intent intent = new Intent(this, MainActivity.class);
intent.putExtra("com.yourdomain.appName.MESSAGE", "Message here!");
startActivity(intent);
```

NextActivity.java
To get the message from MainActivity.
```java
Intent intent = getIntent();
String str = intent.getStringExtra("com.yourdomain.appName.MESSAGE");
```

# When your activity comes from another activity

When your activity comes back from next activity. You need to use startActivityForResult.

MainActivity.java
```java
Intent intent = new Intent(this, MainActivity.class);
intent.putExtra("com.yourdomain.appName.MESSAGE", "Message here!");
startActivityForResult(intent, 1); //startActivityForResult(Intent, requestCode)
```
Request code should be unique and best practice is declare static final int in the class.
You need to select a number greater than zero for the requestCode.

When you want to go back to the activity you came.
NextActivity.java
```java
Intent intent = new Intent(this, MainActivity.class);
intent.putExtra("com.yourdomain.appName.RETURN_MESSAGE", "This is return");
setResult(Actibity.RESULT_OK, intent);
finish()
```
MainActivity.java
Once active actibity returns previous activity, onActivityResult is called.

```java
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {

    if (requestCode == 1) {
        if(resultCode == Activity.RESULT_OK){
            String result=data.getStringExtra("com.yourdomain.appName.RETURN_MESSAGE");
        }
        if (resultCode == Activity.RESULT_CANCELED) {
        	...
        }
    }
}
```



categories: [Java, Android]
