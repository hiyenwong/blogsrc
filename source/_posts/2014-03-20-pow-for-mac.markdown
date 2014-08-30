---
layout: post
title: "pow for mac"
date: 2014-03-20 16:30
comments: true
categories: [rvm,pow,rails]
---

## Pow 介绍

Pow 简单的说是一个可以实时快速将rails在mac系统中进行部署测试的插件，你只需要做几个简单设置，就可以通过特定的域名进行访问。

## Pow 安装和配置
### 安装pow
``` bash
$ curl get.pow.cx | sh
```
## 卸载pow
``` bash
$ curl get.pow.cx/uninstall.sh | sh
```

###在rvm环境下的配置
需要在每个app中设置powenv或是powrc
``` bash .powenv
# detect `$rvm_path`
if [ -z "${rvm_path:-}" ] && [ -x "${HOME:-}/.rvm/bin/rvm" ]
then rvm_path="${HOME:-}/.rvm"
fi
if [ -z "${rvm_path:-}" ] && [ -x "/usr/local/rvm/bin/rvm" ]
then rvm_path="/usr/local/rvm"
fi

# load environment of current project ruby
if
  [ -n "${rvm_path:-}" ] &&
  [ -x "${rvm_path:-}/bin/rvm" ] &&
  rvm_project_environment=`"${rvm_path:-}/bin/rvm" . do rvm env --path 2>/dev/null` &&
  [ -n "${rvm_project_environment:-}" ] &&
  [ -s "${rvm_project_environment:-}" ]
then
  echo "RVM loading: ${rvm_project_environment:-}"
  \. "${rvm_project_environment:-}"
else
  echo "RVM project not found at: $PWD"
fi
```
``` bash .powrc
if [ -f "$rvm_path/scripts/rvm" ] && [ -f ".rvmrc" ]; then
  source "$rvm_path/scripts/rvm"
  source ".rvmrc"
fi
```



