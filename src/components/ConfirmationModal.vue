<script>
import feather from 'feather-icons';
// import Button from './reusable/Button.vue';
import '@vuepic/vue-datepicker/dist/main.css'
export default {
	props: ['showConfirmModal', 'confirmModal', 'bookingData'],
	components: { 
		// Button ,
	},
	data() {
		return {
		};
	},
	mounted() {
		feather.replace();
	},
	updated() {
		feather.replace();
	},
	methods: {
	},
};
</script>

<template>
	<transition name="fade">
		<div v-show="confirmModal" class="font-general-regular fixed inset-0 z-30">
			<!-- Modal body background as backdrop -->
			<div
				v-show="confirmModal"
				@click="showConfirmModal()"
				class="bg-filter bg-black bg-opacity-50 fixed inset-0 w-full h-full z-20"
			></div>
			<!-- Modal content -->
			<main
				class="flex flex-col items-center justify-center h-full w-full"
			>
				<transition name="fade-up-down">
					<div
						v-show="confirmModal"
						class="modal-wrapper flex z-30"
					>
						<div
							class="modal mx-5 bg-secondary-light dark:bg-primary-dark max-h-screen shadow-lg flex-row rounded-lg relative"
						>
							<div
								class="modal-header flex text-right justify-between gap-10 p-5 border-b border-ternary-light dark:border-ternary-dark"
							>
								<label></label>
								<button
									class="px-4 text-primary-dark dark:text-primary-light"
									@click="showConfirmModal()"
								>
									<i data-feather="x"></i>
								</button>
							</div>
							<div class="modal-body  overflow-y-scroll w-full h-full">
								<div class="flex">
									<div class="block px-6 bg-[#F5F5F5]">
										<h5 class="text-[#006f9c] text-xl font-bold my-5">
											Your itinerary
										</h5>

										<table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
											<thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
											</thead>
											<tbody>
												<tr class="dark:bg-gray-800 dark:border-gray-700">
													<th scope="row" class="font-bold text-md">
														{{ bookingData.departure_date }}
													</th>
													<td class="px-6 py-4">
														Passengers: {{ bookingData.passengers }}
													</td>
												</tr>
												<tr class="">
													<th scope="row" class=" font-light">
														Departure time:
														<p class=" font-bold">{{ bookingData.departure_time }}</p>
													</th>
													<td class="px-6 py-4">
														<div class="flex">
															<div>
																<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
																	<path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 11-6 0 3 3 0 016 0z" />
																	<path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1115 0z" />
																</svg>
															</div>
															<div class="text-left pl-3">
																<p>From:</p>
																<p>{{ bookingData.departure_address }}</p>
															</div>
														</div>
													</td>
												</tr>
												<tr v-for="(stop, index) in bookingData.stops" class="dark:bg-gray-800" :key="index">
													<th class="text-light font-100">
														{{ stop.depart_after }}
													</th>
													<td class="px-6 py-4">
														<div class="flex">
															<div>
																<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
																	<path stroke-linecap="round" stroke-linejoin="round" d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
																	<path stroke-linecap="round" stroke-linejoin="round" d="M9 9.563C9 9.252 9.252 9 9.563 9h4.874c.311 0 .563.252.563.563v4.874c0 .311-.252.563-.563.563H9.564A.562.562 0 019 14.437V9.564z" />
																</svg>
															</div>
															<div class="text-left pl-3">
																<p>Via:</p>
																<p>{{ stop.address }}</p>
															</div>
														</div>
													</td>
												</tr>
												<tr>
													<th></th>
													<td class="px-6 py-4">
														<div class="flex">
															<div>
																<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
																	<path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 11-6 0 3 3 0 016 0z" />
																	<path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1115 0z" />
																</svg>
															</div>
															<div class="text-left pl-3">
																<p>To:</p>
																<p>{{ bookingData.return_address }}</p>
															</div>
														</div>
													</td>
												</tr>


												<tr class="dark:bg-gray-800 dark:border-gray-700">
													<th scope="row" class="font-bold text-md">
														{{ bookingData.return_date }}
													</th>
													<td class="px-6 py-4">
														Passengers: {{ bookingData.passengers }}
													</td>
												</tr>
												<tr class="">
													<th scope="row" class=" font-light">
														Departure time:
														<p class=" font-bold">{{ bookingData.return_time }}</p>
													</th>
													<td class="px-6 py-4">
														<div class="flex">
															<div>
																<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
																	<path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 11-6 0 3 3 0 016 0z" />
																	<path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1115 0z" />
																</svg>
															</div>
															<div class="text-left pl-3">
																<p>From:</p>
																<p>{{ bookingData.return_address }}</p>
															</div>
														</div>
													</td>
												</tr>
												
												<tr v-for="(stop, index) in bookingData.stops" class="dark:bg-gray-800" :key="index">
													<th class="text-light font-100">
														{{ stop.depart_after }}
													</th>
													<td class="px-6 py-4">
														<div class="flex">
															<div>
																<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
																	<path stroke-linecap="round" stroke-linejoin="round" d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
																	<path stroke-linecap="round" stroke-linejoin="round" d="M9 9.563C9 9.252 9.252 9 9.563 9h4.874c.311 0 .563.252.563.563v4.874c0 .311-.252.563-.563.563H9.564A.562.562 0 019 14.437V9.564z" />
																</svg>
															</div>
															<div class="text-left pl-3">
																<p>Via:</p>
																<p>{{ stop.address }}</p>
															</div>
														</div>
													</td>
												</tr>
												
												<tr>
													<th></th>
													<td class="px-6 py-4">
														<div class="flex">
															<div>
																<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
																	<path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 11-6 0 3 3 0 016 0z" />
																	<path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1115 0z" />
																</svg>
															</div>
															<div class="text-left pl-3">
																<p>To:</p>
																<p>{{ bookingData.departure_address }}</p>
															</div>
														</div>
													</td>
												</tr>

											</tbody>
										</table>
										
									</div>
									<div class="p-6 flex-1 lg:min-w-md text-left">
										<h5
											class="text-[#006f9c] text-3xl font-bold"
										>
										Receive a free quote for your bus trip
										</h5>
										<p class="my-3">We will send the price quote for a modern bus with driver to your e-mail address. Requesting quotes is always free and you can choose to book now when you want.</p>
										<div class="mb-3">
											<label for="first_name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">First Name</label>
											<input type="text" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="First Name" required>
										</div>
										<div class="mb-3">
											<label for="last_name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Last Name</label>
											<input type="text" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Last Name" required>
										</div>
										<div class="mb-3">
											<label for="last_name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Email</label>
											<input type="email" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="your Email" required>
										</div>
										<div class="mb-3">
											<label for="last_name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Additional description and/or specific requests for your trip</label>
											<textarea id="message" rows="4" class="block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Tell us about your trip. For example, do you need the bus on location, do you have a lot of luggage with you or have any other specific wishes."></textarea>
										</div>
										<button class="flex text-white bg-[#f99d0b] px-5 py-3 rounded">
											<span class="flex-1 text-right">Receive quote by email</span>
										</button>
									</div>
								</div>
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
