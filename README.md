如何通过git-action中使用Pnpm将前端项目通过cicd自动部署到github pages(by branch)上

下面是.github/workflows/deploy.yaml文件的内容

``` yaml
name: pnpm-build-demo
on: push

permissions:
  contents: write

jobs:
  npm-build:
    name: pnpm-build
    runs-on: ubuntu-latest
    steps:
      - name: 读取仓库的内容
        uses: actions/checkout@v4
      - name: 显示当前工作目录
        run: pwd
      - name: 配置 pnpm
        uses: pnpm/action-setup@v4
        with:
          version: 10
      - name: 安装依赖和构建项目
        uses: actions/setup-node@v4
        with:
          node-version: "22"
          cache: pnpm
      - run: |
          pnpm install
          pnpm run build
      - name: 部署
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          branch: gh-pages
          folder: dist
```
