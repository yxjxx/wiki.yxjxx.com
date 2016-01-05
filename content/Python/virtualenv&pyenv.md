---
title: "virtualenv and pyenv"
date: 2016-01-05 21:48
---

virtualenv 在某一目录下创建一个干净的 Python 环境。

~~~
$ [sudo] pip install virtualenv
virtualenv ENV
virtualenv --python=/usr/local/bin/python3 venv3
~~~

`tldr virtualenv`
~~~
  
  virtualenv
  Create virtual isolated Python environments

  - Create a new environment
    virtualenv path/to/venv

  - Start (select) the environment
    source path/to/venv/bin/activate

  - Stop the environment
    deactivate
~~~

***********************

pyenv 

用于安装多个版本的 Python 比如3.4，3.5。同时结合 virtualenv 更方便

~~~
brew install pyenv
pyenv install 3.4.3
brew install pyenv-virtualenv
pyenv virtualenv 3.4.3 env343
pyenv activate env343
pyenv shell env343
pyenv deactivate
~~~
