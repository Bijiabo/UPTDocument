# 主界面信息显示控件

格式说明

```javascript
{
	type: 'infoView',
	displayData: function(data) {
		var _displayData = {
			bigNumber: ['--', '--', '--'],
			badgeTitle: "剩余时间",
			status: [],
			director: false,
			url: '/work/app.html'
		};
        return _displayData;
    }
}
```

举例(`格兰仕微波炉BM1(G0)`)：

```javascript
{
	type: 'infoView',
	displayData: function(data) {
		var _displayData = {
			bigNumber: ['--', '--', '--'],
			badgeTitle: "剩余时间",
			status: [],
			director: false,
			url: '/work/app.html'
		};

		// 判断工作食谱
		if (data.WorkStatus !== '0') {
			var modeList = ["云食谱", "省电", "快速启动", "光波", "光波组合1", "光波组合2", "营养解冻", "智能除味", "微波杀菌", "光波杀菌", "蒸汽清洁", "煮水饺", "煲汤", "煮稀饭", "煮米饭", "烤蛋糕", "烧排骨", "烤红薯", "烤鸡翅", "清蒸鱼", "蒸馒头/包子", "蒸水蛋", "自动翻热", "宝宝粥", "宝宝牛奶", "宝宝果泥", "酸奶", "微波"];
			var currentMode = modeList[Number(data.WorkMode)];
			if (currentMode) {
				_displayData.status.push(currentMode);
			}
		}

		// 判断工作状态
		var statusList = ["待机", "预约中", "工作中", "暂停中", "童锁锁定", "完成", "感应中", "感应暂停中"];
		var currentStatus = statusList[Number(data.WorkStatus)];
		if (currentStatus) {
			_displayData.status.push(currentStatus);
		}

		// 判断工作时间
		var timeToArray = function(time, arrayLength) {
				var timeArray = [];
				var _time = Number(time);
				var numberToString = function(n) {
						if (n < 10) {
							return '0' + n.toString();
						}
						return n.toString();
					};

				if (time > 3600) {
					timeArray.push(numberToString(Math.floor(_time / 3600)));
					_time = time % 3600;
				}
				if (time > 60) {
					timeArray.push(numberToString(Math.floor(_time / 60)));
					_time = time % 60;
				}

				timeArray.push(numberToString(_time));

				if (arrayLength) {
					if (timeArray.length < arrayLength) {
						var additionalArray = [];
						for (var i = 0, len = arrayLength - timeArray.length; i < len; i++) {
							additionalArray.push('00');
						}
						timeArray = additionalArray.concat(timeArray);
					}
				}

				return timeArray;
			};

		if (['0', '6', '7'].indexOf(data.WorkStatus) >= 0) {
			_displayData.bigNumber = ['--', '--', '--'];
		} else if (data.WorkStatus === '1') {
			_displayData.bigNumber = timeToArray(data.TM_Start, 2);
		} else {
			_displayData.bigNumber = timeToArray(data.WorkTime, 3);
		}

		// 判断是否可跳转
		_displayData.director = data.WorkStatus !== '0';

		return _displayData;
	}
}
```