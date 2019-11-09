1. 卸载之前的版本

`npm uninstall -g @angular/cli`

2. 清除缓存，确保卸载干净

`npm cache clean --force`

3. 检查是否卸载干净

`ng v`

若显示command not found则卸载干净

4. 安装指定版本

`npm install -g @angular/cli@1.6.3`

5. 检查版本号

`ng v`

6. 安装 AngularCli
`npm install -g @angular/cli`