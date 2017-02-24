##版本号:Serialport@5.0.0-beta3
>[`serialport@5.0.0-beta3`
英文文档](https://github.com/EmergingTechnologyAdvisors/node-serialport/blob/5.0.0-beta3/README.md)

想象一个世界，你可以在那写javascript来控制搅拌机，灯，安全系统或者甚至是机器人。是的，我说的是机器人。那个世界就是这儿，现在使用node serialport。它提供一个非常简单的接口所需要的串口程序代码[Arduino](http://www.arduino.cc/) 单片机, [X10](http://www.smarthome.com/manuals/protocol.txt) 无线通信模块, 或者甚至是上升到 [Z-Wave](http://www.z-wave.com/modules/ZwaveStart/) 和[Zigbee](http://www.zigbee.org/) . The physical world is your oyster with this goodie. For a full break down of why we made this, please read [NodeBots - The Rise of JS Robotics](http://www.voodootikigod.com/nodebots-the-rise-of-js-robotics).在这个物理世界，你可以随心所欲。想完全了解为什么我们做这个，请阅读[NodeBots - The Rise of JS Robotics](http://www.voodootikigod.com/nodebots-the-rise-of-js-robotics).

***

为了入门node-serialport，我们建议你从下列文章开始：
* [Johnny-Five](http://johnny-five.io/#hello-world) - Johnny-Five 机器人技术和物联网平台的六行“helloworld”（太棒了）.
* [Arduino Node Security Sensor Hacking](http://nexxylove.tumblr.com/post/20159263403/arduino-node-security-sensor-hacking) -一个关于“我怎么使用这个”的文章.
* [NodeBots - The Rise of JS Robotics](http://www.voodootikigod.com/nodebots-the-rise-of-js-robotics) - 一篇调查文章关于为什么一个世界需要在js里编写机器人程序以及如何开始。

***
* [平台支持](#平台支持)
* [安装说明](#安装说明)
* [安装的平台环境](#安装平台环境)
  * [Alpine Linux](#alpine-linux)
  * [Electron](#electron)
  * [非法指令](#非法指令)
  * [Mac OS X](#mac-os-x)
  * [Raspberry Pi Linux](#raspberry-pi-linux)
  * [sudo / root](#sudo--root)
  * [Ubuntu/Debian Linux](#ubuntudebian-linux)
  * [Windows](#windows)
* [协议](#协议)
* [使用](#使用)
  * [打开一个串口](#打开一个串口)
  * [调试](#调试)
  * [错误处理](#错误处理)
* [SerialPort](#exp_module_serialport--SerialPort) ⏏
    * [`new SerialPort(path, [options], [openCallback])`](#new_module_serialport--SerialPort_new)
    * _instance_
        * [`.open([callback])`](#module_serialport--SerialPort+open)
        * [`.update([options], [callback])`](#module_serialport--SerialPort+update)
        * [`.write(data, [encoding], [callback])`](#module_serialport--SerialPort+write) ⇒ <code>boolean</code>
        * [`.read([size])`](#module_serialport--SerialPort+read) ⇒ <code>string</code> &#124; <code>Buffer</code> &#124; <code>null</code>
        * [`.close(callback)`](#module_serialport--SerialPort+close)
        * [`.set([options], [callback])`](#module_serialport--SerialPort+set)
        * [`.get([callback])`](#module_serialport--SerialPort+get)
        * [`.flush([callback])`](#module_serialport--SerialPort+flush)
        * [`.drain([callback])`](#module_serialport--SerialPort+drain)
        * [`.pause()`](#module_serialport--SerialPort+pause) ⇒
        * [`.resume()`](#module_serialport--SerialPort+resume) ⇒
        * [`Event: "error"`](#module_serialport--SerialPort+event_error)
        * [`Event: "open"`](#module_serialport--SerialPort+event_open)
        * [`Event: "data"`](#module_serialport--SerialPort+event_data)
        * [`Event: "disconnect"`](#module_serialport--SerialPort+event_disconnect)
        * [`Event: "close"`](#module_serialport--SerialPort+event_close)
    * _static_
        * [`.Binding`](#module_serialport--SerialPort.Binding) : <code>[BaseBinding](#module_serialport--SerialPort..BaseBinding)</code>
        * [`.parsers`](#module_serialport--SerialPort.parsers) : <code>object</code>
        * [`.list(callback)`](#module_serialport--SerialPort.list) : <code>function</code>
    * _inner_
        * [~BaseBinding](#module_serialport--SerialPort..BaseBinding)
            * [`new BaseBinding(options)`](#new_module_serialport--SerialPort..BaseBinding_new)
            * _instance_
                * [`.open(path, openOptions)`](#module_serialport--SerialPort..BaseBinding+open) ⇒ <code>Promise</code>
                * [`.close()`](#module_serialport--SerialPort..BaseBinding+close) ⇒ <code>Promise</code>
                * [`.read(data, length)`](#module_serialport--SerialPort..BaseBinding+read) ⇒ <code>Promise</code>
                * [`.write(data)`](#module_serialport--SerialPort..BaseBinding+write) ⇒ <code>Promise</code>
                * [`.update([options])`](#module_serialport--SerialPort..BaseBinding+update) ⇒ <code>Promise</code>
                * [`.set([options])`](#module_serialport--SerialPort..BaseBinding+set) ⇒ <code>Promise</code>
                * [`.get()`](#module_serialport--SerialPort..BaseBinding+get) ⇒ <code>Promise</code>
                * [`.flush()`](#module_serialport--SerialPort..BaseBinding+flush) ⇒ <code>Promise</code>
                * [`.drain()`](#module_serialport--SerialPort..BaseBinding+drain) ⇒ <code>Promise</code>
            * _static_
                * [`.list()`](#module_serialport--SerialPort..BaseBinding.list) ⇒ <code>Promise</code>
        * [`~errorCallback`](#module_serialport--SerialPort..errorCallback) : <code>function</code>
        * [`~modemBitsCallback`](#module_serialport--SerialPort..modemBitsCallback) : <code>function</code>
        * [`~openOptions`](#module_serialport--SerialPort..openOptions) : <code>Object</code>
        * [`~listCallback`](#module_serialport--SerialPort..listCallback) : <code>function</code>
* [命令行工具](#命令行工具)
  * [串口列表](#串口列表)
  * [串口终端](#串口终端)

***

##平台支持
`serialport`支持NodeJS v4 以及更高版本。0.10和0.12版本使用`serialport@4`。`serialport`支持的平台，体系架构和nodejs版本可以查看下列表格信息。
| 平台/架构 | Node v4.x | Node v6.x | Node v7.x |
|       ---       | --- | --- | --- |
| Linux / ia32    |  ☑  |  ☑  |  ☑  |
| Linux / x64     |  ☑  |  ☑  |  ☑  |
| Linux / ARM v6¹ |  ☐  |  ☐  |  ☐  |
| Linux / ARM v7¹ |  ☐  |  ☐  |  ☐  |
| Linux / ARM v8¹ |  ☐  |  ☐  |  ☐  |
| Linux / MIPSel¹ |  ☐  |  ☐  |  ☐  |
| Linux / PPC64¹  |  ☐  |  ☐  |  ☐  |
| Windows² / x86  |  ☑  |  ☑  |  ☑  |
| Windows² / x64  |  ☑  |  ☑  |  ☑  |
| OSX³ / x64      |  ☑  |  ☑  |  ☑  |

¹ ARM, MIPSel and PPC64¹ 平台已知可以运行但是不属于我们的测试范围或者构建矩阵。 [#846](https://github.com/EmergingTechnologyAdvisors/node-serialport/issues/846) ARM v4 and v5 在 Node v0.10版本之后从Nodejs中取消.

² Windows 7, 8, 10, and 10 IoT 是支持的但是只有Windows Server 2012 R2 是由我们测试的.

³ OSX 10.4 Tiger 以及更高版本是支持的 但是只有 10.9.5 Mavericks 和 Xcode 6.1 是由我们测试的.

##安装说明
对于大多数“标准”使用案例（在mac，linux，windows x86或者x64上node V4.x），node-serialport将会很好以及很容易的安装。

```
npm install serialport 
```

###安装的平台环境
我们使用[node-pre-gyp](https://github.com/mapbox/node-pre-gyp)来编译以及公布大多数常见使用平台（linux，mac，windows在标准的处理器平台）的二进制库。如果你是特别的平台，node-serialport将会工作，但是当你安装的时候它将会编译二进制文件。

这假定你有必要让你可以在自己系统中编译一些nodejs模块。这个或许并非如此，可是，请确认下列对于你系统是正确的，在你提出关于“无法安装”的issue之前。对于所有操作系统，请确认你有安装了Python 2.x 以及不是3.0，node-gyp（你用来编译的工具）需要Python 2.x。

####Alpine Linux

[Alpine](http://www.alpinelinux.org/) 是一个（非常）小的linux开发版系统, 但是它使用组织标准库来代替函数库 (大多数开发版linux系统使用的), 所以他需要编译。 它通常使用Docker.我们已经编译了可以工作的 [apline-node](https://github.com/mhart/alpine-node).

```
# 如果你没有安装node/npn，先添加它们
sudo apk add --no-cache nodejs

# 添加必要的构建库和运行依赖
sudo apk add --no-cache make gcc g++ python linux-headers udev

# 然后我们就能安装 serialport, 强制它编译
npm install serialport --build-from-source

# 如果你使用root来安装，你需要使用
```

####Electron
Electron是一个框架用来创建跨平台桌面程序。Electron自带他自己的Node.js运行版本

如果你需要`serialport`作为一个Electron项目的依赖，你需要为你用在项目里的Electron项目编译它。

当你第一次安装`serialport`,它会编译针对你机器的Node.js版本的serialport，而不是针对Electron捆绑的Node.js运行版本。

再次为Electron编译`serialport`(或者一个本地模块)，你可以使用`electron-rebuild`.

1.`npm install --save-dev electron-rebuild`
2.将`electron-rebuild`加入到你项目中的package.json的安装钩子。
3.运行`npm install`

更多关于`electron-rebuild`的信息访问[README](https://github.com/electron/electron-rebuild/blob/master/README.md).

查看实例项目可查看[`electron-serialport`](https://github.com/johnny-five-io/electron-serialport).

####非法指令
假定一个完全有能力的芯片预编译的二进制文件。例如Galileo2缺乏一些`ia32`指令集架构。一些其他平台有相似的问题。所以当你试图运行serialport时，如果你得到`非法指令`，你将需要重新构建serialport二进制文件通过告知npm去重新构建它。

```命令
#告知npm构建serialport在安装的时间内
npm install serialport --build-form-source

#如果你有一个依赖serialport的包，你可以告知npm去特别重新构建它。
npm rebuild serialport --build-form-source

#或者除去包名，重新构建所有
npm rebuild --build-form-source
```

####Mac OS X
确定你有是在最低的xCode命令行工具里安装适用你系统的配置。如果你最近更新了系统，可能会移除你安装的命令行工具，请在提交问题前仔细查证。你需要使用g++ v4.8或者更高版本来编译Node.js 4.x+的`node-serialport`。

####Raspberry Pi Linux
下列是关于[使用Johnny-Five和Raspi IO设置树莓派](https://github.com/nebrius/raspi-io/wiki/Getting-a-Raspberry-Pi-ready-for-NodeBots)的说明。这些项目使用Node Serialport。

| Revision       |      CPU              | Arm Version |
|   ----         |      ---              |     ---     |
| A, A+, B, B+   | 32-bit ARM1176JZF-S   |    ARMv6    |
| Compute Module | 32-bit ARM1176JZF-S   |    ARMv6    |
| Zero           | 32-bit ARM1176JZF-S   |    ARMv6    |
| B2             | 32-bit ARM Cortex-A7  |    ARMv7    |
| B3             | 32-bit ARM Cortex-A53 |    ARMv8    |

#### sudo / root
如果你准备使用`sudo`或者root权限去安装node Serialport，`npm`需要你使用不安全的参数标志。这个需求一般很少需要。

```命令
sudo npm install serialport --unsafe-perm --build-form-source
```

使用标志失败导致类似的错误如下；
```命令
root@rpi3:~# npm install -g serialport
/usr/bin/serialport-list -> /usr/lib/node_modules/serialport/bin/serialport-list.js
/usr/bin/serialport-term -> /usr/lib/node_modules/serialport/bin/serialport-terminal.js

> serialport@4.0.3 install /usr/lib/node_modules/serialport
> node-pre-gyp install --fallback-to-build

gyp WARN EACCES user "root" does not have permission to access the dev dir "/root/.node-gyp/6.9.1"
gyp WARN EACCES attempting to reinstall using temporary dev dir "/usr/lib/node_modules/serialport/.node-gyp"
make: Entering directory '/usr/lib/node_modules/serialport/build'
make: *** No rule to make target '../.node-gyp/6.9.1/include/node/common.gypi', needed by 'Makefile'.  Stop.
make: Leaving directory '/usr/lib/node_modules/serialport/build'
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
```
####Ubuntu/Debian Linux
最好的方式来安装任何版本的NodeJS是使用[NodeSource Node.js Binary Distributions](https://github.com/nodesource/distributions#installation-instructions).旧版本的Ubuntu安装错误的nodejs版本和二进制名称。如果你node二进制文件是`nodejs`不是`node`或者如果你的nodejs版本是[`v0.10.29`](https://github.com/fivdi/onoff/wiki/Node.js-v0.10.29-and-native-addons-on-the-Raspberry-Pi) ，那么你应该根据以下这个说明来操作。

`build-essential`包是编译`serialport`必要的包。如果那儿有一个你不需要的你平台的二进制文件，请继续！

```
#Using Ubuntu and node 6
curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
sudo apt-get install -y nodejs

#Using Debian and node 6,使用root权限
curl -sL https://deb.nodesource.com/setup_7.x | bash - 
apt-get install -y nodejs
```

####Windows
Windows 7,Windows 8.1,Windows 10和Windows 10 IoT是支持的。预编译二进制文件是可用的，但是如果你想要从源码构建它的话，你需要查看[node-gyp 的安装](https://github.com/nodejs/node-gyp#installation)的说明。一旦这些都完成了并且可以工作了你将能从源码来安装serialport。

```powershell
npm install serialport --build-from-source
```

这不是node-gyp说明的一部分，但是有些时候它会帮助你，如果你在visual studio创建了一个c++项目，它将会安装那些在两个小时安装visual studio过程中不能安装的必要的组件，而你只能坐在那儿。这个将解决一些`Failed to locate:"CL.exe"`的实例。

##协议
SerialPort 使用的是MIT协议以及它所有的依赖关系都是遵循MIT或者BSD协议。

##使用
打开一个串口：
```js代码
var SerialPort = require('serialport');
var port = new SerialPort('/dev/tty-usbserial1',{
    baudRate: 57600
});
```

当打开一个串口，你可以指定（按这个顺序）
1.串口的路径 - 需要
2.选项 - 可选的，下面会描述

###打开一个串口

构造一个`SerialPort`项目将会立即打开一个串口。当你可以在任何时候能读出和写入（它会在打开的串口中排列），大多数串口函数要求一个开启的串口。当串口是打开的时候，你可以使用以下三个方式调用代码。

 - `open`事件经常会触发当串口打开的时候。 当`autoOpen`选项没有失效的时候，构造函数的 openCallback
 - 被传递给`.open()`。如果你已经将它关闭，callback回调会被忽视。
 - `.open()`函数需要一个在串口打开后的回调。如果你关闭了`autoOpen`选项或者已经关闭了串口，这个就可以被使用。

```js代码
var SerialPort = require('serialport');
var port = new SerialPort('/dev/tty-usbserial1');

port.on('open',function(){
    port.write('main screen turn on ',function(err){
        if(err){
            return console.log('Error on write: ' ,err.message);
        }
        console.log('message written');
    });
});

//打开错误将会发出一个错误事件
port.on('error',function(err){
    console.log('Error: ',err.message);
});
```

这个可以被移动到构造函数的回调
```js代码
var SerialPort = require('serialport');
var port = new SerialPort('/dev/tty-usbserial1',function(err){
    if(err){
        return console.log('Error:',err.message);
    }
    port.write('main screen turn on',function(err){
        if(err){
            return console.log('Error on write: ',err.message);
        }
        console.log('message written');
    });
});
```

当关闭`autoOpen`选项，你将要自己打开串口。
```js代码
var SerialPort = require('serialport');
var port = new SerialPort('/dev/tty-usbserial1',{autoOpen:false});

port.open(function(err){
    if(err){
        return console.log('Error opening port: ',err.message);
    }
    
    //写入失败将会被串口发出由于没有写回调。
    port.write('main screen turn on');
});

//开启事件总是会被发出
port.on('open',function(){
    //打开的逻辑
});
```

你可以从下列串口更新新的数据
```js代码
port.on('data',function(data){
    console.log('Data: '+data);
});
```

你可以通过发送一个字符串或者缓冲给写入方法来向串口写入数据。像下列一样：
```js代码
port.write('Hi Mon!');
port.write(new Buffer('Hi Mom!'));
```

享受以及使用这些代码做一些酷的事情吧！

###调试

我们使用[debug](https://www.npmjs.com/package/debug) 包以及记录下`serialport`的命名空间。我们的日志；

 - `serialport:main`对于所有高等级的主要日志
 - `serialport:binding` 对于所有低级的日志

你可以通过环境变量来应用日志。检查[debug](https://www.npmjs.com/package/debug)文档给更多的信息。

```bash
DEBUG=serialport:main node myapp.js
DEBUG=serialport:* node myapp.js
DEBUG=* node myapp.js
```

###错误处理
所有函数在SerialPort的两个约定。

 - 参数错误抛出一个`TypeError`对象。当这些函数被叫做无效参数时，你将会看见这些。
 - 如果没有回调被提供，运行时错误提供`Error`对象给函数回调或者发出一个[`error event`](#module_serialport--SerialPort+event_error)。你将会看到这些当一个运行错误发生，比如试图开启一个错误的串口，或者设置一个不支持的波特率。
 
如果你调用正确参数的函数，它应该不需要在一个try/catch结构中包括一个SerialPort对象

<a name="exp_module_serialport--SerialPort"></a>


### SerialPort ⏏

**Kind**: 输出类
**Kind**: Exported class  
**Emits**: <code>[open](#module_serialport--SerialPort+event_open)</code>, <code>[data](#module_serialport--SerialPort+event_data)</code>, <code>[close](#module_serialport--SerialPort+event_close)</code>, <code>[error](#module_serialport--SerialPort+event_error)</code>, <code>[disconnect](#module_serialport--SerialPort+event_disconnect)</code>  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| baudRate | <code>number</code> | 串口的波特率，使用`.update`来改变它。只读 |
| binding | <code>object</code> | 支持串口的绑定对象，只读. |
| isOpen | <code>boolean</code> | 如果串口打开时为`true` ，其他情况是 `false`.只读. (`since 5.0.0`) |
| path | <code>string</code> | 串口的系统路径或者名称. 只读. |

-

<a name="new_module_serialport--SerialPort_new"></a>


####`new SerialPort(path,[options],[openCallback])`
为`path`创建一个新的串口对象.用无效的参数或者无效的选项构造一个新的串口时，会抛出错误。串口将默认自动打开，其次这相当于调用`port.open(openCallback)`。这个可以被关闭，通过设置`autoOpen`选项为false。

**Throws**:
 - <code>TypeError</code> 当提供无效参数时， 将会抛出TypeError。

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| path | <code>string</code> | 串口打开的系统路径.例如, 在Mac/Linux上`/dev/tty.XXX`  或者 Windows上的 `COM1` . |
| [options] | <code>[openOptions](#module_serialport--SerialPort..openOptions)</code> | 串口配置选项 |
| [openCallback] | <code>[errorCallback](#module_serialport--SerialPort..errorCallback)</code> | 当连接已经打开. 如果它没有提供以及由错误发生，它将会发出串口`error`事件。如果在openOptions中autoOpen被设置为false，回调将不会调用 |

-

<a name="module_serialport--SerialPort+open"></a>

####`serialPort.open([callback])`
打开一个连接到串口

**Kind**：实例方法 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  
**Emits**:<code>[open](#module_serialport--SerialPort+event_open)</code> 

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| [callback] | <code>[errorCallback](#module_serialport--SerialPort..errorCallback)</code> | 当连接已经被打开. 如果它没有被提供以及有一个错误发生, 它将在串口上被发出`error`事件``. |

-

<a name="module_serialport--SerialPort+update"></a>

#### `serialPort.update([options],[callback])`
改变打开的串口的波特率。抛出异常如果你提供了一个错误的参数。当波特率不支持事，会抛出错误或者产生回调。
**Kind**: instance method of <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| [options] | <code>object</code> | 目前只有波特率是支持的 |
| [options.baudRate] | <code>number</code> | 设置波特率的串口是打开的。这应该匹配常见的波特率之一, 比如 110, 300, 1200, 2400, 4800, 9600, 14400, 19200, 38400, 57600, 115200. 当然不能担保, 串口连接的设备将支持请求的波特率,只要串口自己支持那个波特率. |
| [callback] | <code>[errorCallback](#module_serialport--SerialPort..errorCallback)</code> | 当波特率被改变的时候. 如果 `.update` 被调用而没有回调以及有一个错误,错误事件将会被触发。 |

-

<a name="module_serialport--SerialPort+write"></a>

#### `serialPort.write(data,[encoding],[callback])`⇒ <code>boolean</code>
向给定的串口写入数据。如果端口没有打开，会缓存写入数据。

写入操作是无阻塞的。当它返回时，数据或许还没有被写入串口。看`drain()`

一些设备，比如当你打开一个连接到Arduino时，它会重启。在这种情况下，如果你立刻向设备写入，它们将不能接收到数据。这经常在Arduino发送“ready”字节后工作，你的node程序会在写入前等待。你也可以侥幸认为等待大概400ms.

尽管串口是一个流，但当写入它可以接受的字节数组除了字符串和缓存时，这个格外的功能非常有用。

**Kind**: 实例方法 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  
**Returns**: <code>boolean</code> -  如果流渴望在继续写入其他数据之前调用代码等待被触发的`drain`事件，就是`false`; 其他情况是 `true`.  
**Since**: 5.0.0  

| 参数 |类型 | 描述 |
| --- | --- | --- |
| data | <code>string</code> &#124; <code>array</code> &#124; <code>buffer</code> | 接收一个 [`Buffer` ](http://nodejs.org/api/buffer.html) 对象, 或者一个接受`buffer`构造函数的类型 (除了字节数组或者一个字符串). |
| [encoding] | <code>string</code> | 编码, 如果数据块是一个字符串. 默认的是 `'utf8'`. 也接受 `'ascii'`, `'base64'`, `'binary'`, `'hex'` 查看 [Buffers and Character Encodings](https://nodejs.org/api/buffer.html#buffer_buffers_and_character_encodings)了解所有可用的选项. |
| [callback] | <code>function</code> |第一次写入操作结束.数据可能还没有刷新到底层端口,没有参数. |

-

<a name="module_serialport--SerialPort+read"></a>

#### `serialPort.read([size])` ⇒ <code>string</code> &#124; <code>Buffer</code> &#124; <code>null</code>
从串口请求一个字节数.`read()`方法从内存缓冲区拉取一些数据然后返回它。如果没有可用数据被读取，会返回null。默认的，数据将会被返回成一个缓存对象，除非一个编码已经指明使用了`.setEncoding()`方法。

**Kind**: 实例方法 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  
**Returns**: <code>string</code> &#124; <code>Buffer</code> &#124; <code>null</code> - 内存缓冲区数据
**Since**: 5.0.0  

| 参数 |类型 |描述 |
| --- | --- | --- |
| [size] | <code>number</code> |指明了会返回多少字节的数据如果是可用的话。|

-

<a name="module_serialport--SerialPort+close"></a>

#### `serialPort.close(callback)` 
关闭开启的连接

**Kind**: 实例方法 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  
**Emits**: <code>[close](#module_serialport--SerialPort+event_close)</code>  

| 参数 |类型 |描述 |
| --- | --- | --- |
| callback | <code>errorCallback</code> | 当连接被关闭. |


-

<a name="module_serialport--SerialPort+set"></a>


#### `serialPort.set([options], [callback])`
在打开的串口上设置控制标志. Uses [`SetCommMask`](https://msdn.microsoft.com/en-us/library/windows/desktop/aa363257(v=vs.85).aspx) for windows and [`ioctl`](http://linux.die.net/man/4/tty_ioctl) for mac and linux.

**Kind**:实例方法 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  
**Since**: 5.0.0  

| 参数 | 类型 | 默认值 | 描述 |
| --- | --- | --- | --- |
| [options] | <code>object</code> |  | 所有选项是操作系统默认的当串口被打开. 每个标志被设置为相同的调用提供或者是默认数据.如果选项没有提供将要使用的默认选项. |
| [options.brk] | <code>Boolean</code> | <code>false</code> |  |
| [options.cts] | <code>Boolean</code> | <code>false</code> |  |
| [options.dsr] | <code>Boolean</code> | <code>false</code> |  |
| [options.dtr] | <code>Boolean</code> | <code>true</code> |  |
| [options.rts] | <code>Boolean</code> | <code>true</code> |  |
| [callback] | <code>[errorCallback](#module_serialport--SerialPort..errorCallback)</code> |  | 当串口标志被设置. |


-

<a name="module_serialport--SerialPort+get"></a>


#### `serialPort.get([callback])`
返回控制标志 (CTS, DSR, DCD)在开启的串口上.
使用[`GetCommModemStatus`](https://msdn.microsoft.com/en-us/library/windows/desktop/aa363258(v=vs.85).aspx) for windows and [`ioctl`](http://linux.die.net/man/4/tty_ioctl) for mac and linux.

**Kind**: 实例方法 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| [callback] | <code>[modemBitsCallback](#module_serialport--SerialPort..modemBitsCallback)</code> | Called once the modem bits have been retrieved（当比特被恢复） |


-

<a name="module_serialport--SerialPort+flush"></a>


#### `serialPort.flush([callback])`
刷新收到的丢弃的数据，但是不读出和写入，也不传输。. 更多的详细技术请看 [`tcflush(fd, TCIFLUSH)`](http://linux.die.net/man/3/tcflush) for Mac/Linux and [`FlushFileBuffers`](http://msdn.microsoft.com/en-us/library/windows/desktop/aa364439) for Windows.

**Kind**: 实例方法 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| [callback] | <code>[errorCallback](#module_serialport--SerialPort..errorCallback)</code> | 当刷新操作完成. |


-

<a name="module_serialport--SerialPort+drain"></a>

#### `serialPort.drain([callback])`
等待直到所有发出的数据被传输到串口。 查看 [`tcdrain()`](http://linux.die.net/man/3/tcdrain) or [FlushFileBuffers()](https://msdn.microsoft.com/en-us/library/windows/desktop/aa364439(v=vs.85).aspx) 了解更多信息。

**Kind**: 实例方法 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

| 参数 |类型 |描述 |
| --- | --- | --- |
| [callback] | <code>[errorCallback](#module_serialport--SerialPort..errorCallback)</code> |当耗尽操作返回 |

**Example**  
写入 `data` 以及等待直到在调用回调之前，结束对目标串口的传输。

```js
function writeAndDrain (data, callback) {
  sp.write(data, function () {
    sp.drain(callback);
  });
}
```

-

<a name="module_serialport--SerialPort+pause"></a>

#### `serialPort.pause()` ⇒
 `pause()`方法会导致一个流的流动模式停止触发'data'事件，切换的流动模式. 任何可用的数据将仍然存放在内存缓存区。

**Kind**: 实例方法<code>[SerialPort](#exp_module_serialport--SerialPort)</code>  
**Returns**: `this`  
**See**: module:serialport#resume  
**Since**: 5.0.0  

-

<a name="module_serialport--SerialPort+resume"></a>

#### `serialPort.resume()` ⇒
 `resume()`会导致一个明确的暂停可读的流，来恢复触发的‘data'事件，切换流到流模式

**Kind**: 实例方法 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  
**Returns**: `this`  
**See**: module:serialport#pause  
**Since**: 5.0.0  

-

<a name="module_serialport--SerialPort+event_error"></a>

#### `Event: "error"`
 无论何时这有一个错误就会回调`error` 事件。

**Kind**: 事件由此触发 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

-

<a name="module_serialport--SerialPort+event_open"></a>

#### `Event: "open"`
当串口打开以及准备进行写入时，`open` 事件将会无参回调。 如果碰巧如果你有构造函数立即打开或者如果你通过`open()`手动打开串口。查看 [Useage/Opening a Port](#opening-a-port) 了解更多信息.

**Kind**: 事件由此触发 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

-

<a name="module_serialport--SerialPort+event_data"></a>

#### `Event: "data"`
`data` 事件输出字符串到串口在流动模式中. 一旦被接受到，数据就会被发出。 数据将会是一个缓存对象，很多不同的数据量在其中.`readLine`解析器将数据转换成字符串.查看 [parsers](#module_serialport--SerialPort.parsers)部分了解关于解析器的更多信息以及 [NodeJS stream documentation](https://nodejs.org/api/stream.html#stream_event_data) 了解更多关于数据事件的信息.

**Kind**: 事件由此触发 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

-

<a name="module_serialport--SerialPort+event_disconnect"></a>

#### `Event: "disconnect"`
`disconnect` 事件回调会调用一个错误对象. 这个经常发生在 `close` 事件之前如果断开连接被发现。

**Kind**: 事件由此触发<code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

-

<a name="module_serialport--SerialPort+event_close"></a>

#### `Event: "close"`
 `close`事件是无参回调当串口被关闭时. 当一个错误发生，错误事件将被触发。

**Kind**: 事件由此触发 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

-

<a name="module_serialport--SerialPort.Binding"></a>

#### `SerialPort.Binding` : <code>[BaseBinding](#module_serialport--SerialPort..BaseBinding)</code>
Binding是node Serialport底层的系统. 默认的我们自动检测 windows, Linux 和 OSX系统 以及为你系统加载合适的模块. 你可以指定 `SerialPort.Binding` 去绑定任何你喜欢的后台. 你可以搜索更多信息从 [npm](https://npmjs.org/).
  你也可以禁止自动后台加载，通过一下代码实现
  ```js代码
  var SerialPort = require('serialport/lib/serialport');
  SerialPort.Binding = MyBindingClass;
  ```

**Kind**: 静态性能<code>[SerialPort](#exp_module_serialport--SerialPort)</code>  
**Since**: 5.0.0  

-

<a name="module_serialport--SerialPort.parsers"></a>

#### `SerialPort.parsers` : <code>object</code>
默认的分析程序是[Transform streams](https://nodejs.org/api/stream.html#stream_class_stream_transform) 可以用各种各样的方式来解析数据，可以被使用来处理传入的数据。

 使用各种解析程序你都需要创建他们然后输送SerialPort到解析程序。千万别编写解析程序，而是编写SerialPort对象。

**Kind**: 静态特性<code>[SerialPort](#exp_module_serialport--SerialPort)</code>  
**Since**: 5.0.0  
**Properties**

| 名称 | 状态 | 描述 |
| --- | --- | --- |
| ByteLength | <code>Class</code> |  发出数据的转换流作为缓存，在收到一个特定的字节数后|
| Delimiter | <code>Class</code> |  发出数据的转换流，每次接受一个字节序列|
| Readline | <code>Class</code> | 发出数据的转换流，在收到一个换行符之后 |

**例子**  
```js
var SerialPort = require('serialport');
var Readline = SerialPort.parsers.Readline;
var port = new SerialPort('/dev/tty-usbserial1');
var parser = new Readline();
port.pipe(parser);
parser.on('data', console.log);
port.write('ROBOT PLEASE RESPOND\n');

// 可以缩短创建的解析程序和传输管道
var parser = port.pipe(new Readline());
```

使用字节长度解析器，你必须提供字节数的长度:
```js
var SerialPort = require('serialport');
var ByteLength = SerialPort.parsers.ByteLength
var port = new SerialPort('/dev/tty-usbserial1');
var parser = port.pipe(new ByteLength({length: 8}));
parser.on('data', console.log);
```

使用分隔符解析器你必须指明分隔符，你必须在一个字符串、缓存或者一个字节数组中提供一个分隔符:
```js
var SerialPort = require('serialport');
var Delimiter = SerialPort.parsers.Delimiter;
var port = new SerialPort('/dev/tty-usbserial1');
var parser = port.pipe(new Delimiter({delimiter: new Buffer('EOL')}));
parser.on('data', console.log);
```

使用换行符解析器,你必须提供一个分隔符 (默认是 '\n')
```js
var SerialPort = require('serialport');
var Readline = SerialPort.parsers.Readline;
var port = new SerialPort('/dev/tty-usbserial1');
var parser = port.pipe(Readline({delimiter: '\r\n'}));
parser.on('data', console.log);
```

-

<a name="module_serialport--SerialPort.list"></a>

#### `SerialPort.list(callback)` : <code>function</code>
从元数据中找回可用的串口列表. 只有“串口名”是可用的，所有其他的字段如果它们不可用，将会无意义。 `串口名` 也是一个路径或者一个标识符(例如 `COM1`)用来打开串口.

**Kind**: 静态方法 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

| 参数 | 类型 |
| --- | --- |
| callback | <code>listCallback</code> | 

**例子**  
```js
// 示例的串口信息
{
  comName: '/dev/cu.usbmodem1421',
  manufacturer: 'Arduino (www.arduino.cc)',
  serialNumber: '757533138333964011C1',
  pnpId: undefined,
  locationId: '0x14200000',
  vendorId: '0x2341',
  productId: '0x0043'
}

```

```js
var SerialPort = require('serialport');
SerialPort.list(function (err, ports) {
  ports.forEach(function(port) {
    console.log(port.comName);
    console.log(port.pnpId);
    console.log(port.manufacturer);
  });
});
```

-

<a name="module_serialport--SerialPort..BaseBinding"></a>

#### SerialPort~BaseBinding
你永远不能直接使用Binding对象，因为它们通过SerialPort来接触底层硬件. 这个文档是针对绑定不同平台的用户.这个类能被继承来为每个方法进行类型检查.

**Kind**: 内部类 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  
**Since**: 5.0.0  
**Properties**

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| isOpen | <code>boolean</code> | 必须的属性. 串口打开就是`true`  , 其他的是`false`.只读. |


* [~BaseBinding](#module_serialport--SerialPort..BaseBinding)
    * [`new BaseBinding(options)`](#new_module_serialport--SerialPort..BaseBinding_new)
    * _instance_
        * [`.open(path, openOptions)`](#module_serialport--SerialPort..BaseBinding+open) ⇒ <code>Promise</code>
        * [`.close()`](#module_serialport--SerialPort..BaseBinding+close) ⇒ <code>Promise</code>
        * [`.read(data, length)`](#module_serialport--SerialPort..BaseBinding+read) ⇒ <code>Promise</code>
        * [`.write(data)`](#module_serialport--SerialPort..BaseBinding+write) ⇒ <code>Promise</code>
        * [`.update([options])`](#module_serialport--SerialPort..BaseBinding+update) ⇒ <code>Promise</code>
        * [`.set([options])`](#module_serialport--SerialPort..BaseBinding+set) ⇒ <code>Promise</code>
        * [`.get()`](#module_serialport--SerialPort..BaseBinding+get) ⇒ <code>Promise</code>
        * [`.flush()`](#module_serialport--SerialPort..BaseBinding+flush) ⇒ <code>Promise</code>
        * [`.drain()`](#module_serialport--SerialPort..BaseBinding+drain) ⇒ <code>Promise</code>
    * _static_
        * [`.list()`](#module_serialport--SerialPort..BaseBinding.list) ⇒ <code>Promise</code>


-

<a name="new_module_serialport--SerialPort..BaseBinding_new"></a>

##### `new BaseBinding(options)`
**Throws**:

- <code>TypeError</code> 当给定一个无效的参数，将会抛出TypeError错误.


| 参数 | 类型 | 描述 |
| --- | --- | --- |
| options | <code>object</code> |  |
| options.disconnect | <code>function</code> | 当binding被检测到一个没连接的串口，方法将会被调用. 这个方法应该在所有操作期间调用，而不是在操作正常回调后调用。`SerialPort` 将试图调用 `close`在断开连接后，以及会忽视所有错误. |


-

<a name="module_serialport--SerialPort..BaseBinding+open"></a>

##### `baseBinding.open(path, openOptions)` ⇒ <code>Promise</code>
通过路径打开一个引用的串口连接

**Kind**: 实例方法<code>[BaseBinding](#module_serialport--SerialPort..BaseBinding)</code>  
**Returns**: <code>Promise</code> - 在串口打开和配置好后返回解决.  
**Throws**:

- <code>TypeError</code> 当给定一个无效的参数，将会抛出TypeError错误.


| 参数 | 类型 |
| --- | --- |
| path | <code>string</code> | 
| openOptions | <code>[openOptions](#module_serialport--SerialPort..openOptions)</code> | 


-

<a name="module_serialport--SerialPort..BaseBinding+close"></a>

##### `baseBinding.close()` ⇒ <code>Promise</code>
关闭一个串口连接

**Kind**: 实例方法 <code>[BaseBinding](#module_serialport--SerialPort..BaseBinding)</code>  
**Returns**: <code>Promise</code> - 一旦串口被关闭返回解决.  
**Throws**:

- <code>TypeError</code> 当给定一个无效的参数，将会抛出TypeError错误.


-

<a name="module_serialport--SerialPort..BaseBinding+read"></a>

##### `baseBinding.read(data, length)` ⇒ <code>Promise</code>
从SerialPort请求一个字节数。这个方法和node的 [`fs.read`](http://nodejs.org/api/fs.html#fs_fs_read_fd_buffer_offset_length_position_callback)相似.

**Kind**: 实例方法 <code>[BaseBinding](#module_serialport--SerialPort..BaseBinding)</code>  
**Returns**: <code>Promise</code> -在阅读操作结束之后返回读取的字节数.  
**Throws**:

- <code>TypeError</code>当给定一个无效的参数，将会抛出TypeError错误.

**Params**: <code>integer</code> 偏移 - 在缓存区偏移处开始写入.  

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| data | <code>buffer</code> | 接受 [`Buffer`](http://nodejs.org/api/buffer.html) 对象 |
| length | <code>integer</code> | 读取指定的最大字节数 |


-

<a name="module_serialport--SerialPort..BaseBinding+write"></a>

##### `baseBinding.write(data)` ⇒ <code>Promise</code>
向SerialPort写入一个字节数，这将只能在没有等待写入的操作时被调用.

**Kind**: 实例方法 <code>[BaseBinding](#module_serialport--SerialPort..BaseBinding)</code>  
**Returns**: <code>Promise</code> - 在数据传递给操作系统编写后返回.  
**Throws**:

- <code>TypeError</code> 当给定一个无效的参数，将会抛出TypeError错误.


| 参数 | 类型 | 描述 |
| --- | --- | --- |
| data | <code>buffer</code> | 接受 [`Buffer`](http://nodejs.org/api/buffer.html) 对象. |


-

<a name="module_serialport--SerialPort..BaseBinding+update"></a>

##### `baseBinding.update([options])` ⇒ <code>Promise</code>
改变开启的串口的连接设置。当前只能设置波特率。

**Kind**: 实例方法 <code>[BaseBinding](#module_serialport--SerialPort..BaseBinding)</code>  
**Returns**: <code>Promise</code> - 当串口波特率被改变后返回.  
**Throws**:

- <code>TypeError</code> 当给定一个无效的参数，将会抛出TypeError错误.


| 参数 | 类型 | 描述 |
| --- | --- | --- |
| [options] | <code>object</code> | 目前只有`波特率`支持 |
| [options.baudRate] | <code>number</code> | 如果通过bingdings提供一个不支持的波特率，它将回调一个错误。 |


-

<a name="module_serialport--SerialPort..BaseBinding+set"></a>

##### `baseBinding.set([options])` ⇒ <code>Promise</code>
设置一个打开的串口的控制标志。

**Kind**: 实例方法<code>[BaseBinding](#module_serialport--SerialPort..BaseBinding)</code>  
**Returns**: <code>Promise</code> - 在串口的标识被设置后返回.  
**Throws**:

- <code>TypeError</code> 当给定一个无效的参数，将会抛出TypeError错误.


| 参数 | 类型 | 默认 | 描述 |
| --- | --- | --- | --- |
| [options] | <code>object</code> |  | 当串口被打开时，所有设置都是操作系统的默认设置. 每个标识都被设置成每次调用时提供的或者默认的数值。所有设置通常都是被提供的. |
| [options.brk] | <code>Boolean</code> | <code>false</code> |  |
| [options.cts] | <code>Boolean</code> | <code>false</code> |  |
| [options.dsr] | <code>Boolean</code> | <code>false</code> |  |
| [options.dtr] | <code>Boolean</code> | <code>true</code> |  |
| [options.rts] | <code>Boolean</code> | <code>true</code> |  |


-

<a name="module_serialport--SerialPort..BaseBinding+get"></a>

##### `baseBinding.get()` ⇒ <code>Promise</code>
从打开的串口中获得控制标识(CTS, DSR, DCD).

**Kind**: 实例 <code>[BaseBinding](#module_serialport--SerialPort..BaseBinding)</code>  
**Returns**: <code>Promise</code> - 当标识被获取后返回.  
**Throws**:

- <code>TypeError</code> 当给定一个无效的参数，将会抛出TypeError错误.


-

<a name="module_serialport--SerialPort..BaseBinding+flush"></a>

##### `baseBinding.flush()` ⇒ <code>Promise</code>
接收到的冲洗 (丢弃)的数据不会被读写也不会传输.

**Kind**: 实例方法 <code>[BaseBinding](#module_serialport--SerialPort..BaseBinding)</code>  
**Returns**: <code>Promise</code> - 当冲洗操作结束后返回.  
**Throws**:

- <code>TypeError</code> 当给定一个无效的参数，将会抛出TypeError错误.


-

<a name="module_serialport--SerialPort..BaseBinding+drain"></a>

##### `baseBinding.drain()` ⇒ <code>Promise</code>
耗尽等待所有输出数据被传输到串口后.

**Kind**: instance method of <code>[BaseBinding](#module_serialport--SerialPort..BaseBinding)</code>  
**Returns**: <code>Promise</code> - 耗尽操作结束后调用.  
**Throws**:

- <code>TypeError</code>当给定一个无效的参数，将会抛出TypeError错误.


-

<a name="module_serialport--SerialPort..BaseBinding.list"></a>

##### `BaseBinding.list()` ⇒ <code>Promise</code>
从元数据中找回可用的串口列表. 只有“串口名”是可用的，所有其他的字段如果它们不可用，将会无意义。 `串口名` 也是一个路径或者一个标识符(例如 `COM1`)用来打开串口.

**Kind**: 实例方法 <code>[BaseBinding](#module_serialport--SerialPort..BaseBinding)</code>  
**Returns**: <code>Promise</code> - 串口列表数组[info objects](#module_serialport--SerialPort.list).  

-

<a name="module_serialport--SerialPort..errorCallback"></a>

#### `SerialPort~errorCallback` : <code>function</code>
错误或者null的回调

**Kind**: 内部类型定义 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

| 参数 | 类型 |
| --- | --- |
| error | <code>error</code> | 


-

<a name="module_serialport--SerialPort..modemBitsCallback"></a>

#### `SerialPort~modemBitsCallback` : <code>function</code>
控制标识(cts, dsr, dcd)一个错误或者对象产生回调.

**Kind**: 内部类型定义 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

| 参数 |类型 |默认 |
| --- | --- | --- |
| error | <code>error</code> |  | 
| status | <code>object</code> |  | 
| [status.cts] | <code>boolean</code> | <code>false</code> | 
| [status.dsr] | <code>boolean</code> | <code>false</code> | 
| [status.dcd] | <code>boolean</code> | <code>false</code> | 


-

<a name="module_serialport--SerialPort..openOptions"></a>

#### `SerialPort~openOptions` : <code>Object</code>
**Kind**: 内部类型定义 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  
**Properties**

| 名称 | 类型 | 默认 | 描述 |
| --- | --- | --- | --- |
| Binding | <code>module:serialport~Binding</code> |  | 硬件访问绑定, 绑定是node SreialPort如何和底层系统通信.默认的，我们自动判断Windows (`WindowsBinding`), Linux (`LinuxBinding`) 和 OSX (`DarwinBinding`)系统，以及加载合适我们系统的模块. |
| autoOpen | <code>boolean</code> | <code>true</code> | 在 `nextTick`自动打开串口 |
| lock | <code>boolean</code> | <code>true</code> |防止其他进程打开串口. 目前不支持Windows系统. |
| baudRate | <code>number</code> | <code>9600</code> | 已经打开的串口的波特率. 这个应该匹配一个常用的波特率，比如 110, 300, 1200, 2400, 4800, 9600, 14400, 19200, 38400, 57600, 115200. 这些是不确定的, 设备连接到串口上将支持请求的波特率，即使串口自己支持那个波特率。 |
| dataBits | <code>number</code> | <code>8</code> |必须是其中之一: 8, 7, 6, or 5. |
| stopBits | <code>number</code> | <code>1</code> | 必须是其中之一: 1 or 2. |
| highWaterMark | <code>number</code> | <code>16384</code> | 读写缓存区大小，默认是 16k |
| parity | <code>string</code> | <code>&quot;none&quot;</code> | 必须是其中之一: 'none', 'even', 'mark', 'odd', 'space' |
| rtscts | <code>boolean</code> | <code>false</code> | 流控制设置 |
| xon | <code>boolean</code> | <code>false</code> | 流控制设置 |
| xoff | <code>boolean</code> | <code>false</code> | 流控制设置 |
| xany | <code>boolean</code> | <code>false</code> | 流控制设置 |
| bindingOptions | <code>object</code> |  | 设置特定的绑定选项 |
| bindingOptions.vmin | <code>number</code> | <code>1</code> | 查看[`man termios`](http://linux.die.net/man/3/termios) LinuxBinding和 DarwinBinding |
| bindingOptions.vtime | <code>number</code> | <code>0</code> | 查看[`man termios`](http://linux.die.net/man/3/termios) LinuxBinding 和 DarwinBinding |


-

<a name="module_serialport--SerialPort..listCallback"></a>

#### `SerialPort~listCallback` : <code>function</code>
这个回调类型叫做 `requestCallback`，作为一个全局标识展示。

**Kind**: 内部类型定义 <code>[SerialPort](#exp_module_serialport--SerialPort)</code>  

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| error | <code>error</code> |  |
| ports | <code>array</code> | 串口信息的对象数组 |


-


## 命令行工具
如果你全局安装了 `serialport`. (例如 `npm install -g serialport`) 你会获得两个命令行工具.

### 串口列表
`serialport-list` 将会通过不同的格式列出所有可用的串口.

```bash
$ serialport-list -h

  Usage: serialport-list [options]

  List available serial ports

  Options:

    -h, --help           输出帮助信息
    -V, --version        输出版本号
    -f, --format <type>  输出的格式： text, json, or jsonline. 默认的是: text


$ serialport-list
/dev/cu.Bluetooth-Incoming-Port
/dev/cu.usbmodem1421    Arduino (www.arduino.cc)

$ serialport-list -f json
[{"comName":"/dev/cu.Bluetooth-Incoming-Port"},{"comName":"/dev/cu.usbmodem1421","manufacturer":"Arduino (www.arduino.cc)","serialNumber":"752303138333518011C1","locationId":"0x14200000","vendorId":"0x2341","productId":"0x0043"}]

$ serialport-list -f jsonline
{"comName":"/dev/cu.Bluetooth-Incoming-Port"}
{"comName":"/dev/cu.usbmodem1421","manufacturer":"Arduino (www.arduino.cc)","serialNumber":"752303138333518011C1","locationId":"0x14200000","vendorId":"0x2341","productId":"0x0043"}
```

### 串口终端
`serialport-term` 提供基础的命令的接口给一个串口通信使用。 通过`ctrl+c`退出.

```bash
$ serialport-term -h

  Usage: serialport-term -p <port> [options]

  A basic terminal interface for communicating over a serial port. Pressing ctrl+c exits.

  Options:

    -h, --help                     输出帮助信息
    -V, --version                  输出版本号
    -l --list                      列出可用串口然后退出
    -p, --port, --portname <port>  串口的路径或者名称
    -b, --baud <baudrate>          波特率，默认是: 9600
    --databits <databits>          数据字节 默认是: 8
    --parity <parity>              奇偶性，默认是: none
    --stopbits <bits>              停止位，默认是: 1
    --echo --localecho             打印类型，你输入它们时.

$ serialport-term -l
/dev/cu.Bluetooth-Incoming-Port
/dev/cu.usbmodem1421    Arduino (www.arduino.cc)
```

