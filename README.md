# 2016-5
Just got back from Shanghai, but also in the bead aggregates company


安卓开发 想要获取某个View的高度（我是在做滚动浮层的时候用到的）

1.activity中有个onWindowFocusChanged()方法，可以获取控件的大小，别的地方可能会调用过早导致获取不到实际的大小

 @Override
    public void onWindowFocusChanged(boolean hasFocus) {
        super.onWindowFocusChanged(hasFocus);
       if (hasFocus){//获取焦点
            heightmiddle = oldconent_floatlayout.getTop();
            MyLog.e(TAG, "控件初始高度:" + heightmiddle);
        }
    }
2.fragment 没有onWindowFocusChanged()方法，不过可以调用视图树ViewTreeObserver的方法来实现：

ViewTreeObserver observer= oldconent2_floatlayout.getViewTreeObserver();
/**对视图变化进行监听的观察者    代替activity的onWindowFocusChanged()方法*/
observer.addOnPreDrawListener(new ViewTreeObserver.OnPreDrawListener() {
    @Override
     public boolean onPreDraw() {
        if (!isMeasured){  
            isMeasured=true;
            heightmiddle = oldconent_floatlayout.getTop();
            MyLog.e(TAG, "Fragment控件初始高度:" + heightmiddle);
        }
        return true;
    }
});

