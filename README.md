# 版本控制工具
## git  ：林纳斯.托瓦兹(Linux内核作者)
    作用：  1. 保存历史记录，
            2. 方便多人协作
            3. 用户多

## bash 基础命令
- pwd (print working dirstory) 显示当前路径
- ls 显示全部文件
- cd (change dirstory) 进入文件
- cd ..  进入上级目录
- mkdir (make dirstory) 创建目录
- touch 创建文件

- rm 
    a)  删除文件
    b) rm -r  (remove recusion) 删除目录
- less 分页阅读; q 退出
- mv 
    a) mv + 位置      移动文件到
    b) mv + 旧名+新名 重命名
- cp (copy) 复制 ,重命名方法与 rm 相同

- cat 查看文件全部内容
- head -数字   查看文件前"数字"行
- tail -数字   查看文件后"数字"行

- history 查看操作历史

## git 命令
-git init 初始化仓库

-git init --bare 初始化一个裸仓库

-git add 文件名  上传到本地缓存

-git commit -m '备注' 提交到本地仓库,形成历史记录

-git branch 查看本地分支

-git branch -a 查看全部分支

-git remote 远程仓库管理 add show rename rm

-git add file 跟踪文件

-git checkout -- file （已跟踪）撤销更改

-git branch 创建分支

-git checkout 切换分支

-git checkout -b 创建并切换分支

-git status 检测当前状态

-git reset 取消暂存文件

-git fetch 抓取远程数据

-git pull 抓取远程数据并合并

-git push 将本地数据推送到远程仓库

-git merge 合并分支

