<template>
  <u-i-stepper
		:steps="steps"
		:step="currentStep"
		@step="catchStep"
	/>
	<div class="buttons">
		<button
			:disabled="isFirstStep()"
			@click="setStep(-1)"
		>
			Prev
		</button>
		<button
			:disabled="isLastStep()"
			@click="setStep(1)"
		>
			Next
		</button>
	</div>
</template>

<script>
import UIStepper from "@/components/UIStepper.vue";

export default {
  name: 'App',
  components: {
		UIStepper,
  },
	data() {
		return {
			currentStep: 0,
			steps: [
				{
					title: "Cart content",
				},
				{
					title: "Delivery address",
				},
				{
					title: "Invoice address",
				},
				{
					title: "Shipping method",
				},
				{
					title: "Payment method",
				},
				{
					title: "Promotion code",
				},
				{
					title: "Review",
				},
				{
					title: "Send command",
				},
			]
		}
	},
	methods: {
		/**
		 * Increase or decrease current step
		 * @param {Number} step
		 */
		setStep(step) {
			this.catchStep(this.currentStep + step);
		},
		/**
		 * Check if we are in the firt step
		 * @return {Boolean}
		 */
		isFirstStep() {
			return this.currentStep === 0;
		},
		/**
		 * Check if we are in the last step
		 * @return {Boolean}
		 */
		isLastStep() {
			return this.currentStep === this.steps.length - 1;
		},
		/**
		 * Dummy method to validate some steps
		 * @param {Number} step
		 */
		catchStep(step) {
			this.currentStep = step;

			// dummy test step validation
			if (step === 3) {
				this.steps[step - 1].error = true;
			} else if (step === 5) {
				this.steps[step - 1].warning = true;
			}
		}
	}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.buttons {
	margin-top: 90px;
}

.buttons button {
	margin: 5px;
}
</style>
