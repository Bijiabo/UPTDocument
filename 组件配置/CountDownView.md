# 倒计时显示控件配置

```javascript
{
    type: 'countDownView',
    displayData: function(data) {
        return {
            mainExplain: '剩余时间',
            main: '00:00:01',
            state: '预约中',
            allTime: '总剩余时间（00:50:49）',
            additional: '附加信息...',
            currentStep: 2,
            allStep: 5
        }
    }
}
```