# Unit Test
> https://github.com/flutter/flutter/wiki/Test-coverage-for-package:flutter

> https://atom.io/

> https://atom.io/packages/lcov-info

## install
1. Go to `https://atom.io/` dowload and install `Atom` application.
2. Open `Atom` application.
3. Go to `https://atom.io/packages/lcov-info` and install `lcov-info` package.

## run test
```
$ flutter test --coverage
```

## view coverage
1. Run test first to get `coverage/lcov.info`
2. Using Atom to open flutter project
3. To toggle Packages->Icov-info->Toggle
4. Open the code and see the color line.

## coverage report
### 1. Installation
#### 1.1. Installing in Ubuntu
```
sudo apt-get update -qq -y
sudo apt-get install lcov -y
```

####1.2. Installing in Mac
```
brew install lcov
```

### 2. Run tests, generate coverage files and convert to HTML
````
flutter test --coverage
genhtml coverage/lcov.info -o coverage/html
```
