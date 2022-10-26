# Testing [mkdocs](https://www.mkdocs.org/)

```yml
name: Branch & Path

on:  
  push:
    branches:
      - "**"
    paths: 
      - '.github/workflows/BranchAndPath.yml'
      - 'README.md'
```


```yml
name: Deploy to GitHub Pages
on:
  push:	
    branches:	
      - master

jobs:
  deploy:
    name: Deploy to GitHub Pages
    runs-on: ubuntu-latest    
    steps:
    - uses: actions/checkout@master
    - name: Use Node.js
      uses: actions/setup-node@v1
      with:
        node-version: 10.x
    - name: npm install and build
      run: |
        npm install
        npm run build

    - name: Deploy
      uses: s0/git-publish-subdir-action@develop
      env:
        REPO: self
        BRANCH: gh-pages
        FOLDER: public/site
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```