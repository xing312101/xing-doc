# test code
> https://flutter.dev/docs/testing

## Unit tests
```
  void main() {
    group('group 1', () {
      test('1 = 0', () {
        expect(1, 0);
      });
      test(' 0= 0', () {
        expect(0, 0);
      });
    });
  }
```

### mocking
> https://flutter.dev/docs/cookbook/testing/unit/mocking

#### package dependencies
```
dependencies:
  http: <newest_version>
dev_dependencies:
  flutter_test:
    sdk: flutter
  mockito: <newest_version>
  build_runner: <newest_version>
```



#### code
```
  Future fetchData(http.Client client) async {
    final response = await client.get(Uri.parse('https://xing312101/hello'));

    if (response.statusCode == 200) {
      // If the server did return a 200 OK response,
      // then parse the JSON.
      return jsonDecode(response.body);
    } else {
      // If the server did not return a 200 OK response,
      // then throw an exception.
      throw Exception('Failed to load album');
    }
  }
```

#### generate the mock
```
import 'package:mockito/annotations.dart';

// Generate a MockClient using the Mockito package.
// Create new instances of this class in each test.
@GenerateMocks([MockClassName])
void main() {
}

$  flutter pub run build_runner build

```


####  mock test
```
@GenerateMocks([http.Client])
void main() {
  group('mock test', () {
    test('returns an Album if the http call completes successfully', () async {
      final client = MockClient();

      // Use Mockito to return a successful response when it calls the
      // provided http.Client.
      when(client.get(Uri.parse('https://xing312101/hello'))).thenAnswer((_) async => http.Response('{"hello": 123, "world": "234"}', 200));

      expect(await fetchData(client), XXXXXX);
    });
  });
}
```

## Widget testing
> https://flutter.dev/docs/cookbook/testing/widget

```
testWidgets('Hello test widget', (WidgetTester tester) async {
    // await tester.pumpWidget(WidgetNameOrBuild);
    await tester.pumpWidget(HelloWidget());
    await tester.pumpWidget(
        MaterialApp(
            home: Material(
                child: Builder(
                    builder: (BuildContext context) {
                        return Container();
                    },
                ),
            ),
        )
    );

});
```

### finder
```
final textFinder = find.text('textString');
final textFinder = find.byKey(Key('keyId'));

```

### enterText, tap, drag
```
testWidgets('...', (WidgetTester tester) async {
  // enterText
  await tester.pumpWidget(HelloWidget());
  await tester.enterText(find.byType(TextField), 'hello');

  // tap
  await tester.tap(find.byType(FloatingActionButton));
  await tester.pump(); // rebuild
  // Expect to find the item on screen.

  // drag
  // Swipe the item to dismiss it.
  await tester.drag(find.byType(Dismissible), const Offset(500.0, 0.0));
  await tester.pumpAndSettle();

});
```




