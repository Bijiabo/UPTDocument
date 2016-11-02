# 模式选择控件配置

格式说明

```javascript
{
	type: 'grid',
	key: 'WorkMode',
	gridNum: '3',
	defaultValue: '0',
	title: '光波/组合', // 标题
	linkToPage: './setting/app.html', // 可选，或填写，则不下发命令，而是跳转到对应页面
	map: [{ // 按钮配置
		txt: '光波',
		value: '4'
	}, {
		txt: '光波组合1',
		value: '5'
	}, {
		txt: '光波组合2',
		value: '6'
	}],
	enable: { // 判断条件
		type: '&&',
		condition: [{
			key: 'OnOff_Power',
			equal: '1'
		}]
	}
}
```