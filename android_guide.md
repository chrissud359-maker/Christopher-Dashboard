# Converting Your Dashboard to a Native Android App

## Option 1 — WebView APK (easiest, ~2 hours)
This wraps your existing web app in a native Android shell.

### What you need
- A PC or Mac (not phone)
- Android Studio (free): developer.android.com/studio
- Java JDK 17+ (comes with Android Studio)

### Steps
1. Install Android Studio
2. New Project → Empty Views Activity → name it "CS Dashboard"
3. In MainActivity.java, replace the content with the WebView code (see below)
4. Put your index.html in app/src/main/assets/
5. Build → Generate Signed APK
6. Transfer APK to your Samsung and install

### MainActivity.java
```java
import android.webkit.*;
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        WebView webView = new WebView(this);
        setContentView(webView);
        WebSettings s = webView.getSettings();
        s.setJavaScriptEnabled(true);
        s.setDomStorageEnabled(true); // enables localStorage
        s.setAllowFileAccessFromFileURLs(true);
        webView.setWebChromeClient(new WebChromeClient());
        webView.loadUrl("file:///android_asset/index.html");
    }
}
```

### AndroidManifest.xml additions
```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```

---

## Option 2 — PWA Install (already done, easiest of all)
Your app already has the service worker and manifest built in.
1. Open Chrome on your Samsung
2. Go to your GitHub Pages URL
3. Tap three-dot menu → "Add to Home Screen"
4. Done — works offline, looks like a native app

---

## Option 3 — Full Native React Native App (advanced)
- Use Expo (expo.dev) — React Native framework
- I can write the full React Native codebase for you
- Builds to a real APK you can sideload or publish
- Full device access: notifications, background sync, widgets
- Requires Node.js on your PC

---

## Self-Updating via Claude (already built)
Your Claude tab can now update the app directly. Try saying:
- "Set my History deadline to May 2"
- "Pin a note: check Physics progress check"
- "Add vitamin C 1000mg to my supplements"
- "Log my weight as 178 lbs"
- "Update my pull-up PR to 12 reps"

Claude will execute these changes live in the app without any GitHub upload.

