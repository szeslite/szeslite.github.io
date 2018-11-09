## Welcome to GitHub Pages

季望沙雕
# android 2D 图形
我们平时使用的控件，自定义控件，或者直接使用canvas绘图底层都是调用的2D图形库，那么2D图形库的本质是什么？今天我们就来看看android的两大图形系统，一个是canvas，一个是opengl（3D）.
  - 同样的问自己一个问题，作为一个图形库，需要哪些功能？


# 自己来设计Actviity
  既然是打算自己来设计一个东西，我们首先就必须知道这个东西要满足哪些功能。仔细想想我们开发中使用到Activity的哪些功能，首先最重要的是，控制UI的显示，然后打交道最多的就是Activity的几个生命周期了，onCreate，onResume，onPause等等，但是生命周期仔细想想是不是都是跟屏幕的交互，所以这一块可以放在与系统的交互中考虑。还有哪些功能？好像没有了，没关系，第一步我们先考虑到这里。


  那么我们就从控制UI这个功能开始设计Activity，Activity是如何控制UI的呢，首先我们需要了解的是android系统的UI是从哪里来的呢？
  首先我们先确定，UI是在屏幕上显示的，那么屏幕作为一个独立的硬件设备，接口是什么样的呢？
  CPU又是如何把数据正确的发送给屏幕并且刷新的呢？
  我们首先知道UI都是配置在XML文件中的，或者通过代码生成，比如Button button=new Button().
  在Android UI系统中我们说过，android的UI是通过window来控制的.既然已经有一套完整的UI方案了，那么可以猜想Activity所有做的事情就是调用window的接口来完成UI的绘制。
  
  
  那么如此看来Actvitiy就是一个壳子而已嘛。
  
  Activity的setContentView就是调用Window的setContentView，但是setContentView的也只是调用ViewGroup.addView而已，那么究竟是谁来绘制的UI呢，这里只能猜想是View体系自己完成了绘制工作。
  
  可以看到在View.draw()中完成了UI的绘制，并且分成了几个步骤，
   /*
         * Draw traversal performs several drawing steps which must be executed
         * in the appropriate order:
         *
         *      1. Draw the background
         *      2. If necessary, save the canvas' layers to prepare for fading
         *      3. Draw view's content
         *      4. Draw children
         *      5. If necessary, draw the fading edges and restore layers
         *      6. Draw decorations (scrollbars for instance)
         */


其中所有的draw方法最终都是调用的canvas来完成的绘制，所以离目标越来越近了，canvas获取就是我们的目标，
事实上，android开发者文档中也说明了，使用 Canvas 或 OpenGL像屏幕绘制图片。
canvas 负责2d图形，openGL 负责3d。
canvas的draw相关方法最终会调用baseCanvas的相关draw方法.baseCanvas最终会调用到native中的方法。



[点次参加阿里云双11一折团购](https://promotion.aliyun.com/ntms/yunparter/invite.html?userCode=71knnyqg).

