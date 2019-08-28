  1# 项目中经常用到倒计时的功能，比如说限时抢购，手机获取验证码等等。而google官方也帮我们封装好了一个类:CountDownTimer,使我们的开发更加方便

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
