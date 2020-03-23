# gitlab导入git bundle文件

如何导入git bundle文件，bundle是git的一个压缩文件，用于备份

## 方法/步骤

1. 在gitlab创建好项目test
2. 进入存储\*.bundle文件的文件夹，执行下面的命令
3. ```text
   git clone *.bundle
   git remote rename origin old-origin
   git remote add origin https://XX/yundd/test.git
   git push -u origin --all
   git push -u origin --tags
   ```



