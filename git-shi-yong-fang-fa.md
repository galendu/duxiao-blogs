# git使用方法



**Git 全局设置**

```text
git config --global user.name "yundd"
git config --global user.email "yundv@outlook.com"
```

**创建一个新仓库**

```text
git clone https://XX/yundd/jenkins.git
cd jenkins
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

**推送现有文件夹**

```text
cd existing_folder
git init
git remote add origin https://XX/yundd/jenkins.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

**推送现有的 Git 仓库**

```text
cd existing_repo
git remote rename origin old-origin
git remote add origin https://XX/yundd/jenkins.git
git push -u origin --all
git push -u origin --tags
```

