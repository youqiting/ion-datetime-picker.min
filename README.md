# ion-datetime-picker.min

https://blog.csdn.net/weixin_41195867/article/details/105048257

angularjs由datetimepicker,改造的带 ‘按日切换’/'按月切换’按钮的自定义组件（纯为实现需求和效果改造，目测可用，不喜勿喷。可以接受优化建议和思路）

改造前：可选择年月日时间，年月日，时间


增加：按月、日选择的切换


改造后的使用：
html:

<div class="flex search-date search-border item-span">
    <p class="date-p" style="border: none;" ion-datetime-picker ng-model="$parent.startDate" datetype="isMonthValid" only-valid="{}" my-click="getTpye(isMonth)">
        <text ng-show="isMonthValid=='true'" class="newDate-text">{{startDate| date: "yyyy-MM"}}</text>
        <text ng-show="isMonthValid=='false'" class="newDate-text">{{startDate| date: "yyyy-MM-dd"}}</text>
        <em class="date-arrow"></em>
    </p>
    <p class="date-get">到</p>
    <p class="date-p" style="border: none;" ion-datetime-picker ng-model="$parent.endDate" datetype="isMonthValid" only-valid="{'after': startDate}" my-click="getTpye(isMonth)">
        <text ng-show="isMonthValid=='true'" class="newDate-text">{{endDate| date: "yyyy-MM"}}</text>
        <text ng-show="isMonthValid=='false'" class="newDate-text">{{endDate| date: "yyyy-MM-dd"}}</text>
        <em class="date-arrow"></em>
    </p>
</div>
1
2
3
4
5
6
7
8
9
10
11
12
13
controller代码：

$scope.isMonthValid = "false"; //用String:'true'/'false'
$scope.getTpye = function(isMonth) {
	// $scope.isMonth = isMonth;
	$scope.isMonthValid = isMonth ? "true" : "false";
}
$scope.$watch('startDate', function() { //监听开始日期
	if ($scope.startDate.getTime() > $scope.endDate.getTime()) {
		var temp = null;
		temp = $scope.endDate;
		$scope.endDate = $scope.startDate;
		$scope.startDate = temp;
	}
});
1
2
3
4
5
6
7
8
9
10
11
12
13
css:

.search-border {
    border: 1px solid;
    width: 255px;
    border-radius: 20px;
    padding: 5px 0 0 10px;
}
.search-date {
    overflow: hidden;
    box-sizing: border-box;
    font-size: 14px;
    align-items: center;
    -webkit-align-items: center;
    margin-top: 10px;
}
.item-span {
    color: #FF6600 !important;
    border: 1px solid #FF6600 !important;
}
.flex {
    display: flex;
    display: -webkit-flex;
}
.search-date p {
    margin: 0;
}

.date-p {
    padding-bottom: 5px;
    /* border-bottom: 1px solid #ccc; */
    position: relative;
    width: 100px;
    font-size: 14px;
}
.date-get {
    padding: 0 10px;
}
.newDate-text {
    display: inline-block;
    width: 82%;
    text-align: center;
}
————————————————
版权声明：本文为CSDN博主「youqiting」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_41195867/article/details/105048257





