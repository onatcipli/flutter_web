# flutter_web Medium

[Flutter Web, Github Actions and Github Pages article, (automation CI&CD)](https://medium.com/flutter-community/flutter-web-github-actions-github-pages-dec8f308542a)

**flutter_build_publish_web.yml** file : 
```
name: Flutter Web
on:
  push:
    branches:
      - master
jobs:
  build:
    name: Build Web
    env:
      my_secret: ${{secrets.commit_secret}}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1
      - uses: subosito/flutter-action@v1
        with:
          channel: 'dev'
      - run: flutter config --enable-web
      - run: flutter pub get
      - run: flutter build web --release
      - run: |
          cd build/web
          git init
          # type configurations: your user.email and user.name followed lines 
          # git config --global user.email your_email 
          # git config --global user.name your_name 
          git config --global user.email onatcipli@outlook.com
          git config --global user.name onatcipli
          git status
          # change this remote url for examle your remote url is https://github.com/onatcipli/flutter_web.git then the following:
          git remote add origin https://${{secrets.commit_secret}}@github.com/onatcipli/flutter_web.git
          git checkout -b gh-pages
          git add --all
          git commit -m "update"
          git push origin gh-pages -f
```


A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://flutter.dev/docs/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://flutter.dev/docs/cookbook)

For help getting started with Flutter, view our
[online documentation](https://flutter.dev/docs), which offers tutorials,
samples, guidance on mobile development, and a full API reference.
