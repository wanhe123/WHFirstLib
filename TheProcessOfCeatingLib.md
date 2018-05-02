
## 创建自己的库

#### 1、代码上传Github

首先我们打开github.com，然后创建自己的项目工程：

![创建项目工程](/images/create_repository.png)

这里注意那个MIT License，在后面添加Cocoapods支持的时候会用到（稍后介绍）。然后点击创建即可。
 然后用SouceTree将代码down到本地，将自己的项目放到里面，文件夹如图所示：
 
 ![load项目](/images/download.png)
 
 这里的LICENSE就是刚才说的MIT License添加的文件。WHFirstLib就是提供给他人使用的库，(在这了还可以添加示例工程)。
然后提交到Github就可以了。

#### 2、创建podspec文件
我们使用终端到工程目录下,然后执行下面的命令：
```
pod spec create WHFirstLib
```
这里的WHFirstLib就是pod添加市的名字（例如MBProgressHUD）。执行完后的结果：

![创建podspec文件](/images/create1.png)

#### 3、编辑podspec文件
此时在工程文件夹下也会多一个WHFirstLib.podspec文件。这里我用Sublime Text打开并做了如下编辑：
```
Pod::Spec.new do |s|

  s.name         = "WHFirstLib"
  s.version      = "0.0.1"
  s.summary      = "A short description of WHFirstLib."

  s.description  = <<-DESC
                   我创建的第一个库
                   DESC

  s.homepage     = "https://github.com/wanhe123/WHFirstLib"
  s.license      = "MIT"
  s.author             = { "wanhe" => "892117610@qq.com" }
  s.platform     = :ios, "8.0"
  s.source       = { :git => "https://github.com/wanhe123/WHFirstLib.git", :tag => "#{s.version}" }
  s.source_files  = "WHFirstLib/**/*.{h,m}"
  s.requires_arc = true
end
```
homtepage:Github上项目地址
license:许可证
author:作者
source:项目的https链接地址
source_files:要共享的代码，这里是WHFirstLib下面的所有代码。

#### 4、验证podspec文件

接下来执行下面的命令进行验证：
```
pod lib lint WHFirstLib.podspec
```
结果多种多样，如果有错，则按照提示进行改错即可。在这里，我执行的结果如下图：

![验证podspec文件](/images/warning1.png)

发现了多个警告，只要不是错误就行，警告可以直接忽略（红色也提示如何忽略）：
```
pod lib lint WHFirstLib.podspec --allow-warnings
```
结果如下：

![podspec文件通过验证](/images/validation.png)

当看到WHFirstLib passed validation之后，就说明验证通过了。

#### 5、在Github上创建release版本

打开项目的目录，然后创建release版本的类库：

![创建releases1](/images/create_releases1.png)

点击 箭头指向开始创建release版本，（点击 Create a new release）：

![创建releases2](/images/create_releases2.png)

点击Publish release即可。创建完成后如图所示：

![创建releases3](/images/create_releases3.png)


#### 6、注册CocoaPods账号

执行命令行：
```
pod trunk register 邮箱地址 ‘用户名’ —description='描述信息'
```
执行完之后会发送了一个验证码到邮箱，你可以打开你的邮箱验证即可。

注册成Cocoapods账号后，可以用
```
pod trunk me
```
检查是否创建成功。成功的结果如下：

![cocoapods账号注册成功](/images/registered_account.png)


#### 7、上传代码到CocoaPods

首先检测文件格式的有效性：
```
pod spec lint
```
结果如下： 

![检测文件格式的有效性1](/images/test_validity1.png)

没有错误，但是有警告。可以使用 --allow-warnings忽略：

![检测文件格式的有效性2](/images/test_validity2.png)

出现passed validation就说明通过验证了。然后执行：

```
pod trunk push WHFirstLib.podspec --allow-warnings
```
执行结果如下：（速度应该有点慢）

![上传成功](/images/upload_success.png)

#### 8、检查上传是否成功

使用
```
pod search WHFirstLib
```
结果如下：

![检查上传是否成功](/images/test_validity2.png)

这样就可以让其他人进行搜索使用了。


[原链接：](http://www.cnblogs.com/zhanggui/p/6003481.html)
