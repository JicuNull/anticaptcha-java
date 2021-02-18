# Anti-Captcha API
This is a fork of [anti-captcha](https://github.com/AdminAnticaptcha/anticaptcha-java) to access the anti-captcha API in Java. The project has been converted to Gradle and has otherwise received only some minor changes compared to the original one. 
If you don't have an account yet, you can do that **[here](http://getcaptchasolution.com/bqdjn5xlgq)**

## Requirements
**Note**: The project is tested and compiled with Java 11

### Gradle
```java
allprojects {
    repositories {
	...
        maven { url 'https://jitpack.io' }
    }
}
```
```java
dependencies {
    implementation 'com.github.JicuNull:anticaptcha-java:v1.0'
}
```
Find more options here: **[Jitpack](https://jitpack.io/#JicuNull/anticaptcha-java)**

### Examples
- Recaptcha V2 with Proxy
```java
    DebugHelper.setVerboseMode(true);

    NoCaptcha api = new NoCaptcha();
    api.setClientKey("1234567890123456789012");
    api.setWebsiteUrl(new URL("http://http.myjino.ru/recaptcha/test-get.php"));
    api.setWebsiteKey("6Lc_aCMTAAAAABx7u2W0WPXnVbI_v6ZdbM6rYf16");
    api.setUserAgent("Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_6) AppleWebKit/537.36 " +
        "(KHTML, like Gecko) Chrome/52.0.2743.116");

    // proxy access parameters
    api.setProxyType(NoCaptcha.ProxyTypeOption.HTTP);
    api.setProxyAddress("xx.xxx.xx.xx");
    api.setProxyPort(8282);
    api.setProxyLogin("login");
    api.setProxyPassword("password");

    if (!api.createTask()) {
        DebugHelper.out("API v2 send failed. " + api.getErrorMessage(), DebugHelper.Type.ERROR);
    } else if (!api.waitForResult()) {
        DebugHelper.out("Could not solve the captcha.", DebugHelper.Type.ERROR);
    } else {
        DebugHelper.out("Result: " + api.getTaskSolution().getGRecaptchaResponse(), DebugHelper.Type.SUCCESS);
    }
```

- HCaptcha Proxyless
```java
    DebugHelper.setVerboseMode(true);

    HCaptchaProxyless api = new HCaptchaProxyless();
    api.setClientKey("1234567890123456789012");
    api.setWebsiteUrl(new URL("http://democaptcha.com/"));
    api.setWebsiteKey("51829642-2cda-4b09-896c-594f89d700cc");

    if (!api.createTask()) {
        DebugHelper.out("API v2 send failed. " + api.getErrorMessage(), DebugHelper.Type.ERROR);
    } else if (!api.waitForResult()) {
        DebugHelper.out("Could not solve the captcha.", DebugHelper.Type.ERROR);
    } else {
        DebugHelper.out("Result: " + api.getTaskSolution().getGRecaptchaResponse(), DebugHelper.Type.SUCCESS);
    }
```

**[More Examples](https://github.com/JicuNull/anticaptcha-java/blob/master/src/main/java/com/anti_captcha/Main.java)**
