<template>
	<div class="stepper">
		<div
			v-for="(step, index) of steps"
			:key="index"
			:class="{
				'active': currentStep === index,
				'passed': currentStep > index,
				'error': step.error,
				'warning': step.warning,
			}"
		>
			<div class="bullet">
				<span />
				<span @click="clickStep(index)">
					{{ index + 1 }}
				</span>
				<span />
			</div>
			<label @click="clickStep(index)">
				{{ step.title }}
			</label>
		</div>
	</div>
</template>

<script>
export default {
	name: "UIStepper",
	props: {
		steps: {
			type: Array,
			default: () => []
		},
		step: {
			type: Number,
			default: 0
		}
	},
	watch: {
		step() {
			this.currentStep = this.step;
		}
	},
	data() {
		return {
			currentStep: 0,
		};
	},
	mounted() {
		this.currentStep = this.step;
	},
	methods: {
		/**
		 * Emitting selected step
		 * @param {Number} step
		 */
		clickStep(step) {
			this.$emit("step", step);
		}
	}
};

</script>
<style scoped>
.stepper {
	display: flex;
	flex-direction: row;
	align-items: flex-start;
	justify-content: center;
	border: solid 1px #DCDFE6;
	padding: 20px;
	font-size: 14px;
	height: 100%;
	overflow: auto;
}

.stepper > div {
	align-items: center;
	display: flex;
	flex-direction: column;
}

.stepper .bullet {
	display: flex;
	flex-direction: row;
	width: 100%;
	min-width: 50px;
	align-items: center;
}

.stepper .bullet span:nth-child(1) {
	flex-grow: 1;
	height: 0;
	font-size: 0;
	border-top: solid 1px #DCDFE6;
}

.stepper div:first-child .bullet span:nth-child(1),
.stepper div:last-child .bullet span:nth-child(3) {
	border: none;
}

.stepper .bullet span:nth-child(2) {
	width: 25px;
	height: 20px;
	border-radius: 35px;
	border: solid 4px #DCDFE6;
	cursor: pointer;
	color: #A2A2A2;
	padding-top: 5px;
}

.stepper .bullet span:nth-child(3) {
	flex-grow: 1;
	height: 0;
	font-size: 0;
	border-top: solid 1px #DCDFE6;
}

.stepper label {
	padding: 0 15px 0 15px;
	text-align: center;
	cursor: pointer;
}

.stepper .active .bullet span:nth-child(2) {
	background-color: #5189c9;
	color: #fff;
}

.stepper .active label {
	color: #5189c9;
}

.stepper .passed .bullet span:nth-child(2) {
	background-color: #eaeaee;
}

.stepper .passed label {
	color: #A2A2A2;
}

.stepper .error .bullet span:nth-child(2) {
	background-color: #ff5151;
	color: #fff;
}

.stepper .error label {
	color: #ff5151 !important;
}

.stepper .warning .bullet span:nth-child(2) {
	background-color: #e5ac61;
	color: #fff;
}

.stepper .warning label {
	color: #e5ac61 !important;
}

@media screen and (max-width: 800px) {
	.stepper {
		zoom: 80%;
	}
}

@media screen and (max-width: 600px) {
	.stepper label {
		display: none;
	}
}
</style>