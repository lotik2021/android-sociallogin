[![](https://jitpack.io/v/KosyanMedia/android-sociallogin.svg)](https://jitpack.io/#KosyanMedia/android-sociallogin)

# Social Login
### Library for authorizing in popular social networks

## Install

Include jitpack to repositories inside your root build.gradle file

```Groovy
allprojects {
    repositories {
        maven { url 'https://jitpack.io' }
    }
}
```

To include 'core' module add following string to your module build.gradle file

```Groovy
dependencies {
    compile 'com.github.lotik2021.android-sociallogin:sociallogin:x.y.z'
}
```
where ```x.y.z``` is the version of lib. You can find latest version in the badge on top of the page

Library is modular, you can include only those socials that you need. Just add appropriate
dependency to build.gradle file. But remember, that each module depends of 'core' module

For example if you need a facebook, you should add this line in build.gradle file

```Groovy
dependencies {
    ...
    compile 'com.github.lotik2021.android-sociallogin:facebook:x.y.z'
}
```

There is a list of modules:

```Groovy
compile 'com.github.lotik2021.android-sociallogin:facebook:x.y.z'
compile 'com.github.lotik2021.android-sociallogin:google:x.y.z'
compile 'com.github.lotik2021.android-sociallogin:odnoklassniki:x.y.z'
compile 'com.github.lotik2021.android-sociallogin:rx:x.y.z'
compile 'com.github.lotik2021.android-sociallogin:twitter:x.y.z'
compile 'com.github.lotik2021.android-sociallogin:vkontakte:x.y.z'
```

If module you want is not present here, you can implement it by yourself
Also you can contribute, by creating pull-requests =)

For instructions see appropriate social network module.

## Usage

All samples will be in Kotlin, [sample project is here][kotlin-sample]

If you use Java see [Java Sample][java-sample]

To login into some network you should call SocialLogin singleton

```Kotlin
SocialLogin.instance.loginTo(this, /* Activity */ FacebookNetwork(), object: SocialLoginCallback {
  
  override fun onLoginSuccess(socialNetwork: SocialNetwork, token: SocialToken){
    // your code  
  }
  
  override fun onLoginError(socialNetwork: SocialNetwork, errorMessage: Strig) {
    // your code
  }
})
```
Also you should redirect you onActivityResult() callback to SocialLogin

```Kotlin
override fun onActivtyResult(requestCode: Int, resultCode: Int, data: Intent?) { 
  SocialLogin.instance.onActivityResult(requestCode, resultCode, data)
  super.onActivityResult(requestCode, resultCode, data)
}
```

## Rx Java

First of all you should include sociallogin-rx module to your project

Social login supports RxJava 2. For use social login in rx maner Just replace **SocialLogin** with **RxSocialLogin**

```Kotlin
RxSocialLogin.instance.loginTo(this, /* Activity */ FacebookNetwork())
      .subscribe(
        { token -> /* do somthing with token */ },
        { error -> /* handle error */ }
      )
```

and in onActivityResult too


```Kotlin
override fun onActivtyResult(requestCode: Int, resultCode: Int, data: Intent?) { 
  RxSocialLogin.instance.onActivityResult(requestCode, resultCode, data)
  super.onActivityResult(requestCode, resultCode, data)
}
```


[java-sample]: https://github.com/lotik2021/android-sociallogin/tree/master/sample-java
[kotlin-sample]: https://github.com/lotik2021/android-sociallogin/tree/master/sample-kotlin
