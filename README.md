
# Deploy your static website to surge via Github Actions!
A simple Github Actions template to deploy your static site using surge.sh

**Demo** -> [https://test-github-action-surge.surge.sh/](https://test-github-action-surge.surge.sh/)

**Step 1** Get a Deployment Token
![get-surge-token](https://user-images.githubusercontent.com/6112201/66218600-d8892080-e70c-11e9-8843-c2c29b4e7e9a.gif)

**Step 2** Setup 3 secrets in your repository secrets tab

SURGE_TOKEN -> Your Surge Token
123abc123abc123abc

SURGE_DOMAIN -> The domain you want to publish your site on
https://your-surge-website-or-custom-domain.surge.sh

<img width="772" alt="Screen Shot 2019-10-06 at 10 41 48 am" src="https://user-images.githubusercontent.com/6112201/66262115-f5654700-e825-11e9-8afe-98c937ee42f9.png">

**Step 3**
Add the a new Github Action in .github/workflows folder in your repo

```
name: Deploy Website

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    name: Deploying to surge
    steps:
      - uses: actions/checkout@v1
      - name: Install surge and fire deployment
        uses: actions/setup-node@v1
        with:
          node-version: 8
      - run: npm install -g surge
      - run: surge ./ ${{ secrets.SURGE_DOMAIN }} --token ${{ secrets.SURGE_TOKEN }}

```

**Step 4**
Test it with a commit
<img width="1674" alt="Screen Shot 2019-10-05 at 1 05 34 am" src="https://user-images.githubusercontent.com/6112201/66218407-75978980-e70c-11e9-8368-1476cb69253a.png">
