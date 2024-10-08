问题描述：
useSmallerSize功能，在切换屏幕缩放率的时候偶尔会出现问题，例如从125%切换到250%时，不会自动勾选“缩小”按钮，或者从250%切换到125%时，会自动勾选上“缩小”按钮。

问题解决：
在change事件绑定的回调函数中打印输出发现，change事件没有成功触发，在MDN上查找得知，change事件的返回值只有true和false，如果绑定的屏幕缩放值改变了或者从别的值变为绑定的缩放值才会返回true，其他情况都返回false。网上搜索js监听屏幕缩放率方法，发现change事件只对返回true的结果做监听，要解决不监听的问题只能在回调函数里，执行完逻辑操作后解绑再绑定change事件，这样change事件每次屏幕缩放率变化都会成功监听。

问题描述：
在displayScale不变的情况下，调整textScale从250%到110%左右会出现widget显示不完全的情况。

问题解决：
textScale变化会首先被textScale相关事件监听器监听到，widget大小变化，而后由于DPR也发生了变化，会随即触发displayScale相关事件回调，widget大小又会变化。可能是因为两者都对widget大小有操作，导致冲突产生bug。对setTimeout定时器做单例操作，即同一时刻只有一个定时器存在。