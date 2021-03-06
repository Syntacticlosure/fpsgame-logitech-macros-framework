# fpsgame-logitech-macros-framework
适用于罗技鼠标的FPS游戏鼠标宏辅助框架 

适用于任何单机FPS游戏，作用是自动压枪，请不要将其使用于多人在线FPS游戏，由此引起的任何后果，概不负责。 

让不会编程的人也能轻松写出鼠标宏，觉得好用，请给star。 


# 步骤： 

1.罗技鼠标（推荐G502） 

2.罗技游戏软件 Logitech Gaming Software 

3.下载framework.lua，放到本地的某个目录中，比如c:\scripts\framework.lua 

4.打开罗技游戏软件，切换到自动游戏检测。 

5.右击游戏图标，单击编辑脚本选项。 

6.将所有代码清空。 

7.载入框架文件：
```
dofile("c:\\scripts\\framework.lua")
``` 

8.载入武器数据：
为了达到最好的压枪效果，您必须载入武器的各种数据，数据越精确，压枪效果也就越优秀。

假设我们有一把武器叫做ak，那么你需要以下参数： 

初始化武器： 
```
ak = {}
```

ak的容弹量：
```
ak.ammo = 30
```
ak两发子弹之间的间隔时间（毫秒）:
```
ak.interval = 1000
```
ak的每一发子弹的落点(像素): 
```
ak.data = {}
ak.data[1] = {100,200}
ak.data[2] = {94,180}
.......
ak.data[30] = {x,y}
```
我们第一次压枪就是向屏幕右侧移动6个像素，向屏幕下侧移动20个像素。 

ak的修正系数：
我们允许对压枪的移动的像素数进行一定的修正。
```
ak.factor =0.5
```
设置该修正系数之后，我们第一次压枪会向屏幕右侧移动6/2=3个像素，向屏幕下侧移动20/2=10个像素。 如果不需要任何修正，请直接将ak.factor设置为1。

9.当武器数据设置完成后，请直接调用initWeapon初始化武器：
```
initWeapon(ak47)
...
```

10.你还需要将武器绑定到某个按键上：
```
bindKey(4,ak)
bindKey(5,m4)
bindKey(6,noWeapon)
```
当你点击鼠标上的G4键（罗技G502鼠标）时，切换到ak压枪模式，当点击了鼠标上的G5键时，切换到m4压枪模式，点击鼠标上的G6键（G切换）后，切换到不压枪模式。

11.保存脚本，享受游戏。 

# 更新
添加makeInexactWeapon函数，函数原型： 
```
function makeInexactWeapon(step)
```
step为自然数，创建一个武器，压枪方式为每10ms向屏幕下方移动step像素。 

通过该方式创建的武器，往往其弹道是垂直式的，一旦水平后坐力比较大，效果就不如步骤里面创建武器的办法。
武器后坐力越大，step越大，武器后坐力越小，step越小。
如果武器有精确的弹道数据，建议采用步骤里面的办法。
例子：
```
bindKey(4,makeInexactWeapon(3))
```

新增自动连点器autoClicker,用法：
```
bindKey(4,autoClicker)
```

