[![](https://jitpack.io/v/ankit1057/ProgressiveStatusBar.svg)](https://jitpack.io/#ankit1057/ProgressiveStatusBar)


# ProgressiveStatusBar
Another way to show progress. A progress View over the system StatusBar.
in addition to showing a toast message.


## Setup
1- Add jitpack.io repositories to you project `build.gradle`
```groovy 
allprojects {
	repositories {
	    maven { url 'https://jitpack.io' }
	}
}
```
2- Add it as a dependency to your app `build.gradle`
```groovy
dependencies {
	implementation 'com.github.ankit1057:ProgressiveStatusBar:Tag'
}
```
3- Add `SYSTEM_ALERT_WINDOW` permission "unnecessary if your app's targetSdkVersion => oreo"
```xml
    <!--unnecessary if your app's minSdkVersion => oreo-->
    <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
```

## Usage
1- In your Activity class

```java
public class MainActivity extends AppCompatActivity {

    ProgressStatusBar mProgressStatusBar;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.acitivity_main);
	
	//initialize
        mProgressStatusBar = new ProgressStatusBar(this); 
	
	//show progress
        mProgressStatusBar.setFakeProgress(3000,true); //make fake progress from 0 to 100 in 3 sec. true/false for display the percentage text.
	//or
        mProgressStatusBar.setProgress(60,false); //set progress value manually
	//or
        mProgressStatusBar.setWaiting(6000); //show waitting balls for 6 sec.
	
	//show toast message
	mProgressStatusBar.showToast("1 new message", 3000); //(Sting message, int duratoion)
		
	/*Addidional*/
	//options, anytime before you start a new progress 
	mProgressStatusBar.setProgressColor(COLOR);//default #40212121
	mProgressStatusBar.setProgressTextColor(COLOR);//default #ffffff
	mProgressStatusBar.setProgressBackgroundColor(COLOR);//default transparent or colorPrimaryDark
	mProgressStatusBar.setBallsColor(COLOR);//default #ffffff

	//Listener
        mProgressStatusBar.setProgressListener(new ProgressStatusBar.OnProgressListener() {
            public void onStart() {
                //ex: lock the UI or tent it
            }
            public void onUpdate(int progress) {
                //ex: simulate with another progressView
            }
            public void onEnd() {
                //ex: continue the job
            }
        });
	
    }

    @Override
    protected void onPause() {
        mProgressStatusBar.remove(); //remove progress view in case user went out before the progress end
        super.onPause();
    }
    
}
```




