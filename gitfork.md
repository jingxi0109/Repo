fork仓库的地址和源仓库地址是独立的，我们clone的时候拉取自己仓库的地址（源仓库：https://git.huawei.com/AlmCommon/pscloudalm.git， fork仓库：https://git.huawei.com/h30001960/pscloudalm.git）

        但是这样就会出现两个问题：

            一、源仓库新增加了分支，如何同步到自己的仓库，

            二、源仓库某个分支代码更新了，如何同步到本地仓库相应的分支

        问题一：同步新分支到fork仓库

            1、首先我们先克隆fork仓库 git clone https://git.huawei.com/h30001960/pscloudalm.git

            2、然后增加源仓库，git remote add source https://git.huawei.com/AlmCommon/pscloudalm.git (suorce为源仓库名字，后面会使用到)

                                               git fetch source（获取源仓库信息）

            3、然后拉取源仓库分支 git checkout -b branchName source/branchName（branchName为分支名字）

            4、然后上传到fork仓库 git push origin branchName

            5、完成新分支同步

        问题二：   同步分支代码

            1、首先切换到需要更新的分支 git checkout -b branchName origin/branchName

            2、拉取源仓库分支内容 git pull sourc branchName

            3、然后上传到fork仓库 git push origin branchName

            4、完成分支同步

作者：因为艾青
链接：https://www.jianshu.com/p/fad8ffc9aeff
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
