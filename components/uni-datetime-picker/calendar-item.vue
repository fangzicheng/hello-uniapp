<template>
	<view class="uni-calendar-item__weeks-box" :class="{
		'uni-calendar-item--disable':weeks.disable,
		'uni-calendar-item--before-checked-x':weeks.beforeMultiple,
		'uni-calendar-item--multiple': weeks.multiple,
		'uni-calendar-item--after-checked-x':weeks.afterMultiple,
		}" @click="choiceDate(weeks)" @mouseenter="handleMousemove(weeks)">
		<view class="uni-calendar-item__weeks-box-item" :class="{
				'uni-calendar-item--isDay-text': weeks.isDay,
				'uni-calendar-item--checked':calendar.fullDate === weeks.fullDate && calendar.userChecked,
				'uni-calendar-item--checked-range-text': checkHover,
				'uni-calendar-item--before-checked':weeks.beforeMultiple,
				'uni-calendar-item--multiple': weeks.multiple,
				'uni-calendar-item--after-checked':weeks.afterMultiple,
				'uni-calendar-item--disable':weeks.disable,
				}">
			<text v-if="selected&&weeks.extraInfo" class="uni-calendar-item__weeks-box-circle"></text>
			<text class="uni-calendar-item__weeks-box-text">{{weeks.date}}</text>
			<!-- 	<text v-if="!lunar&&!weeks.extraInfo && weeks.isDay" class="uni-calendar-item__weeks-lunar-text">今天</text>
			<text v-if="lunar&&!weeks.extraInfo" class="uni-calendar-item__weeks-lunar-text" >{{weeks.isDay?'今天': (weeks.lunar.IDayCn === '初一'?weeks.lunar.IMonthCn:weeks.lunar.IDayCn)}}</text> -->
			<!-- <text v-if="weeks.extraInfo&&weeks.extraInfo.info" class="uni-calendar-item__weeks-lunar-text">{{weeks.extraInfo.info}}</text> -->
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			weeks: {
				type: Object,
				default () {
					return {}
				}
			},
			calendar: {
				type: Object,
				default: () => {
					return {}
				}
			},
			selected: {
				type: Array,
				default: () => {
					return []
				}
			},
			lunar: {
				type: Boolean,
				default: false
			},
			checkHover: {
				type: Boolean,
				default: false
			}
		},
		methods: {
			choiceDate(weeks) {
				this.$emit('change', weeks)
			},
			handleMousemove(weeks) {
				this.$emit('handleMouse', weeks)
			}
		}
	}
</script>

<style scoped>
	.uni-calendar-item__weeks-box {
		flex: 1;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		justify-content: center;
		align-items: center;
		margin: 3px 0;
	}

	.uni-calendar-item__weeks-box-text {
		font-size: 12px;
	}

	.uni-calendar-item__weeks-lunar-text {
		font-size: 12px;
		color: #333;
	}

	.uni-calendar-item__weeks-box-item {
		position: relative;
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		justify-content: center;
		align-items: center;
		width: 40px;
		height: 40px;
		/* #ifdef H5 */
		cursor: pointer;
		/* #endif */
	}

	.uni-calendar-item__weeks-box-circle {
		position: absolute;
		top: 5px;
		right: 5px;
		width: 8px;
		height: 8px;
		border-radius: 8px;
		background-color: #dd524d;
	}

	.uni-calendar-item__weeks-box .uni-calendar-item--disable {
		color: #c0c0c0;
		cursor: default;
	}

	.uni-calendar-item__weeks-box .uni-calendar-item--isDay-text {
		color: #007aff;
	}

	.uni-calendar-item--isDay {
		background-color: #007aff;
		opacity: 0.8;
		color: #fff;
	}

	.uni-calendar-item--extra {
		color: #dd524d;
		opacity: 0.8;
	}

	.uni-calendar-item__weeks-box .uni-calendar-item--checked {
		background-color: #007aff;
		box-sizing: border-box;
		border: 6px solid #f2f6fc;
		color: #fff;
		opacity: 0.8;
	}

	.uni-calendar-item--multiple .uni-calendar-item--checked-range-text {
		color: #333;
	}

	.uni-calendar-item--multiple {
		background-color: #f2f6fc;
		opacity: 0.8;
	}

	.uni-calendar-item--multiple .uni-calendar-item--before-checked {
		background-color: #409eff;
		color: #fff !important;
		box-sizing: border-box;
		border: 6px solid #f2f6fc;
	}

	.uni-calendar-item--multiple .uni-calendar-item--after-checked {
		background-color: #409eff;
		color: #fff !important;
		box-sizing: border-box;
		border: 6px solid #f2f6fc;
	}

	.uni-calendar-item--before-checked-x {
		background-color: #f2f6fc;
	}

	.uni-calendar-item--after-checked-x {
		background-color: #f2f6fc;
	}
</style>