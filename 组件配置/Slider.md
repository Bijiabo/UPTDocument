# 滑动选择器控件

```javascript
{
	type: 'slider',
	key: 'Temperature_Target',
	title: '温度设定',
	min: 35,
	max: 48,
	step: 1,
	defaultValue: '39',
	unit: '℃',
	enable: {
		type: '&&',
		condition: [{
			key: 'WorkMode',
			equal: '0'
		}]
	}
},
```