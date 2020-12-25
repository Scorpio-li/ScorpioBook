<!--
 * @Author: Li Zhiliang
 * @Date: 2020-12-24 11:15:02
 * @LastEditors: Li Zhiliang
 * @LastEditTime: 2020-12-24 11:16:36
 * @FilePath: /ScorpioBook/project/gitflow.md
-->

# Git Flow工作流程

## master主分支

伴随整个项目周期的分支

## 功能分支（feature branch）

从master切，顾名思义，开发每一个功能的分支，开发完的功能合并到release分支。

## 补丁分支（hotfix branch）

从master切，修复BUG分支，测试完直接合并到master。

## 预发分支（release branch）

从master切，需要测试的功能都合并到该分支上进行测试。
一旦开发完成，就会把release分支合并到master分支，并删除原分支。

## 开发分支（devlop branch）

## 测试分支（test branch）
