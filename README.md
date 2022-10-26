# Testing [mkdocs](https://www.mkdocs.org/) for [SilverKey Technologies](https://www.silverkeytech.com/)

```yml
name: Deploy to GitHub Pages
on:
  push:
    branches:
      - master
    paths:
      - 'docs/**'
      - 'mkdocs.yml'

jobs:
  build-deploy:
    name: Build Docs and Deploy to GitHub Pages
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - uses: actions/setup-python@v4
      with:
        python-version: '3.10'
    - name: build docs
      run: |
        pip3 install mkdocs
        mkdocs build
    - name: Deploy
      uses: s0/git-publish-subdir-action@develop
      env:
        REPO: self
        BRANCH: docs
        FOLDER: site
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```