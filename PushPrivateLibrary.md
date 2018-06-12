### 把工程推到私有库

##### 1.将您的Private Repo添加到您的CocoaPods安装中

```
$ pod repo add REPO_NAME git@gitlab.xxx.git
```

REPO_NAME 本地名字   git@gitlab.xxx.git 私有库git地址

##### 2.创建podspec文件

```
pod spec create  HelloWorld 
```

##### 3.编辑podspec文件

```
Pod::Spec.new do |s|
  s.name         = "HelloWorld"
  #版本号
  s.version      = "0.0.1"
  s.summary      = "A short description of HelloWorld."
  s.description  = 'A short description of HelloWorld.'
  s.homepage     = "http://EXAMPLE/HelloWorld"
  s.license      = "A short description of HelloWorld"
  #作者
  s.author             = { "" => "" }

  s.platform     = :ios, "9.0"
  #本地项目git地址
  s.source       = { :git => "git@gitlab.xxx/HelloWorld.git", :tag => "#{s.version}" }
  #公开文件路径
  s.source_files  = "HelloWorld/HelloWorld", "HelloWorld/HelloWorld/**/*.{h,m}"
  #图片路径
  s.resource  = "HelloWorld/HelloWorld.bundle"
  #系统依赖framework
  s.frameworks = 'UIKit', 'Foundation'
  # s.frameworks = "SomeFramework", "AnotherFramework"
  #项目PCH里引用的头文件
  s.prefix_header_contents = '#import <GGCategorys/UIView+NIM.h>', '#import "GGGlobal.h"', '#import "DataService.h"', '#import "UIView+Toast.h"'
   #依赖第三方库（包括自己私有库里的项目）
    s.dependency "GGCommon"
    s.dependency "GGSideingListView"
    s.dependency "BlocksKit"
    s.dependency "GGStockPortfolio"
    s.dependency "UICountingLabel"
    s.dependency "YYText"


end
```
##### 4.验证podspec文件

查看编译是否报错
```
pod spec lint [HelloWorld.podspec] --allow-warnings --sources='git@gitlab.xxx.git, https://github.com/CocoaPods/Specs.git' --verbose  
```

##### 5.将您的Podspec添加到您的仓库

~/Desktop/HelloWorld.podspec podspec文件的路径
```
pod repo push REPO_NAME ~/Desktop/HelloWorld.podspec
```
执行成功后 我们就把项目成功的添加到私有库中了
[链接：http://guides.cocoapods.org/making/private-cocoapods]http://guides.cocoapods.org/making/private-cocoapods
