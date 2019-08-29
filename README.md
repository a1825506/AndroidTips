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
