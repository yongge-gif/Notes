# 初始化仓库                     git init
# 查看修改状态                   git status
# 添加到暂存区                   git add .
# 提交版本                      git commit -m "版本名"
# 查看历史                      git log
    向下翻	                    ↓ 或 Enter
    向上翻	                    ↑
    翻页	                        Space
    退出日志                    	q

# 查看改了什么                   git diff

# 切换历史版本                   git checkout 提交ID

# 回退                          git reset --hard HEAD~1

# 从公开仓库删除内容             git filter-repo --path 目录名/ --invert-paths


# 关联仓库                      git remote add origin 你的仓库地址
                                例如 git remote add origin https://github.com/yongge-gif/fastapi_project.git
# 修改仓库地址                   git remote set-url origin 仓库地址
                                例如 git remote set-url origin https://github.com/yongge-gif/Notes.git
# 首次推送                      git push -u origin main
                               或 git push -u origin master

# 强推覆盖                      git push -u origin main --force
# 删除分支                      git push origin --delete 分支名
                                例如 git push origin --delete master

# github SSH 指纹               SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU

# 删除旧git绑定                  Remove-Item -Recurse -Force .git  (windows终端执行)