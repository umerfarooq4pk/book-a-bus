<script>
import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'
import StopModal from './StopModal.vue';
import ConfirmationModal from './ConfirmationModal.vue';

export default {
    components: { 
        VueDatePicker,
        StopModal,
        ConfirmationModal,
    },
    name: 'Home',
    data() {
        return {
            modal: false,
            confirmModal: false,
            isOpen: false,
            booking: {
                type: null,
                departure_address: null,
                departure_date: null,
                departure_time: null,
                return_address: null,
                return_date: null,
                return_time: null,
                passengers: null,
                outbound_trip: true,
                stops: []
            },
            stops_options: [
                { id: 0, text: "As soon as possible" },
                { id: 30, text: "Within 30 minutes" },
                { id: 45, text: "Within 45 minutes" },
                { id: 60, text: "Within 1 hour" },
                { id: 90, text: "Within 1.5 hour" },
                { id: 120, text: "Within 2 hour" },
                { id: 150, text: "Within 2.5 hour" },
                { id: 180, text: "Within 3 hour" },
            ],
            stop: null,
            currentIndex: null,
        }
    },
	methods: {
        addStop(){
            this.booking.stops.push({
                address: '',
                depart_after: "As soon as possible",
                depart_date: null,
                depart_time: null,
            });
            console.log("stops", this.booking.stops);
        },

        opnModal(index){
            this.currentIndex = index;
            this.showModal();
        },
        
		showModal() {
			if (this.modal) {
				// Stop screen scrolling
				document
					.getElementsByTagName('html')[0]
					.classList.remove('overflow-y-hidden');
				this.modal = false;
			} else {
				document
					.getElementsByTagName('html')[0]
					.classList.add('overflow-y-hidden');
				this.modal = true;
			}
		},
        showConfirmModal(){
            if (this.confirmModal) {
				// Stop screen scrolling
				document
					.getElementsByTagName('html')[0]
					.classList.remove('overflow-y-hidden');
				this.confirmModal = false;
			} else {
				document
					.getElementsByTagName('html')[0]
					.classList.add('overflow-y-hidden');
				this.confirmModal = true;
			}
        },
        setStopData(data){
            if(data.type == 1){
                this.stops_options.map((item) => {
                    console.log(item);
                    if(item.id == data.depart_after){
                        this.booking.stops[this.currentIndex].depart_after = item.text;
                    }
                });
            }else{
                var strDateTime = data.date;
                var myDate = new Date(strDateTime);
                // console.log("stop data", data, myDate.toDateString());
                let formattedDate = myDate.getDate() + '-' + (myDate.getMonth() + 1) + '-' + myDate.getFullYear()
                this.booking.stops[this.currentIndex].depart_after = formattedDate + " "+ data.time;
            }
            this.showModal();
        },
        removeStop(stopIndex){
            this.booking.stops = this.booking.stops.map((stop, index) => {
                if(stopIndex !== index)
                    return stop;
            })
        },
    },
}
</script>
<template>
    <div class="p-3">
        <h3 class="text-3xl">Coach hire & bus rentals across Europe</h3>
        <p>Thanks to our vast network of bus partners, we are always able to find the best deal for your bus with driver. Save 15% - 40% by booking through Bookabus.</p>
        
        <div class="booking_type flex bg-[#F3F6FA] p-5 rounded">
            <h3 class=" pr-3 text-2xl font-bold text-[#4d4d4d]">Plan your</h3>
            <div class="flex items-center pl-4">
                <input id="bordered-radio-1" type="radio" value="1" v-model="booking.type" name="bordered-radio" class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
                <label for="bordered-radio-1" class="w-full ml-2 text-sm font-bold text-gray-900 dark:text-gray-300">Return Trip</label>
            </div>
            <div class="flex items-center pl-4">
                <input checked id="bordered-radio-2" type="radio" value="2" v-model="booking.type" name="bordered-radio" class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
                <label for="bordered-radio-2" class="w-full ml-2 text-sm font-bold text-gray-900 dark:text-gray-300">One-Way Trip</label>
            </div>
            <div class="flex items-center pl-4">
                <input checked id="bordered-radio-2" type="radio" value="3" v-model="booking.type" name="bordered-radio" class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
                <label for="bordered-radio-2" class="w-full ml-2 text-sm font-bold text-gray-900 dark:text-gray-300">Multiple Stops</label>
            </div>
        </div>
        <div class="grid gap-6 mb-6 md:grid-cols-2 mt-3">
            <div class="flex items-end">
                <div class=" mr-2 mb-3">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 11-6 0 3 3 0 016 0z" />
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1115 0z" />
                    </svg>
                </div>
                <div class=" flex-1">
                    <label for="from" class="block mb-2 text-left text-sm font-bold text-[#93A2A8]">From</label>
                    <input type="text" id="from" v-model="booking.departure_address" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Address and/or city" required>
                </div>
            </div>
            <div class="grid gap-6 grid-cols-2">
                <div>
                    <div class="flex-1">
                        <label for="depart_date" class="block text-left mb-2 text-sm font-bold text-[#93A2A8]">Departure Date:</label>
                        <VueDatePicker 
                            v-model="booking.departure_date" 
                            :enable-time-picker="false" 
                            six-weeks 
                            :placeholder="'dd-mm-yyyy'"
                            auto-apply="true"
                            :format="'dd-MM-yyyy'"
                        />
                    </div>
                </div>
                <div>
                    <label for="depart_time" class="block text-left mb-2 text-sm font-bold text-[#93A2A8]">Departure Time:</label>
                    <input type="time" v-model="booking.departure_time"  class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Time" required>
                </div>
            </div>
        </div>

        <!-- stops -->
        <div v-for="(stop, stopIndex) in booking.stops" :key="stopIndex" class="grid gap-6 mb-6 md:grid-cols-2 mt-3">
            <div class="flex items-end">
                <div class=" mr-2 mb-3">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                        <path stroke-linecap="round" stroke-linejoin="round" d="M9 9.563C9 9.252 9.252 9 9.563 9h4.874c.311 0 .563.252.563.563v4.874c0 .311-.252.563-.563.563H9.564A.562.562 0 019 14.437V9.564z" />
                    </svg>
                </div>
                <div class=" flex-1">
                    <label for="to" class="block mb-2 text-left text-sm font-bold text-[#93A2A8]">Via:</label>
                    <input type="text" v-model="stop.address" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Address and/or city" required>
                </div>
            </div>
            <div class="w-full">
                <div class="flex items-end h-full">
                    <div class="flex-1">
                        <label @click="opnModal(stopIndex)" for="depart_date" class="flex items-center cursor-pointer text-left text-sm text-[#93A2A8] p-2.5 border border-gray-300 rounded-lg">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v6h4.5m4.5 0a9 9 0 11-18 0 9 9 0 0118 0z" />
                            </svg>
                            <span class="ml-2">{{ stop.depart_after }}</span>
                        </label>
                    </div>
                    <div class="ml-2 mb-3">
                        <svg @click="removeStop(stopIndex)" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 cursor-pointer">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M9.75 9.75l4.5 4.5m0-4.5l-4.5 4.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                        </svg>
                    </div>
                </div>
            </div>
        </div>


        <div class="grid gap-6 mb-6 md:grid-cols-2 mt-3">
            <div class="flex items-end">
                <div class=" mr-2 mb-3">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M15 10.5a3 3 0 11-6 0 3 3 0 016 0z" />
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1115 0z" />
                    </svg>
                </div>
                <div class=" flex-1">
                    <label for="to" class="block mb-2 text-left text-sm font-bold text-[#93A2A8]">To:</label>
                    <input type="text" v-model="booking.return_address" id="to" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Address and/or city" required>
                </div>
            </div>
            <div class="grid gap-6 grid-cols-2">
                <div>
                    <div class="flex-1">
                        <label for="return_date" class="block text-left mb-2 text-sm font-bold text-[#93A2A8]">Return Date:</label>
                        <VueDatePicker 
                            v-model="booking.return_date" 
                            :enable-time-picker="false" 
                            six-weeks 
                            :placeholder="'dd-mm-yyyy'"
                            auto-apply="true"
                            :format="'dd-MM-yyyy'"
                        />
                    </div>
                </div>
                <div>
                    <label for="return_time" class="block text-left mb-2 text-sm font-bold text-[#93A2A8]">Return Time:</label>
                    <input type="time" v-model="booking.return_time"  class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Address and/or city" required>
                </div>
            </div>
        </div>
        <div @click="addStop" class="flex cursor-pointer text-[#209ac9] mb-5">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v6m3-3H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
            <p class="ml-3">Add stop inbetween</p>
        </div>

        <div class="flex items-center bg-[#F3F6FA] p-5 rounded">
            <label class="cursor-pointer pr-3 text-md text-[#4d4d4d]">
                <input checked v-model="booking.outbound_trip" id="checked-checkbox" type="checkbox" value="" class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600">
                Outbound trip is equal to return trip.
            </label>
            <div class="flex items-center pl-4">
                <label for="bordered-radio-1" class="w-full ml-2 text-sm font-bold text-gray-900 dark:text-gray-300">Passengers</label>
                <input type="number" v-model="booking.passengers" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="eg: 43" required>
            </div>
            <div class="flex-1 items-center pl-4 md:ml-5">
                <button @click="showConfirmModal()" class="w-full flex text-white bg-[#f99d0b] px-5 py-3 rounded">
                    <span class="flex-1 text-right">Continue</span>
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 flex-1 text-right">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M13.5 4.5L21 12m0 0l-7.5 7.5M21 12H3" />
                    </svg>
                </button>
            </div>
        </div>
    </div>

    <!-- Hire me modal -->
    <StopModal
        :showModal="showModal"
        :modal="modal"
        aria-modal=""
    />
    <ConfirmationModal
        :showConfirmModal="showConfirmModal"
        :confirmModal="confirmModal"
        :bookingData="booking"
        aria-modal=""
    />

</template>
<style scoped>

</style>