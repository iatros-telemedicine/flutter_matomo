# flutter_matomo

Matomo tracking for flutter

Works on both **Android and/or iOS**.

[Dart package](https://pub.dev/packages/flutter_matomo)

[Gitlab link](https://gitlab.com/petleo-and-iatros-opensource/flutter_matomo)

## About

Matomo/Piwik tracking for flutter, this library is based on the android and the ios libraries provided by the Matomo team.
[Matomo Android](https://github.com/matomo-org/matomo-sdk-android/),

For help getting started with Flutter, view our 
[Matomo iOS](https://github.com/matomo-org/matomo-sdk-ios), which offers tutorials, 
samples, guidance on mobile development, and a full API reference.

## How to use 

#### Initialize Matomo/Piwik

```$xslt
await FlutterMatomo.initializeTracker('https://YOUR_URL/piwik.php', SITE_ID);
```

 **Important:** It does not matter if you are using piwik or matomo, you need to append **piwik.php and not matomo.php**

 
#### Adding a screen open event

If you have the BuildContext this will automatically add the widget name

```$xslt
await FlutterMatomo.trackScreen(context, "Screen opened")
``` 

If not or you want to enter a custom name then use this 

```$xslt
await FlutterMatomo.trackScreenWithName("SomeWidgetName", "Screen opened");
```

#### Extending out of the box TraceableWidgets

You can also use `TraceableStatefulWidget`, `TraceableStatelessWidget` & `TraceableInheritedWidget` Where you get a screen open event with the name of the widget out of the box

##### Example

Replace 
```$xslt
class HomeWidget extends StatefulWidget {
...
```
whith this
```$xslt
class HomeWidget extends TraceableStatefulWidget {
...
```

```$xslt
class HomeWidget extends TraceableStatefulWidget {
  HomeWidget({Key key}) : super(key: key, name: 'ONLY_IF_YOU_WANT_TO_OVERRIDE_THE_WIDGET_NAME');

  @override
  _HomeWidgetState createState() => _HomeWidgetState();
}
```


#### Tracking an event

If you have the BuildContext this will automatically add the widget name

```$xslt
await FlutterMatomo.trackEvent(context, "Sign up button", "Clicked");
``` 

If not or you want to enter a custom name then use this 

```$xslt
await FlutterMatomo.trackEventWithName("SomeWidgetName", "Sign up button", "Clicked");
```



#### Track app download (ONLY ON ANDROID)

```$xslt
await FlutterMatomo.trackDownload();
``` 



#### Track goal with id (ONLY ON ANDROID)

```$xslt
await FlutterMatomo.goal(GOAL_ID);
```



## Full Example

```$xslt
Future<void> initPlatformState() async {
    _matomoStatus = await FlutterMatomo.initializeTracker('https://YOUR_URL/piwik.php', SITE_ID);

    setState(() {});

    Future.delayed(Duration(seconds: 2), () async {
      _matomoStatus = await FlutterMatomo.trackScreen(context, "Screen opened");
      setState(() {});
    });

    Future.delayed(Duration(seconds: 4), () async {
      _matomoStatus = await FlutterMatomo.trackScreenWithName("This uses a name MyAppWidget", "Screen opened");
      setState(() {});
    });

    Future.delayed(Duration(seconds: 6), () async {
      _matomoStatus = await FlutterMatomo.trackEvent(context, "Sign up button", "Clicked");
      setState(() {});
    });

    Future.delayed(Duration(seconds: 8), () async {
      _matomoStatus = await FlutterMatomo.trackEventWithName("LoginWidget", "Login button", "Clicked");
      setState(() {});
    });

    Future.delayed(Duration(seconds: 10), () async {
      _matomoStatus = await FlutterMatomo.trackDownload();
      setState(() {});
    });

    Future.delayed(Duration(seconds: 12), () async {
      _matomoStatus = await FlutterMatomo.trackGoal(1);
      setState(() {});
    });

    if (!mounted) return;
  }
``` 



