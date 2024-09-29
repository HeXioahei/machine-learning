```shell
git init
git remote add origin <https> or <ssh>
git commit -m "first commit"
git remote rm origin
git push -u origin master
git push --force origin master
git push origin master --allow-unrelated-histories
git ls-files   # 查看commit暂存区中的文件列表
git rm --cache <文件名>  # cache表示只删除暂存区的文件不删除本地文件
git rm --cache -r <目录名>  
```
