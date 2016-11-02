# 步骤显示控件配置

```javascript
{
	type: 'stepView', // 控件类型
    explain: '我是当前步骤的说明文字',
	displayData: function(data) {
		return { // 返回显示数据
			list: ['预约中', '感应', '工作'], //步骤
			stepNow: 0 // 当前步骤序号，从 0 开始计数
		}
	}
}
```