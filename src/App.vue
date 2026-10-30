<script>
import { onMounted, reactive, onUnmounted, inject, ref, computed } from 'vue';//组件导入
import getDate from './js/time.js'//导入时间函数
import Speed1xf5 from "./components/Speed1xf5.vue";
import Speed1xf6 from "./components/Speed1xf6.vue";
import Speed1xf7 from "./components/Speed1xf7.vue";
import Speed1xf8 from "./components/Speed1xf8.vue";
import Speed2xf5 from "./components/Speed2xf5.vue";
import Speed2xf6 from "./components/Speed2xf6.vue";
import Speed2xf7 from "./components/Speed2xf7.vue";
import Speed2xf8 from "./components/Speed2xf8.vue";
import Speed3xf5 from "./components/Speed3xf5.vue";
import Speed3xf6 from "./components/Speed3xf6.vue";
import Speed3xf7 from "./components/Speed3xf7.vue";
import Speed3xf8 from "./components/Speed3xf8.vue";
export default {
	name: 'HomeView',
	components: {
		Speed1xf5,
		Speed1xf6,
		Speed1xf7,
		Speed1xf8,
		Speed2xf5,
		Speed2xf6,
		Speed2xf7,
		Speed2xf8,
		Speed3xf5,
		Speed3xf6,
		Speed3xf7,
		Speed3xf8,
	},

	setup() {
		const worker = inject('worker')
		let flag, flag1, flag2
		const base = reactive
			({
				msg: 0,//基础数据接驳
				symple: 0,//报文标志位
				trainNumber: "",//列车号
				carriageNumber: "",//车厢号
			})

		const x_speedxf = reactive({
			xfarray11_dianzu: [0, 0, 0, 0],
			xfarray12_dianliu: [0, 0, 0, 0],
			xfarray12_jianxi: [0, 0, 0, 0],
			xfarray13_speed: [0, 0, 0, 0],
			xfarray14_dianya: [0, 0, 0, 0],
			xfarray14_acc: [0, 0, 0, 0],
			xfarray15_speed: [0, 0, 0, 0],
		}
		)
		const x_speedxf2 = reactive({
			xfarray11_dianzu: [0, 0, 0, 0],
			xfarray12_dianliu: [0, 0, 0, 0],
			xfarray12_jianxi: [0, 0, 0, 0],
			xfarray13_speed: [0, 0, 0, 0],
			xfarray14_dianya: [0, 0, 0, 0],
			xfarray14_acc: [0, 0, 0, 0],
			xfarray15_speed: [0, 0, 0, 0],
		}
		)

		const x_speedxf3 = reactive({
			xfarray11_dianzu: [0, 0, 0, 0],
			xfarray12_dianliu: [0, 0, 0, 0],
			xfarray12_jianxi: [0, 0, 0, 0],
			xfarray13_speed: [0, 0, 0, 0],
			xfarray14_dianya: [0, 0, 0, 0],
			xfarray14_acc: [0, 0, 0, 0],
			xfarray15_speed: [0, 0, 0, 0],
		}
		)

		const x_speedxf4 = reactive({
			xfarray11_dianzu: [0, 0, 0, 0],
			xfarray12_dianliu: [0, 0, 0, 0],
			xfarray12_jianxi: [0, 0, 0, 0],
			xfarray13_speed: [0, 0, 0, 0],
			xfarray14_dianya: [0, 0, 0, 0],
			xfarray14_acc: [0, 0, 0, 0],
			xfarray15_speed: [0, 0, 0, 0],
		}
		)

		const TimeData = reactive({
			nowTime: "",
			nowWeek: "",
		})
		const colorSig = (sig) => {
			if (sig) {
				return "#00ffff";
			} else {
				return '#00657F';
			};
		}
		function timeToString(timeObj) {
			var str = "";
			var year = timeObj.getFullYear();
			var month = timeObj.getMonth();
			var date = timeObj.getDate();
			var time = timeObj.toTimeString().split(" ")[0];
			str = time;
			// console.log("------当前日期：" + str);
			return str;
		}
		//增加时间
		const addTime = (num) => {
			var curTime = new Date()
			// console.log(curTime)
			var addSeconds = new Date(curTime.setSeconds(curTime.getSeconds() + num));
			return addSeconds
		}
		const formatDate = () => {
			var date = new Date()// 时间戳为10位需*1000，时间戳为13位的话不需乘1000
			var hour = ('0' + date.getHours()).slice(-2)
			var minute = ('0' + date.getMinutes()).slice(-2)
			var second = ('0' + date.getSeconds()).slice(-2)
			var milsec = date.getMilliseconds()
			// 拼接
			var result = hour + ':' + minute + ':' + second
			// 返回
			return result
		}
		//获取当前时间
		const currentTime = () => {
			setInterval(() => {
				TimeData.nowTime = getDate().nowTime;
				TimeData.nowWeek = getDate().nowWeek;
				////console.log(TimeData)
			}, 1000)
		};
		// onMounted(() => {
		// 	flag = formatDate()
		// 	flag1 = formatDate()
		// 	flag2 = formatDate()
		// 	worker.onmessage = (event) => {
		// 		const message = event.data;
		// 		var data_state = JSON.parse(message)//转换为双层对象
		// 		var symple = data_state.symple // 定义标志位并赋值
		// 		// console.log(symple)
		// 		// console.log(data_state)
		// 		switch (symple) {
		// 			case "01":
		// 				var dianzu_mret_th1 = data_state.dianzu_mret//双层对象替换为单层对象
		// 				//console.log(x_Dianzumret)

		// 				var speed_mret_th1 = data_state.speed_mret
		// 				//console.log(x_Speedmret)
		// 				var dianliu1_mret_th1 = data_state.dianliu1_mret
		// 				//console.log(x_DianLiu1Mret)
		// 				var dianliu2_mret_th1 = data_state.dianliu2_mret
		// 				//console.log(x_DianLiu2Mret)
		// 				var dianya_mret_th1 = data_state.dianya_mret
		// 				//console.log(x_Dianyamret)
		// 				var jiasudu1_mret_th1 = data_state.jiasudu1_mret
		// 				//console.log(x_Jiasudu1mret)
		// 				var jiasudu2_mret_th1 = data_state.jiasudu2_mret
		// 				//console.log(x_Jiasudu2mret)
		// 				var jianxi_mret_th1 = data_state.jianxi_mret
		// 				//console.log(x_Jianximret)
		// 				if (formatDate() > flag) {
		// 					x_speedxf.xfarray11_dianzu = [formatDate(), dianzu_mret_th1.mret8, dianzu_mret_th1.mret9, dianzu_mret_th1.mret10, dianzu_mret_th1.mret11]
		// 					x_speedxf.xfarray12_dianliu = [formatDate(), dianliu2_mret_th1.mret8, dianliu2_mret_th1.mret9, dianliu2_mret_th1.mret10, dianliu2_mret_th1.mret11]
		// 					x_speedxf.xfarray12_jianxi = [formatDate(), jianxi_mret_th1.mret8, jianxi_mret_th1.mret9, jianxi_mret_th1.mret10, jianxi_mret_th1.mret11]
		// 					x_speedxf.xfarray13_speed = [formatDate(), speed_mret_th1.mret8, speed_mret_th1.mret9, speed_mret_th1.mret10, speed_mret_th1.mret11]
		// 					x_speedxf.xfarray14_dianya = [formatDate(), dianya_mret_th1.mret8, dianya_mret_th1.mret9, dianya_mret_th1.mret10, dianya_mret_th1.mret11]
		// 					x_speedxf.xfarray14_acc = [formatDate(), jiasudu2_mret_th1.mret8, jiasudu2_mret_th1.mret9, jiasudu2_mret_th1.mret10, jiasudu2_mret_th1.mret11]
		// 					x_speedxf.xfarray15_speed = [formatDate(), speed_mret_th1.mret8, speed_mret_th1.mret9, speed_mret_th1.mret10, speed_mret_th1.mret11]

		// 					x_speedxf2.xfarray11_dianzu = [formatDate(), dianzu_mret_th1.mret12, dianzu_mret_th1.mret13, dianzu_mret_th1.mret14, dianzu_mret_th1.mret15]
		// 					x_speedxf2.xfarray12_dianliu = [formatDate(), dianliu2_mret_th1.mret12, dianliu2_mret_th1.mret13, dianliu2_mret_th1.mret14, dianliu2_mret_th1.mret15]
		// 					x_speedxf2.xfarray12_jianxi = [formatDate(), jianxi_mret_th1.mret12, jianxi_mret_th1.mret13, jianxi_mret_th1.mret14, jianxi_mret_th1.mret15]
		// 					x_speedxf2.xfarray13_speed = [formatDate(), speed_mret_th1.mret12, speed_mret_th1.mret13, speed_mret_th1.mret14, speed_mret_th1.mret15]
		// 					x_speedxf2.xfarray14_dianya = [formatDate(), dianya_mret_th1.mret12, dianya_mret_th1.mret13, dianya_mret_th1.mret14, dianya_mret_th1.mret15]
		// 					x_speedxf2.xfarray14_acc = [formatDate(), jiasudu2_mret_th1.mret12, jiasudu2_mret_th1.mret13, jiasudu2_mret_th1.mret14, jiasudu2_mret_th1.mret15]
		// 					x_speedxf2.xfarray15_speed = [formatDate(), speed_mret_th1.mret12, speed_mret_th1.mret13, speed_mret_th1.mret14, speed_mret_th1.mret15]

		// 					x_speedxf3.xfarray11_dianzu = [formatDate(), dianzu_mret_th1.mret24, dianzu_mret_th1.mret25, dianzu_mret_th1.mret26, dianzu_mret_th1.mret27]
		// 					x_speedxf3.xfarray12_dianliu = [formatDate(), dianliu2_mret_th1.mret24, dianliu2_mret_th1.mret25, dianliu2_mret_th1.mret26, dianliu2_mret_th1.mret27]
		// 					x_speedxf3.xfarray12_jianxi = [formatDate(), jianxi_mret_th1.mret24, jianxi_mret_th1.mret25, jianxi_mret_th1.mret26, jianxi_mret_th1.mret27]
		// 					x_speedxf3.xfarray13_speed = [formatDate(), speed_mret_th1.mret24, speed_mret_th1.mret25, speed_mret_th1.mret26, speed_mret_th1.mret27]
		// 					x_speedxf3.xfarray14_dianya = [formatDate(), dianya_mret_th1.mret24, dianya_mret_th1.mret25, dianya_mret_th1.mret26, dianya_mret_th1.mret27]
		// 					x_speedxf3.xfarray14_acc = [formatDate(), jiasudu2_mret_th1.mret24, jiasudu2_mret_th1.mret25, jiasudu2_mret_th1.mret26, jiasudu2_mret_th1.mret27]
		// 					x_speedxf3.xfarray15_speed = [formatDate(), speed_mret_th1.mret24, speed_mret_th1.mret25, speed_mret_th1.mret26, speed_mret_th1.mret27]

		// 					x_speedxf4.xfarray11_dianzu = [formatDate(), dianzu_mret_th1.mret28, dianzu_mret_th1.mret29, dianzu_mret_th1.mret30, dianzu_mret_th1.mret31]
		// 					x_speedxf4.xfarray12_dianliu = [formatDate(), dianliu2_mret_th1.mret28, dianliu2_mret_th1.mret29, dianliu2_mret_th1.mret30, dianliu2_mret_th1.mret31]
		// 					x_speedxf4.xfarray12_jianxi = [formatDate(), jianxi_mret_th1.mret28, jianxi_mret_th1.mret29, jianxi_mret_th1.mret30, jianxi_mret_th1.mret31]
		// 					x_speedxf4.xfarray13_speed = [formatDate(), speed_mret_th1.mret28, speed_mret_th1.mret29, speed_mret_th1.mret30, speed_mret_th1.mret31]
		// 					x_speedxf4.xfarray14_dianya = [formatDate(), dianya_mret_th1.mret28, dianya_mret_th1.mret29, dianya_mret_th1.mret30, dianya_mret_th1.mret31]
		// 					x_speedxf4.xfarray14_acc = [formatDate(), jiasudu2_mret_th1.mret28, jiasudu2_mret_th1.mret29, jiasudu2_mret_th1.mret30, jiasudu2_mret_th1.mret31]
		// 					x_speedxf4.xfarray15_speed = [formatDate(), speed_mret_th1.mret28, speed_mret_th1.mret29, speed_mret_th1.mret30, speed_mret_th1.mret31]
		// 					flag = timeToString(addTime(1))
		// 				}
		// 				break;
		// 		}
		// 	}
		// 	currentTime()
		// })
		// ====== 可配置项默认值（运行时可通过 config.json 覆盖）======
		const DEFAULT_TITLE = '高速磁浮悬浮状态诊断模块'
		const DEFAULT_LOGOS = [
			{ src: 'logo.png', width: 124.65, height: 41.43 }
		]

		const title = ref(DEFAULT_TITLE)
		const logos = ref(DEFAULT_LOGOS)
		const logoGap = ref(24)
		const titleAlign = ref('center') // 主标题对齐方式：'center' 居中 | 'left' 原位置

		// logo 区域基准参数（与原设计保持一致）
		const LOGO_START_X = 39.2
		const LOGO_BASE_Y = 10.45
		const LOGO_MAX_HEIGHT = 41.43
		const LOGO_DEFAULT_WIDTH = 124.65

		// 多 logo 一行布局：从左至右依次排列，垂直方向居中对齐
		const logoItems = computed(() => {
			let cursorX = LOGO_START_X
			const list = logos.value
			return list.map((logo, index) => {
				const height = Number(logo.height) > 0 ? Number(logo.height) : LOGO_MAX_HEIGHT
				const width = Number(logo.width) > 0 ? Number(logo.width) : LOGO_DEFAULT_WIDTH
				const y = LOGO_BASE_Y + (LOGO_MAX_HEIGHT - height) / 2
				const item = { x: cursorX, y, width, height, src: logo.src }
				cursorX += width + (index < list.length - 1 ? logoGap.value : 0)
				return item
			})
		})

		// 主标题布局：居中时以画布中线对齐，左对齐时保持原位置
		const TITLE_LEFT_X = 708.5
		const titleProps = computed(() => {
			if (titleAlign.value === 'center') {
				return { x: 960, anchor: 'middle' } // 1920 / 2
			}
			return { x: TITLE_LEFT_X, anchor: 'start' }
		})

		// 运行时加载外部配置文件（打包后位于 dist/config.json，可直接修改无需重新构建）
		onMounted(async () => {
			try {
				const res = await fetch('./config.json', { cache: 'no-cache' })
				if (!res.ok) return
				// 防止 SPA fallback 返回 index.html（非 JSON）导致解析报错
				const contentType = res.headers.get('content-type') || ''
				if (!contentType.includes('application/json')) return
				const config = await res.json()
				if (typeof config.title === 'string' && config.title.trim()) {
					title.value = config.title
				}
				if (Array.isArray(config.logos)) {
					const valid = config.logos.filter(l => l && typeof l.src === 'string' && l.src.trim())
					if (valid.length) logos.value = valid
				}
				if (typeof config.logoGap === 'number' && config.logoGap >= 0) {
					logoGap.value = config.logoGap
				}
				if (typeof config.titleAlign === 'string' && ['center', 'left'].includes(config.titleAlign)) {
					titleAlign.value = config.titleAlign
				}
			} catch (e) {
				console.warn('[配置] 加载 config.json 失败，使用默认配置', e)
			}

			flag = formatDate()
			flag1 = formatDate()
			flag2 = formatDate()
			worker.onmessage = (event) => {
				const message = event.data;
				var data_state = JSON.parse(message)//转换为双层对象
				var symple = data_state.symple // 定义标志位并赋值
				// console.log(symple)
				// console.log(data_state)
				switch (symple) {
					case "01":
						var dianzu_mret_th1 = data_state.dianzu_mret//双层对象替换为单层对象
						//console.log(x_Dianzumret)

						var speed_mret_th1 = data_state.speed_mret
						//console.log(x_Speedmret)
						var dianliu1_mret_th1 = data_state.dianliu1_mret
						//console.log(x_DianLiu1Mret)
						var dianliu2_mret_th1 = data_state.dianliu2_mret
						//console.log(x_DianLiu2Mret)
						var dianya_mret_th1 = data_state.dianya_mret
						//console.log(x_Dianyamret)
						var jiasudu1_mret_th1 = data_state.jiasudu1_mret
						//console.log(x_Jiasudu1mret)
						var jiasudu2_mret_th1 = data_state.jiasudu2_mret
						//console.log(x_Jiasudu2mret)
						var jianxi_mret_th1 = data_state.jianxi_mret
						//console.log(x_Jianximret)
						if (formatDate() > flag) {
							x_speedxf.xfarray11_dianzu = [formatDate(), dianzu_mret_th1.mret8, dianzu_mret_th1.mret9, dianzu_mret_th1.mret10, dianzu_mret_th1.mret11]
							x_speedxf.xfarray12_dianliu = [formatDate(), dianliu2_mret_th1.mret8, dianliu2_mret_th1.mret9, dianliu2_mret_th1.mret10, dianliu2_mret_th1.mret11]
							x_speedxf.xfarray12_jianxi = [formatDate(), jianxi_mret_th1.mret8, jianxi_mret_th1.mret9, jianxi_mret_th1.mret10, jianxi_mret_th1.mret11]
							x_speedxf.xfarray13_speed = [formatDate(), speed_mret_th1.mret8, speed_mret_th1.mret9, speed_mret_th1.mret10, speed_mret_th1.mret11]
							x_speedxf.xfarray14_dianya = [formatDate(), dianya_mret_th1.mret8, dianya_mret_th1.mret9, dianya_mret_th1.mret10, dianya_mret_th1.mret11]
							x_speedxf.xfarray14_acc = [formatDate(), jiasudu2_mret_th1.mret8, jiasudu2_mret_th1.mret9, jiasudu2_mret_th1.mret10, jiasudu2_mret_th1.mret11]
							x_speedxf.xfarray15_speed = [formatDate(), speed_mret_th1.mret8, speed_mret_th1.mret9, speed_mret_th1.mret10, speed_mret_th1.mret11]

							x_speedxf2.xfarray11_dianzu = [formatDate(), dianzu_mret_th1.mret12, dianzu_mret_th1.mret13, dianzu_mret_th1.mret14, dianzu_mret_th1.mret15]
							x_speedxf2.xfarray12_dianliu = [formatDate(), dianliu2_mret_th1.mret12, dianliu2_mret_th1.mret13, dianliu2_mret_th1.mret14, dianliu2_mret_th1.mret15]
							x_speedxf2.xfarray12_jianxi = [formatDate(), jianxi_mret_th1.mret12, jianxi_mret_th1.mret13, jianxi_mret_th1.mret14, jianxi_mret_th1.mret15]
							x_speedxf2.xfarray13_speed = [formatDate(), speed_mret_th1.mret12, speed_mret_th1.mret13, speed_mret_th1.mret14, speed_mret_th1.mret15]
							x_speedxf2.xfarray14_dianya = [formatDate(), dianya_mret_th1.mret12, dianya_mret_th1.mret13, dianya_mret_th1.mret14, dianya_mret_th1.mret15]
							x_speedxf2.xfarray14_acc = [formatDate(), jiasudu2_mret_th1.mret12, jiasudu2_mret_th1.mret13, jiasudu2_mret_th1.mret14, jiasudu2_mret_th1.mret15]
							x_speedxf2.xfarray15_speed = [formatDate(), speed_mret_th1.mret12, speed_mret_th1.mret13, speed_mret_th1.mret14, speed_mret_th1.mret15]

							x_speedxf3.xfarray11_dianzu = [formatDate(), dianzu_mret_th1.mret24, dianzu_mret_th1.mret25, dianzu_mret_th1.mret26, dianzu_mret_th1.mret27]
							x_speedxf3.xfarray12_dianliu = [formatDate(), dianliu2_mret_th1.mret24, dianliu2_mret_th1.mret25, dianliu2_mret_th1.mret26, dianliu2_mret_th1.mret27]
							x_speedxf3.xfarray12_jianxi = [formatDate(), jianxi_mret_th1.mret24, jianxi_mret_th1.mret25, jianxi_mret_th1.mret26, jianxi_mret_th1.mret27]
							x_speedxf3.xfarray13_speed = [formatDate(), speed_mret_th1.mret24, speed_mret_th1.mret25, speed_mret_th1.mret26, speed_mret_th1.mret27]
							x_speedxf3.xfarray14_dianya = [formatDate(), dianya_mret_th1.mret24, dianya_mret_th1.mret25, dianya_mret_th1.mret26, dianya_mret_th1.mret27]
							x_speedxf3.xfarray14_acc = [formatDate(), jiasudu2_mret_th1.mret24, jiasudu2_mret_th1.mret25, jiasudu2_mret_th1.mret26, jiasudu2_mret_th1.mret27]
							x_speedxf3.xfarray15_speed = [formatDate(), speed_mret_th1.mret24, speed_mret_th1.mret25, speed_mret_th1.mret26, speed_mret_th1.mret27]

							x_speedxf4.xfarray11_dianzu = [formatDate(), dianzu_mret_th1.mret28, dianzu_mret_th1.mret29, dianzu_mret_th1.mret30, dianzu_mret_th1.mret31]
							x_speedxf4.xfarray12_dianliu = [formatDate(), dianliu2_mret_th1.mret28, dianliu2_mret_th1.mret29, dianliu2_mret_th1.mret30, dianliu2_mret_th1.mret31]
							x_speedxf4.xfarray12_jianxi = [formatDate(), jianxi_mret_th1.mret28, jianxi_mret_th1.mret29, jianxi_mret_th1.mret30, jianxi_mret_th1.mret31]
							x_speedxf4.xfarray13_speed = [formatDate(), speed_mret_th1.mret28, speed_mret_th1.mret29, speed_mret_th1.mret30, speed_mret_th1.mret31]
							x_speedxf4.xfarray14_dianya = [formatDate(), dianya_mret_th1.mret28, dianya_mret_th1.mret29, dianya_mret_th1.mret30, dianya_mret_th1.mret31]
							x_speedxf4.xfarray14_acc = [formatDate(), jiasudu2_mret_th1.mret28, jiasudu2_mret_th1.mret29, jiasudu2_mret_th1.mret30, jiasudu2_mret_th1.mret31]
							x_speedxf4.xfarray15_speed = [formatDate(), speed_mret_th1.mret28, speed_mret_th1.mret29, speed_mret_th1.mret30, speed_mret_th1.mret31]
							flag = timeToString(addTime(1))
						}
						break;
				}
			}
			currentTime()
		})
		onUnmounted(() => {
			if (getDate) {
				clearInterval(getDate) // 在Vue实例销毁前，清除时间定时器
			}
		})
		return {
			TimeData,
			x_speedxf,
			x_speedxf2,
			x_speedxf3,
			x_speedxf4,
			base,
			colorSig,
			title,
			logoItems,
			titleProps
		};
	}
}
</script>

<template>
	<svg class="block" width="100%" height="100%" preserveAspectRatio="none" viewBox="0 0 1920 1080" version="1.1"
		xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">

		<defs>
			<linearGradient x1="28.1148014%" y1="99.9994492%" x2="28.1148624%" y2="-15.9417764%" id="linearGradient-1">
				<stop stop-color="#0D98FF" offset="0%"></stop>
				<stop stop-color="#0D98FF" stop-opacity="0" offset="100%"></stop>
			</linearGradient>
			<linearGradient x1="50%" y1="0%" x2="50%" y2="100%" id="linearGradient-2">
				<stop stop-color="#0E74B7" stop-opacity="0.583749624" offset="0%"></stop>
				<stop stop-color="#1896E8" stop-opacity="0.147807515" offset="100%"></stop>
			</linearGradient>
			<linearGradient x1="50%" y1="36.2928152%" x2="50%" y2="100%" id="linearGradient-3">
				<stop stop-color="#09446F" offset="0%"></stop>
				<stop stop-color="#016CAB" offset="100%"></stop>
			</linearGradient>
		</defs>
		<g id="高速磁浮悬浮状态诊断模块" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
			<rect fill="#000000" x="0" y="0" width="1920" height="1080"></rect>
			<g id="编组-6备份-5" transform="translate(24.000000, 102.000000)" fill="#00A1FF" fill-opacity="0.07"
				stroke="#015A90" stroke-width="2">
				<rect id="矩形" x="1" y="1" width="1870" height="228"></rect>
			</g>
			<g id="编组-6备份-4" transform="translate(24.000000, 356.000000)" fill="#00A1FF" fill-opacity="0.07"
				stroke="#015A90" stroke-width="2">
				<rect id="矩形" x="1" y="1" width="1870" height="698"></rect>
			</g>
			<g id="编组-5备份-3" transform="translate(24.000000, 356.000000)">
				<rect id="矩形" fill="#0D98FF" x="0" y="0" width="3" height="38"></rect>
				<rect id="矩形备份-4" fill="url(#linearGradient-1)" opacity="0.37" x="3" y="0" width="1869" height="38">
				</rect>
				<text id="悬浮控制器状态曲线" font-family="PingFangSC-Regular, PingFang SC" font-size="20" font-weight="normal"
					fill="#FFFFFF">
					<tspan x="34" y="26">悬浮控制器状态曲线</tspan>
				</text>
				<g id="编组" transform="translate(1825.146667, 13.000000)" fill="#4EB3FE">
					<polygon id="矩形" opacity="0.220115298"
						points="11.1466667 0 16.2133333 0 26.8533333 13 21.7866667 13">
					</polygon>
					<polygon id="矩形备份" points="-4.60824712e-13 0 5.06666667 0 15.7066667 13 10.64 13"></polygon>
				</g>
				<g id="上箭头"
					transform="translate(22.000000, 19.000000) rotate(-270.000000) translate(-22.000000, -19.000000) translate(16.000000, 13.000000)"
					fill="#FFFFFF" fill-rule="nonzero">
					<rect id="矩形" opacity="0" x="0" y="0" width="12" height="12"></rect>
					<path
						d="M6.7155,3.1875 L10.33425,7.929 C10.5419684,8.2011872 10.5772501,8.56766184 10.4252743,8.874478 C10.2732984,9.18129416 9.96039265,9.37530038 9.618,9.37500035 L2.381625,9.37500035 C2.03936752,9.37500035 1.72672265,9.18089984 1.57493463,8.87414166 C1.42314661,8.56738348 1.45848879,8.20107975 1.666125,7.929 L5.284875,3.1875 C5.45513546,2.9645217 5.71963814,2.83369413 6.0001875,2.83369413 C6.28073686,2.83369413 6.54523954,2.9645217 6.7155,3.1875 Z"
						id="路径"></path>
				</g>
			</g>
			<g id="编组-8备份-10" transform="translate(48.000000, 410.000000)">
				<rect id="矩形" stroke="#00A1FF" opacity="0.500722976" x="0.5" y="0.5" width="437" height="199"></rect>
				<text id="电阻/间隙" class="hidden" font-family="PingFangSC-Regular, PingFang SC" font-size="16"
					font-weight="normal" fill="#FFFFFF">
					<tspan x="9" y="28.3602484">电阻/间隙</tspan>
				</text>
				<g id="编组-8备份-7" class="hidden" transform="translate(9.000000, 45.969403)">
					<line x1="418.507024" y1="118.065169" x2="13.2806697" y2="118.065169" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square"></line>
					<line x1="418.507024" y1="68.2924526" x2="13.2806697" y2="68.2924526" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<line x1="418.507024" y1="10.635419" x2="13.2806697" y2="10.635419" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<text id="0备份" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="118.271667">0</tspan>
					</text>
					<text id="00:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="13.3250883" y="137.905915">00:00</tspan>
					</text>
					<text id="01:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="87.2517079" y="137.905915">01:00</tspan>
					</text>
					<text id="02:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="158.178327" y="137.905915">02:00</tspan>
					</text>
					<text id="03:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="232.104947" y="137.905915">03:00</tspan>
					</text>
					<text id="04:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="306.031567" y="137.905915">04:00</tspan>
					</text>
					<text id="05:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="379.958186" y="137.905915">05:00</tspan>
					</text>
					<text id="1" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="67.2394875">1</tspan>
					</text>
					<text id="2" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="17.4223602">2</tspan>
					</text>
					<path
						d="M13.2600334,60.9586902 C20.1631081,78.3841628 28.5454131,87.0968991 38.4069484,87.0968991 C53.1992514,87.0968991 93.1384693,30.0933584 118.285384,30.0933584 C143.432299,30.0933584 171.006165,73.4716625 195.20536,73.4716625 C219.404554,73.4716625 232.679194,36.7669436 260.291492,36.7669436 C287.903791,36.7669436 295.302952,87.0968991 311.568105,87.0968991 C327.833257,87.0968991 358.61881,46.1746884 380.318102,52.4544251 C394.784297,56.6409162 407.205923,68.1884075 417.58298,87.0968991"
						id="路径-8备份-2" stroke="#FFBF46" stroke-width="2"></path>
				</g>
			</g>
			<g id="编组-8备份-11" transform="translate(510.000000, 410.000000)">
				<rect id="矩形" stroke="#00A1FF" opacity="0.500722976" x="0.5" y="0.5" width="437" height="199"></rect>
				<text id="电阻/间隙" class="hidden" font-family="PingFangSC-Regular, PingFang SC" font-size="16"
					font-weight="normal" fill="#FFFFFF">
					<tspan x="9" y="28.3602484">电阻/间隙</tspan>
				</text>
				<g id="编组-8备份-7" class="hidden" transform="translate(9.000000, 45.969403)">
					<line x1="418.507024" y1="118.065169" x2="13.2806697" y2="118.065169" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square"></line>
					<line x1="418.507024" y1="68.2924526" x2="13.2806697" y2="68.2924526" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<line x1="418.507024" y1="10.635419" x2="13.2806697" y2="10.635419" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<text id="0备份" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="118.271667">0</tspan>
					</text>
					<text id="00:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="13.3250883" y="137.905915">00:00</tspan>
					</text>
					<text id="01:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="87.2517079" y="137.905915">01:00</tspan>
					</text>
					<text id="02:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="158.178327" y="137.905915">02:00</tspan>
					</text>
					<text id="03:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="232.104947" y="137.905915">03:00</tspan>
					</text>
					<text id="04:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="306.031567" y="137.905915">04:00</tspan>
					</text>
					<text id="05:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="379.958186" y="137.905915">05:00</tspan>
					</text>
					<text id="1" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="67.2394875">1</tspan>
					</text>
					<text id="2" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="17.4223602">2</tspan>
					</text>
					<path
						d="M13.2600334,60.9586902 C20.1631081,78.3841628 28.5454131,87.0968991 38.4069484,87.0968991 C53.1992514,87.0968991 93.1384693,30.0933584 118.285384,30.0933584 C143.432299,30.0933584 171.006165,73.4716625 195.20536,73.4716625 C219.404554,73.4716625 232.679194,36.7669436 260.291492,36.7669436 C287.903791,36.7669436 295.302952,87.0968991 311.568105,87.0968991 C327.833257,87.0968991 358.61881,46.1746884 380.318102,52.4544251 C394.784297,56.6409162 407.205923,68.1884075 417.58298,87.0968991"
						id="路径-8备份-2" stroke="#FFBF46" stroke-width="2"></path>
				</g>
			</g>
			<g id="编组-8备份-12" transform="translate(972.000000, 410.000000)">
				<rect id="矩形" stroke="#00A1FF" opacity="0.500722976" x="0.5" y="0.5" width="437" height="199"></rect>
				<text id="电阻/间隙" class="hidden" font-family="PingFangSC-Regular, PingFang SC" font-size="16"
					font-weight="normal" fill="#FFFFFF">
					<tspan x="9" y="28.3602484">电阻/间隙</tspan>
				</text>
				<g id="编组-8备份-7" class="hidden" transform="translate(9.000000, 45.969403)">
					<line x1="418.507024" y1="118.065169" x2="13.2806697" y2="118.065169" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square"></line>
					<line x1="418.507024" y1="68.2924526" x2="13.2806697" y2="68.2924526" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<line x1="418.507024" y1="10.635419" x2="13.2806697" y2="10.635419" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<text id="0备份" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="118.271667">0</tspan>
					</text>
					<text id="00:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="13.3250883" y="137.905915">00:00</tspan>
					</text>
					<text id="01:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="87.2517079" y="137.905915">01:00</tspan>
					</text>
					<text id="02:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="158.178327" y="137.905915">02:00</tspan>
					</text>
					<text id="03:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="232.104947" y="137.905915">03:00</tspan>
					</text>
					<text id="04:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="306.031567" y="137.905915">04:00</tspan>
					</text>
					<text id="05:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="379.958186" y="137.905915">05:00</tspan>
					</text>
					<text id="1" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="67.2394875">1</tspan>
					</text>
					<text id="2" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="17.4223602">2</tspan>
					</text>
					<path
						d="M13.2600334,60.9586902 C20.1631081,78.3841628 28.5454131,87.0968991 38.4069484,87.0968991 C53.1992514,87.0968991 93.1384693,30.0933584 118.285384,30.0933584 C143.432299,30.0933584 171.006165,73.4716625 195.20536,73.4716625 C219.404554,73.4716625 232.679194,36.7669436 260.291492,36.7669436 C287.903791,36.7669436 295.302952,87.0968991 311.568105,87.0968991 C327.833257,87.0968991 358.61881,46.1746884 380.318102,52.4544251 C394.784297,56.6409162 407.205923,68.1884075 417.58298,87.0968991"
						id="路径-8备份-2" stroke="#FFBF46" stroke-width="2"></path>
				</g>
			</g>
			<g id="编组-8备份-13" transform="translate(1434.000000, 410.000000)">
				<rect id="矩形" stroke="#00A1FF" opacity="0.500722976" x="0.5" y="0.5" width="437" height="199"></rect>
				<text id="电阻/间隙" class="hidden" font-family="PingFangSC-Regular, PingFang SC" font-size="16"
					font-weight="normal" fill="#FFFFFF">
					<tspan x="9" y="28.3602484">电阻/间隙</tspan>
				</text>
				<g id="编组-8备份-7" class="hidden" transform="translate(9.000000, 45.969403)">
					<line x1="418.507024" y1="118.065169" x2="13.2806697" y2="118.065169" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square"></line>
					<line x1="418.507024" y1="68.2924526" x2="13.2806697" y2="68.2924526" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<line x1="418.507024" y1="10.635419" x2="13.2806697" y2="10.635419" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<text id="0备份" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="118.271667">0</tspan>
					</text>
					<text id="00:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="13.3250883" y="137.905915">00:00</tspan>
					</text>
					<text id="01:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="87.2517079" y="137.905915">01:00</tspan>
					</text>
					<text id="02:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="158.178327" y="137.905915">02:00</tspan>
					</text>
					<text id="03:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="232.104947" y="137.905915">03:00</tspan>
					</text>
					<text id="04:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="306.031567" y="137.905915">04:00</tspan>
					</text>
					<text id="05:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="379.958186" y="137.905915">05:00</tspan>
					</text>
					<text id="1" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="67.2394875">1</tspan>
					</text>
					<text id="2" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="17.4223602">2</tspan>
					</text>
					<path
						d="M13.2600334,60.9586902 C20.1631081,78.3841628 28.5454131,87.0968991 38.4069484,87.0968991 C53.1992514,87.0968991 93.1384693,30.0933584 118.285384,30.0933584 C143.432299,30.0933584 171.006165,73.4716625 195.20536,73.4716625 C219.404554,73.4716625 232.679194,36.7669436 260.291492,36.7669436 C287.903791,36.7669436 295.302952,87.0968991 311.568105,87.0968991 C327.833257,87.0968991 358.61881,46.1746884 380.318102,52.4544251 C394.784297,56.6409162 407.205923,68.1884075 417.58298,87.0968991"
						id="路径-8备份-2" stroke="#FFBF46" stroke-width="2"></path>
				</g>
			</g>
			<g id="编组-8备份-20" transform="translate(48.000000, 626.000000)">
				<rect id="矩形" stroke="#00A1FF" opacity="0.500722976" x="0.5" y="0.5" width="437" height="199"></rect>
				<text id="电压/电流" class="hidden" font-family="PingFangSC-Regular, PingFang SC" font-size="16"
					font-weight="normal" fill="#FFFFFF">
					<tspan x="9" y="28.3602484">电压/电流</tspan>
				</text>
				<g id="编组-8备份-7" class="hidden" transform="translate(9.000000, 45.969403)">
					<line x1="418.507024" y1="118.065169" x2="13.2806697" y2="118.065169" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square"></line>
					<line x1="418.507024" y1="68.2924526" x2="13.2806697" y2="68.2924526" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<line x1="418.507024" y1="10.635419" x2="13.2806697" y2="10.635419" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<text id="0备份" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="118.271667">0</tspan>
					</text>
					<text id="00:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="13.3250883" y="137.905915">00:00</tspan>
					</text>
					<text id="01:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="87.2517079" y="137.905915">01:00</tspan>
					</text>
					<text id="02:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="158.178327" y="137.905915">02:00</tspan>
					</text>
					<text id="03:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="232.104947" y="137.905915">03:00</tspan>
					</text>
					<text id="04:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="306.031567" y="137.905915">04:00</tspan>
					</text>
					<text id="05:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="379.958186" y="137.905915">05:00</tspan>
					</text>
					<text id="1" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="67.2394875">1</tspan>
					</text>
					<text id="2" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="17.4223602">2</tspan>
					</text>
					<path
						d="M13.2600334,60.9586902 C20.1631081,78.3841628 28.5454131,87.0968991 38.4069484,87.0968991 C53.1992514,87.0968991 93.1384693,30.0933584 118.285384,30.0933584 C143.432299,30.0933584 171.006165,73.4716625 195.20536,73.4716625 C219.404554,73.4716625 232.679194,36.7669436 260.291492,36.7669436 C287.903791,36.7669436 295.302952,87.0968991 311.568105,87.0968991 C327.833257,87.0968991 358.61881,46.1746884 380.318102,52.4544251 C394.784297,56.6409162 407.205923,68.1884075 417.58298,87.0968991"
						id="路径-8备份-2" stroke="#00A1FF" stroke-width="2"></path>
				</g>
			</g>
			<g id="编组-8备份-24" transform="translate(48.000000, 842.000000)">
				<rect id="矩形" stroke="#00A1FF" opacity="0.500722976" x="0.5" y="0.5" width="437" height="199"></rect>
				<text id="速度/加速度" class="hidden" font-family="PingFangSC-Regular, PingFang SC" font-size="16"
					font-weight="normal" fill="#FFFFFF">
					<tspan x="9" y="28.3602484">速度/加速度</tspan>
				</text>
				<g id="编组-8备份-7" class="hidden" transform="translate(9.000000, 45.969403)">
					<line x1="418.507024" y1="118.065169" x2="13.2806697" y2="118.065169" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square"></line>
					<line x1="418.507024" y1="68.2924526" x2="13.2806697" y2="68.2924526" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<line x1="418.507024" y1="10.635419" x2="13.2806697" y2="10.635419" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<text id="0备份" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="118.271667">0</tspan>
					</text>
					<text id="00:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="13.3250883" y="137.905915">00:00</tspan>
					</text>
					<text id="01:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="87.2517079" y="137.905915">01:00</tspan>
					</text>
					<text id="02:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="158.178327" y="137.905915">02:00</tspan>
					</text>
					<text id="03:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="232.104947" y="137.905915">03:00</tspan>
					</text>
					<text id="04:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="306.031567" y="137.905915">04:00</tspan>
					</text>
					<text id="05:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="379.958186" y="137.905915">05:00</tspan>
					</text>
					<text id="1" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="67.2394875">1</tspan>
					</text>
					<text id="2" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="17.4223602">2</tspan>
					</text>
					<path
						d="M13.2600334,60.9586902 C20.1631081,78.3841628 28.5454131,87.0968991 38.4069484,87.0968991 C53.1992514,87.0968991 93.1384693,30.0933584 118.285384,30.0933584 C143.432299,30.0933584 171.006165,73.4716625 195.20536,73.4716625 C219.404554,73.4716625 232.679194,36.7669436 260.291492,36.7669436 C287.903791,36.7669436 295.302952,87.0968991 311.568105,87.0968991 C327.833257,87.0968991 358.61881,46.1746884 380.318102,52.4544251 C394.784297,56.6409162 407.205923,68.1884075 417.58298,87.0968991"
						id="路径-8备份-2" stroke="#00A1FF" stroke-width="2"></path>
				</g>
			</g>
			<g id="编组-8备份-25" transform="translate(510.000000, 842.000000)">
				<rect id="矩形" stroke="#00A1FF" opacity="0.500722976" x="0.5" y="0.5" width="437" height="199"></rect>
				<text id="速度/加速度" class="hidden" font-family="PingFangSC-Regular, PingFang SC" font-size="16"
					font-weight="normal" fill="#FFFFFF">
					<tspan x="9" y="28.3602484">速度/加速度</tspan>
				</text>
				<g id="编组-8备份-7" class="hidden" transform="translate(9.000000, 45.969403)">
					<line x1="418.507024" y1="118.065169" x2="13.2806697" y2="118.065169" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square"></line>
					<line x1="418.507024" y1="68.2924526" x2="13.2806697" y2="68.2924526" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<line x1="418.507024" y1="10.635419" x2="13.2806697" y2="10.635419" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<text id="0备份" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="118.271667">0</tspan>
					</text>
					<text id="00:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="13.3250883" y="137.905915">00:00</tspan>
					</text>
					<text id="01:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="87.2517079" y="137.905915">01:00</tspan>
					</text>
					<text id="02:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="158.178327" y="137.905915">02:00</tspan>
					</text>
					<text id="03:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="232.104947" y="137.905915">03:00</tspan>
					</text>
					<text id="04:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="306.031567" y="137.905915">04:00</tspan>
					</text>
					<text id="05:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="379.958186" y="137.905915">05:00</tspan>
					</text>
					<text id="1" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="67.2394875">1</tspan>
					</text>
					<text id="2" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="17.4223602">2</tspan>
					</text>
					<path
						d="M13.2600334,60.9586902 C20.1631081,78.3841628 28.5454131,87.0968991 38.4069484,87.0968991 C53.1992514,87.0968991 93.1384693,30.0933584 118.285384,30.0933584 C143.432299,30.0933584 171.006165,73.4716625 195.20536,73.4716625 C219.404554,73.4716625 232.679194,36.7669436 260.291492,36.7669436 C287.903791,36.7669436 295.302952,87.0968991 311.568105,87.0968991 C327.833257,87.0968991 358.61881,46.1746884 380.318102,52.4544251 C394.784297,56.6409162 407.205923,68.1884075 417.58298,87.0968991"
						id="路径-8备份-2" stroke="#00A1FF" stroke-width="2"></path>
				</g>
			</g>
			<g id="编组-8备份-26" transform="translate(972.000000, 842.000000)">
				<rect id="矩形" stroke="#00A1FF" opacity="0.500722976" x="0.5" y="0.5" width="437" height="199"></rect>
				<text id="速度/加速度" class="hidden" font-family="PingFangSC-Regular, PingFang SC" font-size="16"
					font-weight="normal" fill="#FFFFFF">
					<tspan x="9" y="28.3602484">速度/加速度</tspan>
				</text>
				<g id="编组-8备份-7" class="hidden" transform="translate(9.000000, 45.969403)">
					<line x1="418.507024" y1="118.065169" x2="13.2806697" y2="118.065169" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square"></line>
					<line x1="418.507024" y1="68.2924526" x2="13.2806697" y2="68.2924526" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<line x1="418.507024" y1="10.635419" x2="13.2806697" y2="10.635419" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<text id="0备份" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="118.271667">0</tspan>
					</text>
					<text id="00:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="13.3250883" y="137.905915">00:00</tspan>
					</text>
					<text id="01:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="87.2517079" y="137.905915">01:00</tspan>
					</text>
					<text id="02:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="158.178327" y="137.905915">02:00</tspan>
					</text>
					<text id="03:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="232.104947" y="137.905915">03:00</tspan>
					</text>
					<text id="04:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="306.031567" y="137.905915">04:00</tspan>
					</text>
					<text id="05:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="379.958186" y="137.905915">05:00</tspan>
					</text>
					<text id="1" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="67.2394875">1</tspan>
					</text>
					<text id="2" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="17.4223602">2</tspan>
					</text>
					<path
						d="M13.2600334,60.9586902 C20.1631081,78.3841628 28.5454131,87.0968991 38.4069484,87.0968991 C53.1992514,87.0968991 93.1384693,30.0933584 118.285384,30.0933584 C143.432299,30.0933584 171.006165,73.4716625 195.20536,73.4716625 C219.404554,73.4716625 232.679194,36.7669436 260.291492,36.7669436 C287.903791,36.7669436 295.302952,87.0968991 311.568105,87.0968991 C327.833257,87.0968991 358.61881,46.1746884 380.318102,52.4544251 C394.784297,56.6409162 407.205923,68.1884075 417.58298,87.0968991"
						id="路径-8备份-2" stroke="#00A1FF" stroke-width="2"></path>
				</g>
			</g>
			<g id="编组-8备份-27" transform="translate(1434.000000, 842.000000)">
				<rect id="矩形" stroke="#00A1FF" opacity="0.500722976" x="0.5" y="0.5" width="437" height="199"></rect>
				<text id="速度/加速度" class="hidden" font-family="PingFangSC-Regular, PingFang SC" font-size="16"
					font-weight="normal" fill="#FFFFFF">
					<tspan x="9" y="28.3602484">速度/加速度</tspan>
				</text>
				<g id="编组-8备份-7" class="hidden" transform="translate(9.000000, 45.969403)">
					<line x1="418.507024" y1="118.065169" x2="13.2806697" y2="118.065169" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square"></line>
					<line x1="418.507024" y1="68.2924526" x2="13.2806697" y2="68.2924526" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<line x1="418.507024" y1="10.635419" x2="13.2806697" y2="10.635419" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<text id="0备份" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="118.271667">0</tspan>
					</text>
					<text id="00:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="13.3250883" y="137.905915">00:00</tspan>
					</text>
					<text id="01:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="87.2517079" y="137.905915">01:00</tspan>
					</text>
					<text id="02:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="158.178327" y="137.905915">02:00</tspan>
					</text>
					<text id="03:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="232.104947" y="137.905915">03:00</tspan>
					</text>
					<text id="04:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="306.031567" y="137.905915">04:00</tspan>
					</text>
					<text id="05:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="379.958186" y="137.905915">05:00</tspan>
					</text>
					<text id="1" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="67.2394875">1</tspan>
					</text>
					<text id="2" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="17.4223602">2</tspan>
					</text>
					<path
						d="M13.2600334,60.9586902 C20.1631081,78.3841628 28.5454131,87.0968991 38.4069484,87.0968991 C53.1992514,87.0968991 93.1384693,30.0933584 118.285384,30.0933584 C143.432299,30.0933584 171.006165,73.4716625 195.20536,73.4716625 C219.404554,73.4716625 232.679194,36.7669436 260.291492,36.7669436 C287.903791,36.7669436 295.302952,87.0968991 311.568105,87.0968991 C327.833257,87.0968991 358.61881,46.1746884 380.318102,52.4544251 C394.784297,56.6409162 407.205923,68.1884075 417.58298,87.0968991"
						id="路径-8备份-2" stroke="#00A1FF" stroke-width="2"></path>
				</g>
			</g>
			<g id="编组-8备份-21" transform="translate(510.000000, 626.000000)">
				<rect id="矩形" stroke="#00A1FF" opacity="0.500722976" x="0.5" y="0.5" width="437" height="199"></rect>
				<text id="电压/电流" class="hidden" font-family="PingFangSC-Regular, PingFang SC" font-size="16"
					font-weight="normal" fill="#FFFFFF">
					<tspan x="9" y="28.3602484">电压/电流</tspan>
				</text>
				<g id="编组-8备份-7" class="hidden" transform="translate(9.000000, 45.969403)">
					<line x1="418.507024" y1="118.065169" x2="13.2806697" y2="118.065169" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square"></line>
					<line x1="418.507024" y1="68.2924526" x2="13.2806697" y2="68.2924526" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<line x1="418.507024" y1="10.635419" x2="13.2806697" y2="10.635419" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<text id="0备份" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="118.271667">0</tspan>
					</text>
					<text id="00:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="13.3250883" y="137.905915">00:00</tspan>
					</text>
					<text id="01:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="87.2517079" y="137.905915">01:00</tspan>
					</text>
					<text id="02:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="158.178327" y="137.905915">02:00</tspan>
					</text>
					<text id="03:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="232.104947" y="137.905915">03:00</tspan>
					</text>
					<text id="04:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="306.031567" y="137.905915">04:00</tspan>
					</text>
					<text id="05:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="379.958186" y="137.905915">05:00</tspan>
					</text>
					<text id="1" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="67.2394875">1</tspan>
					</text>
					<text id="2" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="17.4223602">2</tspan>
					</text>
					<path
						d="M13.2600334,60.9586902 C20.1631081,78.3841628 28.5454131,87.0968991 38.4069484,87.0968991 C53.1992514,87.0968991 93.1384693,30.0933584 118.285384,30.0933584 C143.432299,30.0933584 171.006165,73.4716625 195.20536,73.4716625 C219.404554,73.4716625 232.679194,36.7669436 260.291492,36.7669436 C287.903791,36.7669436 295.302952,87.0968991 311.568105,87.0968991 C327.833257,87.0968991 358.61881,46.1746884 380.318102,52.4544251 C394.784297,56.6409162 407.205923,68.1884075 417.58298,87.0968991"
						id="路径-8备份-2" stroke="#00A1FF" stroke-width="2"></path>
				</g>
			</g>
			<g id="编组-8备份-22" transform="translate(972.000000, 626.000000)">
				<rect id="矩形" stroke="#00A1FF" opacity="0.500722976" x="0.5" y="0.5" width="437" height="199"></rect>
				<text id="电压/电流" class="hidden" font-family="PingFangSC-Regular, PingFang SC" font-size="16"
					font-weight="normal" fill="#FFFFFF">
					<tspan x="9" y="28.3602484">电压/电流</tspan>
				</text>
				<g id="编组-8备份-7" class="hidden" transform="translate(9.000000, 45.969403)">
					<line x1="418.507024" y1="118.065169" x2="13.2806697" y2="118.065169" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square"></line>
					<line x1="418.507024" y1="68.2924526" x2="13.2806697" y2="68.2924526" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<line x1="418.507024" y1="10.635419" x2="13.2806697" y2="10.635419" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<text id="0备份" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="118.271667">0</tspan>
					</text>
					<text id="00:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="13.3250883" y="137.905915">00:00</tspan>
					</text>
					<text id="01:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="87.2517079" y="137.905915">01:00</tspan>
					</text>
					<text id="02:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="158.178327" y="137.905915">02:00</tspan>
					</text>
					<text id="03:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="232.104947" y="137.905915">03:00</tspan>
					</text>
					<text id="04:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="306.031567" y="137.905915">04:00</tspan>
					</text>
					<text id="05:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="379.958186" y="137.905915">05:00</tspan>
					</text>
					<text id="1" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="67.2394875">1</tspan>
					</text>
					<text id="2" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="17.4223602">2</tspan>
					</text>
					<path
						d="M13.2600334,60.9586902 C20.1631081,78.3841628 28.5454131,87.0968991 38.4069484,87.0968991 C53.1992514,87.0968991 93.1384693,30.0933584 118.285384,30.0933584 C143.432299,30.0933584 171.006165,73.4716625 195.20536,73.4716625 C219.404554,73.4716625 232.679194,36.7669436 260.291492,36.7669436 C287.903791,36.7669436 295.302952,87.0968991 311.568105,87.0968991 C327.833257,87.0968991 358.61881,46.1746884 380.318102,52.4544251 C394.784297,56.6409162 407.205923,68.1884075 417.58298,87.0968991"
						id="路径-8备份-2" stroke="#00A1FF" stroke-width="2"></path>
				</g>
			</g>
			<g id="编组-8备份-23" transform="translate(1434.000000, 626.000000)">
				<rect id="矩形" stroke="#00A1FF" opacity="0.500722976" x="0.5" y="0.5" width="437" height="199"></rect>
				<text id="电压/电流" class="hidden" font-family="PingFangSC-Regular, PingFang SC" font-size="16"
					font-weight="normal" fill="#FFFFFF">
					<tspan x="9" y="28.3602484">电压/电流</tspan>
				</text>
				<g id="编组-8备份-7" class="hidden" transform="translate(9.000000, 45.969403)">
					<line x1="418.507024" y1="118.065169" x2="13.2806697" y2="118.065169" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square"></line>
					<line x1="418.507024" y1="68.2924526" x2="13.2806697" y2="68.2924526" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<line x1="418.507024" y1="10.635419" x2="13.2806697" y2="10.635419" id="直线-7备份-5" stroke="#ACCFF1"
						opacity="0.35" stroke-linecap="square" stroke-dasharray="4"></line>
					<text id="0备份" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="118.271667">0</tspan>
					</text>
					<text id="00:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="13.3250883" y="137.905915">00:00</tspan>
					</text>
					<text id="01:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="87.2517079" y="137.905915">01:00</tspan>
					</text>
					<text id="02:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="158.178327" y="137.905915">02:00</tspan>
					</text>
					<text id="03:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="232.104947" y="137.905915">03:00</tspan>
					</text>
					<text id="04:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="306.031567" y="137.905915">04:00</tspan>
					</text>
					<text id="05:00" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="379.958186" y="137.905915">05:00</tspan>
					</text>
					<text id="1" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="67.2394875">1</tspan>
					</text>
					<text id="2" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#749DC0">
						<tspan x="0" y="17.4223602">2</tspan>
					</text>
					<path
						d="M13.2600334,60.9586902 C20.1631081,78.3841628 28.5454131,87.0968991 38.4069484,87.0968991 C53.1992514,87.0968991 93.1384693,30.0933584 118.285384,30.0933584 C143.432299,30.0933584 171.006165,73.4716625 195.20536,73.4716625 C219.404554,73.4716625 232.679194,36.7669436 260.291492,36.7669436 C287.903791,36.7669436 295.302952,87.0968991 311.568105,87.0968991 C327.833257,87.0968991 358.61881,46.1746884 380.318102,52.4544251 C394.784297,56.6409162 407.205923,68.1884075 417.58298,87.0968991"
						id="路径-8备份-2" stroke="#00A1FF" stroke-width="2"></path>
				</g>
			</g>
			<g id="编组-5备份-4" transform="translate(24.000000, 102.000000)">
				<rect id="矩形" fill="#0D98FF" x="0" y="0" width="3" height="38"></rect>
				<rect id="矩形备份-4" fill="url(#linearGradient-1)" opacity="0.37" x="3" y="0" width="1869" height="38">
				</rect>
				<text id="右侧电磁铁模块" font-family="PingFangSC-Regular, PingFang SC" font-size="20" font-weight="normal"
					fill="#FFFFFF">
					<tspan x="34" y="26">右侧电磁铁模块</tspan>
				</text>
				<g id="编组" transform="translate(1825.146667, 13.000000)" fill="#4EB3FE">
					<polygon id="矩形" opacity="0.220115298"
						points="11.1466667 0 16.2133333 0 26.8533333 13 21.7866667 13">
					</polygon>
					<polygon id="矩形备份" points="-4.60824712e-13 0 5.06666667 0 15.7066667 13 10.64 13"></polygon>
				</g>
				<g id="上箭头"
					transform="translate(22.000000, 20.000000) rotate(-270.000000) translate(-22.000000, -20.000000) translate(16.000000, 14.000000)"
					fill="#FFFFFF" fill-rule="nonzero">
					<rect id="矩形" opacity="0" x="0" y="0" width="12" height="12"></rect>
					<path
						d="M6.7155,3.1875 L10.33425,7.929 C10.5419684,8.2011872 10.5772501,8.56766184 10.4252743,8.874478 C10.2732984,9.18129416 9.96039265,9.37530038 9.618,9.37500035 L2.381625,9.37500035 C2.03936752,9.37500035 1.72672265,9.18089984 1.57493463,8.87414166 C1.42314661,8.56738348 1.45848879,8.20107975 1.666125,7.929 L5.284875,3.1875 C5.45513546,2.9645217 5.71963814,2.83369413 6.0001875,2.83369413 C6.28073686,2.83369413 6.54523954,2.9645217 6.7155,3.1875 Z"
						id="路径"></path>
				</g>
			</g>
			<g id="编组-6" transform="translate(26.000000, 170.000000)">
				<rect id="矩形" fill-opacity="0.154217" fill="#0DD6FF" x="0" y="17.0984456" width="1816"
					height="97.119171">
				</rect>
				<g id="编组-4">
					<g id="编组-5" fill="#077088">
						<rect id="矩形" x="0" y="0" width="133" height="35.3385827"></rect>
					</g>
					<g id="编组-5备份-5" transform="translate(0.000000, 96.661417)" fill="#077088">
						<rect id="矩形" x="0" y="0" width="133" height="35.3385827"></rect>
					</g>
					<g id="编组-5备份" transform="translate(340.000000, 0.000000)">
						<rect id="矩形" fill="#077088" x="0" y="0" width="266" height="35.3385827"></rect>
						<line x1="133" y1="0" x2="133" y2="35.3385827" id="直线-4" stroke-opacity="0.497824929"
							stroke="#FFFFFF" stroke-width="2"></line>
					</g>
					<g id="编组-5备份-2" transform="translate(801.000000, 0.000000)">
						<rect id="矩形" fill="#077088" x="0" y="0" width="266" height="35.3385827"></rect>
						<line x1="133" y1="0" x2="133" y2="35.3385827" id="直线-4" stroke-opacity="0.503863035"
							stroke="#FFFFFF" stroke-width="2"></line>
					</g>
					<g id="编组-5备份-10" transform="translate(1262.000000, 0.000000)">
						<rect id="矩形" fill="#077088" x="0" y="0" width="266" height="35.3385827"></rect>
						<line x1="133" y1="0" x2="133" y2="35.3385827" id="直线-4" stroke-opacity="0.5" stroke="#FFFFFF"
							stroke-width="2"></line>
					</g>
					<g id="编组-5备份-11" transform="translate(1683.000000, 0.000000)" fill="#077088">
						<rect id="矩形" x="0" y="0" width="133" height="35.3385827"></rect>
					</g>
					<g id="编组-5备份-12" transform="translate(1683.000000, 96.661417)" fill="#077088">
						<rect id="矩形" x="0" y="0" width="133" height="35.3385827"></rect>
					</g>
					<g id="编组-5备份-7" transform="translate(340.000000, 96.661417)">
						<rect id="矩形" fill="#077088" x="0" y="0" width="266" height="35.3385827"></rect>
						<line x1="133" y1="0" x2="133" y2="35.3385827" id="直线-4" stroke-opacity="0.49801529"
							stroke="#FFFFFF" stroke-width="2"></line>
					</g>
					<g id="编组-5备份-8" transform="translate(801.000000, 96.661417)">
						<rect id="矩形" fill="#077088" x="0" y="0" width="266" height="35.3385827"></rect>
						<line x1="133" y1="0" x2="133" y2="35.3385827" id="直线-4" stroke-opacity="0.5" stroke="#FFFFFF"
							stroke-width="2"></line>
					</g>
					<g id="编组-5备份-9" transform="translate(1262.000000, 96.661417)">
						<rect id="矩形" fill="#077088" x="0" y="0" width="266" height="35.3385827"></rect>
						<line x1="133" y1="0" x2="133" y2="35.3385827" id="直线-4" stroke-opacity="0.5" stroke="#FFFFFF"
							stroke-width="2"></line>
					</g>
					<text id="T8R" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="52" y="51.5142857">T8R</tspan>
					</text>
					<text id="T9R" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="395" y="51.5142857">T9R</tspan>
					</text>
					<text id="T10R" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="525" y="51.5142857">T10R</tspan>
					</text>
					<text id="T11R" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="853" y="51.5142857">T11R</tspan>
					</text>
					<text id="T12R" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="986" y="51.5142857">T12R</tspan>
					</text>
					<text id="T13R" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="1314" y="51.5142857">T13R</tspan>
					</text>
					<text id="T14R" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="1448" y="51.5142857">T14R</tspan>
					</text>
					<text id="T15R" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="1741" y="51.5142857">T15R</tspan>
					</text>
					<text id="T8L" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="52" y="89.8571429">T8L</tspan>
					</text>
					<text id="T1L" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="395" y="89.8571429">T1L</tspan>
					</text>
					<text id="T10L" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="525" y="89.8571429">T10L</tspan>
					</text>
					<text id="T11L" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="853" y="89.8571429">T11L</tspan>
					</text>
					<text id="T12L" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="986" y="89.8571429">T12L</tspan>
					</text>
					<text id="T13L" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="1314" y="89.8571429">T13L</tspan>
					</text>
					<text id="T14L" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="1448" y="89.8571429">T14L</tspan>
					</text>
					<text id="T15L" font-family="PingFangSC-Regular, PingFang SC" font-size="14" font-weight="normal"
						fill="#FFFFFF">
						<tspan x="1741" y="89.8571429">T15L</tspan>
					</text>
				</g>
				<text id="二-位-端" font-family="PingFangSC-Regular, PingFang SC" font-size="16" font-weight="normal"
					fill="#FFFFFF">
					<tspan x="1832" y="45.2372846">二</tspan>
					<tspan x="1832" y="72.2372846">位</tspan>
					<tspan x="1832" y="99.2372846">端</tspan>
				</text>
			</g>
			<g id="编组-4备份-8">
				<g id="编组-3">
					<g id="编组-20">
						<rect id="矩形备份-2" fill="url(#linearGradient-2)" x="0" y="0" width="1920" height="59"></rect>
						<polyline id="路径备份" fill="url(#linearGradient-3)"
							points="1303.50685 0 1240.76712 78 678.739726 78 616 0"></polyline>
						<g id="编组" transform="translate(591.000000, 52.000000)" fill="#4EB3FE">
							<polygon id="矩形" points="44 0 54 0 75 26 65 26"></polygon>
							<polygon id="矩形备份" opacity="0.597190494" points="22 0 32 0 53 26 43 26"></polygon>
							<polygon id="矩形备份-3" opacity="0.310084025" points="-9.09522457e-13 0 10 0 31 26 21 26">
							</polygon>
						</g>
						<g id="编组备份"
							transform="translate(1295.500000, 65.000000) scale(-1, 1) translate(-1295.500000, -65.000000) translate(1258.000000, 52.000000)"
							fill="#4EB3FE">
							<polygon id="矩形" points="44 0 54 0 75 26 65 26"></polygon>
							<polygon id="矩形备份" opacity="0.597190494" points="22 0 32 0 53 26 43 26"></polygon>
							<polygon id="矩形备份-3" opacity="0.310084025" points="-9.09522457e-13 0 10 0 31 26 21 26">
							</polygon>
						</g>
					</g>
					<!-- 时间模块 -->
					<text fill="#ffffff" font-family="SimHei" font-size="40" font-weight="400" height="56"
						letter-spacing="1.81818182" width="544" :text-anchor="titleProps.anchor">
						<tspan :x="titleProps.x" y="55">{{ title }}</tspan>
					</text>
				</g>
				<text fill="#ffffff" font-family="SimHei" font-size="22">
					<tspan x="1648" y="36">{{ TimeData.nowTime }}</tspan>
				</text>
				<text id="车号：CF002" font-family="PingFangSC-Regular, PingFang SC" font-size="22" font-weight="normal"
					fill="#FFFFFF">
					<tspan x="202" y="39">车号：CF002</tspan>
				</text>
				<text id="车厢：MC1" font-family="PingFangSC-Regular, PingFang SC" font-size="22" font-weight="normal"
					fill="#FFFFFF">
					<tspan x="372" y="39">车厢：MC2</tspan>
				</text>
				<g id="caret-right" class="hidden" transform="translate(344.000000, 25.000000)" fill="#FFFFFF"
					fill-rule="nonzero">
					<rect id="矩形" opacity="0" x="0" y="0" width="16" height="16"></rect>
					<path
						d="M11.184375,7.7109375 L5.234375,2.5796875 C5.0125,2.3890625 4.6875,2.5609375 4.6875,2.86875 L4.6875,13.13125 C4.6875,13.4390625 5.0125,13.6109375 5.234375,13.4203125 L11.184375,8.2890625 C11.3546875,8.1421875 11.3546875,7.8578125 11.184375,7.7109375 Z"
						id="路径"></path>
				</g>
				<g id="caret-right备份" class="hidden" transform="translate(495.000000, 23.000000)" fill="#FFFFFF"
					fill-rule="nonzero">
					<rect id="矩形" opacity="0" x="0" y="0" width="16" height="16"></rect>
					<path
						d="M11.184375,7.7109375 L5.234375,2.5796875 C5.0125,2.3890625 4.6875,2.5609375 4.6875,2.86875 L4.6875,13.13125 C4.6875,13.4390625 5.0125,13.6109375 5.234375,13.4203125 L11.184375,8.2890625 C11.3546875,8.1421875 11.3546875,7.8578125 11.184375,7.7109375 Z"
						id="路径"></path>
				</g>
				<!-- logo 图标（可配置，支持一行多个，默认左上角原位置） -->
				<image v-for="(logo, index) in logoItems" :key="index" :height="logo.height" :width="logo.width"
					:x="logo.x" :y="logo.y" :xlink:href="logo.src" />

				<g id="caret-right备份-2" class="hidden" transform="translate(1881.000000, 23.000000)" fill="#FFFFFF"
					fill-rule="nonzero">
					<rect id="矩形" opacity="0" x="0" y="0" width="16" height="16"></rect>
					<path
						d="M11.184375,7.7109375 L5.234375,2.5796875 C5.0125,2.3890625 4.6875,2.5609375 4.6875,2.86875 L4.6875,13.13125 C4.6875,13.4390625 5.0125,13.6109375 5.234375,13.4203125 L11.184375,8.2890625 C11.3546875,8.1421875 11.3546875,7.8578125 11.184375,7.7109375 Z"
						id="路径"></path>
				</g>
			</g>
		</g>
		<foreignObject width="100%" height="100%">
			<div class="SpeedStyle0">
				<Speed1xf5 :dianzu="x_speedxf.xfarray11_dianzu" :jianxi="x_speedxf.xfarray12_jianxi" />
			</div>
			<div class="SpeedStyle1">
				<Speed1xf6 :dianzu="x_speedxf2.xfarray11_dianzu" :jianxi="x_speedxf2.xfarray12_jianxi" />
			</div>
			<div class="SpeedStyle2">
				<Speed1xf7 :dianzu="x_speedxf3.xfarray11_dianzu" :jianxi="x_speedxf3.xfarray12_jianxi" />
			</div>
			<div class="SpeedStyle3">
				<Speed1xf8 :dianzu="x_speedxf4.xfarray11_dianzu" :jianxi="x_speedxf4.xfarray12_jianxi" />
			</div>
			<div class="SpeedStyle11">
				<Speed2xf5 :dianya="x_speedxf.xfarray14_dianya" :dianliu="x_speedxf.xfarray12_dianliu" />
			</div>
			<div class="SpeedStyle12">
				<Speed2xf6 :dianya="x_speedxf2.xfarray14_dianya" :dianliu="x_speedxf2.xfarray12_dianliu" />
			</div>
			<div class="SpeedStyle13">
				<Speed2xf7 :dianya="x_speedxf3.xfarray14_dianya" :dianliu="x_speedxf3.xfarray12_dianliu" />
			</div>
			<div class="SpeedStyle14">
				<Speed2xf8 :dianya="x_speedxf4.xfarray14_dianya" :dianliu="x_speedxf4.xfarray12_dianliu" />
			</div>
			<div class="SpeedStyle21">
				<Speed3xf5 :speed="x_speedxf.xfarray13_speed" :acc="x_speedxf.xfarray14_acc" />
			</div>
			<div class="SpeedStyle22">
				<Speed3xf6 :speed="x_speedxf2.xfarray13_speed" :acc="x_speedxf2.xfarray14_acc" />
			</div>
			<div class="SpeedStyle23">
				<Speed3xf7 :speed="x_speedxf3.xfarray13_speed" :acc="x_speedxf3.xfarray14_acc" />
			</div>
			<div class="SpeedStyle24">
				<Speed3xf8 :speed="x_speedxf4.xfarray13_speed" :acc="x_speedxf4.xfarray14_acc" />
			</div>
		</foreignObject>
	</svg>
</template>

<style scoped>
.SpeedStyle0 {
	position: absolute;
	top: 416px;
	left: 50px;
}

.SpeedStyle1 {
	position: absolute;
	top: 416px;
	left: 510px;
}

.SpeedStyle2 {
	position: absolute;
	top: 416px;
	left: 972px;
}

.SpeedStyle3 {
	position: absolute;
	top: 416px;
	left: 1434px;
}

.SpeedStyle11 {
	position: absolute;
	top: 632px;
	left: 50px;
}

.SpeedStyle12 {
	position: absolute;
	top: 632px;
	left: 510px;
}

.SpeedStyle13 {
	position: absolute;
	top: 632px;
	left: 972px;
}

.SpeedStyle14 {
	position: absolute;
	top: 632px;
	left: 1434px;
}

.SpeedStyle21 {
	position: absolute;
	top: 848px;
	left: 50px;
}

.SpeedStyle22 {
	position: absolute;
	top: 848px;
	left: 510px;
}

.SpeedStyle23 {
	position: absolute;
	top: 848px;
	left: 972px;
}

.SpeedStyle24 {
	position: absolute;
	top: 848px;
	left: 1434px;
}
</style>
