<script>
import feather from 'feather-icons';
// import Button from './reusable/Button.vue';
import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'
export default {
	props: ['showModal', 'modal', 'categories'],
	components: { 
		// Button ,
		VueDatePicker
	},
	data() {
		return {
			stop: {
				type: 1,
				depart_after: 0,
				date: null,
				time: null,
			}
		};
	},
	mounted() {
		feather.replace();
	},
	updated() {
		feather.replace();
	},
	methods: {
		change(type){
			this.stop.type = type;
		},
		setStopData(){
			this.$emit('setStopData', this.stop);
			this.stop.type = 1;
			this.stop.depart_after = 0;
			this.stop.date = null;
			this.stop.time = null;
		},
	},
};
</script>

<template>
	<transition name="fade">
		<div v-show="modal" class="font-general-regular fixed inset-0 z-30">
			<!-- Modal body background as backdrop -->
			<div
				v-show="modal"
				@click="showModal()"
				class="bg-filter bg-black bg-opacity-50 fixed inset-0 w-full h-full z-20"
			></div>
			<!-- Modal content -->
			<main
				class="flex flex-col items-center justify-center h-full w-full"
			>
				<transition name="fade-up-down">
					<div
						v-show="modal"
						class="modal-wrapper flex items-center z-30"
					>
						<div
							class="modal max-w-md mx-5 xl:max-w-xl lg:max-w-xl md:max-w-xl bg-secondary-light dark:bg-primary-dark max-h-screen shadow-lg flex-row rounded-lg relative"
						>
							<div
								class="modal-header flex justify-between gap-10 p-5 border-b border-ternary-light dark:border-ternary-dark"
							>
								<h5
									class="text-[#006f9c] text-3xl font-bold"
								>
								When would you like to depart?
								</h5>
								<button
									class="px-4 text-primary-dark dark:text-primary-light"
									@click="showModal()"
								>
									<i data-feather="x"></i>
								</button>
							</div>
							<div class="modal-body p-5 w-full h-full">
								<p class=" text-left px-4 mb-5">For a pick-up or drop-off the bus will stop for 1 to 15 minutes depending on your group size and leave as soon as possible.</p>
								<!-- <form class="max-w-xl m-4 text-left"> -->
									<div class="mt-0">
										<label class="font-bold w-full ml-6 flex">Select to depart after:</label>
										<div class="flex items-center">
											<input type="radio" v-model="stop.type" value="1" name="bordered-radio" class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
											<select v-model="stop.depart_after" @change="change(1)" class="select__inner ml-3 mt-2 rounded-lg flex-1">
												<option value="0">As soon as possible</option>
												<option value="30">Within 30 minutes</option>
												<option value="45">Within 45 minutes</option>
												<option value="60">Within 1 hour</option>
												<option value="90">Within 1.5 hour</option>
												<option value="120">Within 2 hour</option>
												<option value="150">Within 2.5 hour</option>
												<option value="180">Within 3 hour</option>
											</select>
										</div>
									</div>
									<div class="mt-6">
										<label class="font-bold w-full ml-6 flex">Or select departure date and time</label>
										<div class="flex items-center mt-2">
											<input type="radio" v-model="stop.type" value="2" name="bordered-radio" class="w-4 h-4 mr-3 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
											<VueDatePicker 
												v-model="stop.date" 
												:enable-time-picker="false" 
												six-weeks 
												:placeholder="'dd-mm-yyyy'"
												auto-apply="true"
												:format="'dd-MM-yyyy'"
												class=" rounded-lg"
											/>
											<input type="time" v-model="stop.time" class="bg-gray-50 ml-3 border flex-1 border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Time" required>
										</div>
									</div>

									<div class="mt-6 pb-4 sm:pb-1">
										<button @click="setStopData()" class="w-full flex text-white bg-[#f99d0b] px-5 py-3 rounded">
											<span class="flex-1 text-right">Done</span>
											<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 flex-1 text-right">
												<path stroke-linecap="round" stroke-linejoin="round" d="M13.5 4.5L21 12m0 0l-7.5 7.5M21 12H3" />
											</svg>
										</button>
									</div>
								<!-- </form> -->
							</div>
						</div>
					</div>
				</transition>
			</main>
		</div>
	</transition>
</template>

<style scoped>
.modal-body {
	max-height: 500px;
}
.bg-gray-800-opacity {
	background-color: #2d374850;
}
@media screen and (max-width: 768px) {
	.modal-body {
		max-height: 400px;
	}
}
.fade-up-down-enter-active {
	transition: all 0.3s ease;
}
.fade-up-down-leave-active {
	transition: all 0.3s ease;
}
.fade-up-down-enter {
	transform: translateY(10%);
	opacity: 0;
}
.fade-up-down-leave-to {
	transform: translateY(10%);
	opacity: 0;
}

.fade-enter-active {
	-webkit-transition: opacity 2s;
	transition: opacity 0.3s;
}
.fade-leave-active {
	transition: opacity 0.3s;
}

.fade-enter,
.fade-leave-to {
	opacity: 0;
}
</style>
