# Git

## Installation

git for windows <https://git-scm.com/download/win>  
SmartGit <https://www.syntevo.com/smartgit/>

## Register on GitHub

## Git tutorial

<https://rogerdudler.github.io/git-guide/index.de.html>

## Using

    echo "# test123" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/user/repository.git
    git push -u origin master

## Create a branch

    git checkout -b feature_x
    git push origin feature_x

make a change  

    git status
    git commit -am "change XYZ"
    git push origin feature_x

create a pull request  
add comment (single quote)  
change quote (configuure prettier .prettierrc)

    {
        "printWidth": 120,
        "singleQuote": true
    }

add file and  commit

    git add .prettierrc
    git commit -am "fix quote add prittierrc"
    git push origin feature_x

use only one commit

    git reset --soft HEAD~2
    git commit -m "change title"
    git push origin +feature_x