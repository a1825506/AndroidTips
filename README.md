  1# 项目中经常用到倒计时的功能，比如说限时抢购，手机获取验证码等等。而google官方也帮我们封装好了一个类:CountDownTimer,使我们的开发更加方便(activity、fragment中使用时注意释放)

   class TimeCount extends CountDownTimer {
   
        public TimeCount(long millisInFuture, long countDownInterval) {
        
            super(millisInFuture, countDownInterval);
        }

        @Override
        public void onTick(long millisUntilFinished) {
           ////这个是每次间隔指定时间的回调，millisUntilFinished：剩余的时间，单位毫秒
        }

        @Override
        public void onFinish() {
        //这个是倒计时结束的回调
        }
    }
    
    TimeCount   timeCount =  new TimeCount(60000, 1000);
    timeCount.start();
 
 2# EventBus、BroadCast和Handler 比较
    BroadCast：广播是相对消耗时间、空间最多的一种方式。它是四大组件之一，许多系统级的事件都是通过广播来通知的，比如：电量的变化、网络的变化、短信的接     收和发生状态等。
    优点：与sdk连接紧密，当需要与Android交互时非常方便。而且可以实现跨进程通讯。必要时还能启动Activity
    缺点：资源占用较多，且需要依赖Context
    Handler中；一般用于线程间通讯。handler的定义类和内部类是绑定的，这就造成了事件发布者和接受者之间的高耦合。使用handler最明显的优点是发生问题时，     可以非常明确、快速的进行定位。
    EventBus的优势在于调度灵活，不需要依赖Context也没有Handler那样的耦合。可继承、优先级、粘滞是EventBus比之于BroadCast和观察者最大的优点。缺点     也很明显，EventBus中的事件分发是通过注解函数的参数类型决定的，这就导致了当接受者过多或相同参数时很难理清消息流。
    
3# 图片裁剪 https://github.com/Yalantis/uCrop 框架

4# SharedPreferences 替代方案 MMKV——基于 mmap 的高性能通用 key-value 组件 https://github.com/Tencent/MMKV/blob/master/readme_cn.md

5# Android Activity的四种启动模式
   .standard:这是 Activity 的默认启动模式，每次激活 Activity 的时候都会创建一个新的 Activity 实例，并放入任务栈中。
   .singleTop:如果在任务的栈顶正好存有该 Activity 的实例，则会通过调用 onNewIntent() 方法进行重用，否则就会同 standard 模式一样，创建新的实例               并放入栈顶。即便栈中已经存在了该 Activity 的实例，也会创建新的实例。使用场景：资讯阅读类 APP 的内容界面。
   .singleTask：只要栈中已经存在了该 Activity 的实例，就会直接调用 onNewIntent() 方法来实现重用实例。重用时，直接让该 Activity 的实例回到栈 。                 顶，并且移除之前它上面的所有 Activity 实例。如果栈中不存在这样的实例，则和 standard 模式相同。使用场景：浏览器的主页面，或者大部                 分 APP 的主页面。
   .singleInstance: 在一个新栈中创建该 Activity 的实例，并让多个应用共享该栈中的该 Activity 实例。一旦该模式的 Activity 实例已经存在于某个栈                       中，任何应用再激活该 Activity 时都会重用该栈中的实例，是的，依然是调用 onNewIntent() 方法。 Android 系统的来电页面，多次                     来电均是使用的同一个 Activity 。
   startActivityForResult启动Activity导致singleTop模式失效。
   
 6# 单例模式(保证线程安全的懒汉式)
     public class Instance{
       private static Instance instance;
       
       public Instance(){
       }
       public static Instance getInstance(){
           if(instance==null){
           synchronized(Instance.class){
           if(instance==null)
              instance = new Instance();
           }
           }
           return instance;
           }
       }
     
     } 
   
7# 建造者模式
package com.senon.lib_common.utils;

public class LoginManager {

    public boolean isSavePwd;

    public boolean isAutoLogin;

    public boolean isBootLauncher;

    public boolean isCrashOnRestart;


    public LoginManager(Builder builder){
        this.isAutoLogin = builder.isAutoLogin;
        this.isBootLauncher = builder.isBootLauncher;
        this.isCrashOnRestart = builder.isCrashOnRestart;
        this.isSavePwd = builder.isSavePwd;
    }


    public static class Builder{

        boolean isSavePwd;

        boolean isAutoLogin;

        boolean isBootLauncher;

        boolean isCrashOnRestart;

        public Builder(){
            this.isSavePwd=false;
            this.isAutoLogin=false;
            this.isBootLauncher=false;
            this.isCrashOnRestart=false;

        }

        public Builder isSavePwd(boolean savePwd){
            this.isSavePwd = savePwd;
            return this;
        }

        public Builder isAutoLogin(boolean autoLogin){
            this.isAutoLogin = autoLogin;
            return this;
        }

        public Builder isBootLauncher(boolean isBootLauncher){
            this.isBootLauncher = isBootLauncher;
            return this;
        }

        public Builder isCrashOnRestart(boolean isCrashOnRestart){
            this.isCrashOnRestart = isCrashOnRestart;
            return this;
        }

        public LoginManager build(){
            return new LoginManager(this);
        }
    }
    
}

8# 事件分发顺序 activity->viewGroup->view
   涉及到的方法 activity:dispatchTouchEvent()->viewGroup:dispatchTouchEvent()->viewGroup:onInterceptTouchEvent()-       >view:dispatchTouchEvent()->view:onTouchEvent()->viewGroup:onTouchEvent()->activity:onTouchEvent()
   只有在viewGroup中有拦截事件onInterceptTouchEvent()，view中消费事件。
   
9# 自定义控件步骤
   1、自定义属性的声明与获取
   2、测量 onMeasure()
   3、布局 onLayout()
   4、绘制 onDraw()
   
   

 
