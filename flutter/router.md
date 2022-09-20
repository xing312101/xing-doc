# Router
> Navigation and routing: https://flutter.dev/docs/cookbook/navigation

```
Navigator.of(context).pushNamedAndRemoveUntil('/a_page', (Route<dynamic> route) => false);

Navigator.of(context).pushNamed('/b_page');
```

#### main.dart:
> onGenerateRoute

> onUnknownRoute

```
void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "Hello Flutter",
      theme: ThemeData(
        primaryColor: Colors.red
      ),
      initialRoute: '/travel_blog',
      onGenerateRoute: AppRoute.onGenerateRoute,
      onUnknownRoute: AppRoute.onUnknownRoute,
    );
  }
}
```

#### routes.dart
```
class AppRoute{
  static Route<dynamic> onGenerateRoute(RouteSettings settings) {
    MaterialPageRoute nextPage;
    switch (settings.name) {
      case '/a_page':
        inspect(settings);
        nextPage = MaterialPageRoute<dynamic>(builder: (context) => APage());
        break;
      case '/b_page':
        inspect(settings);
        nextPage = MaterialPageRoute<dynamic>(builder: (context) => BPage());
        break;
      default:
        nextPage = onUnknownRoute(settings);
    }
    return nextPage;
  }

  static Route<dynamic> onUnknownRoute(RouteSettings settings) {
    return MaterialPageRoute<dynamic>(
      settings: settings,
      builder: (context) => ErrorPage('Not Found'),
    );
  }
}
```

#### error_page.dart
```
class ErrorPage extends StatelessWidget {
  final String errorMessage;

  ErrorPage(this.errorMessage);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        body: Center(
            child: Text(errorMessage)
        )
    );
  }
}

```


