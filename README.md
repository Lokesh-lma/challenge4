
name: lomayoga site CI

on:
  push:
    branches: [ "master" ]
  pull_request:
    branches: [ "master" ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - name: Build the site in the lomayoga/builder container
      run: |
        docker run \
        -v ${{ github.workspace }}:/srv/lomayoga -v ${{ github.workspace }}/_site:/srv/jekyll/_site \
        lomayoga/builder:latest /bin/bash -c "chmod -R 777 /srv/jekyll && lomayoga build --future"
        
