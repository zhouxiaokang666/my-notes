# Git工作流规范
统一团队Git commit日志标准，便于后续代码review，版本发布以及日志自动化生成等等。  
统一团队的Git工作流，包括分支使用、tag规范等

![flow-chart](https://github.com/zhouxiaokang666/my-notes/blob/master/img/git-specifications/flow-chart.png)

## 版本发布规范
* __基本原则__：<kbd>master</kbd>、<kbd>develop</kbd>作为长期分支存在(暂时不设置保护分支)，不直接在<kbd>master</kbd>上进行代码修改和提交，开发人员尽在<kbd>develop</kbd>和对应的功能分支上操作。<kbd>master</kbd>是生产发版分支，每次发版必须打tag标签（包括紧急版）。

* __迭代需求开发__：从<kbd>develop</kbd>分支上checkout一个feature分支进行开发。开发完成需要转测时将自己的功能分支合并回<kbd>develop</kbd>(多人合并时此处可能产生冲突，冲突在此处解决，后面环节理论上都不会产生冲突)。

* __测试阶段__：中间产生的bug问题修复，开发人员只需提交对应代码到develop，更改对应的禅道bug单状态即可，直到功能测试完毕。

* __发布阶段__：发布完成后，开发人员将<kbd>develop</kbd>分支合并到<kbd>master</kbd>分支并且打Tag。

* __紧急修复版本/临时版本__：从<kbd>master</kbd>分支上checkout一个bugfix分支进行bug修复.修复完成后直接转测此分支。测试验证通过后，发布该bugfix分支。上线成功后将bugfix分支合并到<kbd>master</kbd>。此时可删除原来的bugfix分支。

* 每次有代码合并到<kbd>master</kbd>后，均需要将<kbd>master</kbd>推送到<kbd>develop</kbd>，保证<kbd>develop</kbd>分支的代码是最新的。两个主线分支形成一个闭环。

## 分支命名规范
* __分支版本命名规则__：分支类型 分支创建时间 分支功能。比如：feature_20170401_fairy_flower
* __分支类型包括__：feature、 bugfix、refactor三种类型，即新功能开发、bug修复和代码重构
* __时间__： 使用年月日进行命名，不足2位补0
* __分支功能命名__：使用snake case命名法，即下划线命名。

## Tag命名规范
* __项目内部__： 使用日期命名，如2021-03-03。
* __公共组件库__ 使用版本号命名，包括3位版本，前缀使用v。比如v1.2.31。
* __Tag命名规范__：
    * 新功能开发使用第2位版本号，bug修复使用第3位版本号
    * 核心基础库或者Node中间件可以在大版本发布请使用灰度版本号，在
    * 版本后面加上后缀，用中划线分隔。alpha或者belta后面加上次数，即第几次alpha
    * tag名称最好加上时间，以方便查看每个版本发布时间。  
> v2.0.0-20180502-alpha.1  
> v2.0.0-20180502-beta.1
    

## Git commit日志基本规范
_type代表某次提交的类型，比如是修复一个bug还是增加一个新的
feature。_

所有的type类型如下：

* __feat__： 新增feature
* __fix__: 修复bug
* __docs__: 仅仅修改了文档，比如README, CHANGELOG, CONTRIBUTE等等
* __style__: 仅仅修改了空格、格式缩进、逗号等等，不改变代码逻辑
* __refactor__: 代码重构，没有加新功能或者修复bug
* __perf__: 优化相关，比如提升性能、体验
* __test__: 测试用例，包括单元测试、集成测试等
* __chore__: 改变构建流程、或者增加依赖库、工具等
* __revert__: 回滚到上一个版本

格式要求：
>标题行：50个字符以内，描述主要变更内容 

针对fix类型提交格式:  
>1.尽量保持一个bug修复对应一个commit  
>2.示例格式:  
>>fix：【禅道bug编号】禅道bug标题或者bug描述 // 禅道bug  
>>fix：bug描述   // 非禅道bug
