```
Handler handler = new Handler();
//3 秒后跳转到主页面
handler.postDelayed(new Runnable() {
    @Override
    public void run() {
        Intent intent = new Intent(LauncherActivity.this, HomeActivity.class);
        startActivity(intent);
        // Activity 切换淡入淡出动画
        overridePendingTransition(android.R.anim.fade_in, android.R.anim.fade_out);
        finish();
    }
}, 3000);
```

