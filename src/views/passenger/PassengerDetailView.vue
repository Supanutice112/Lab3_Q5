<script setup lang="ts">
import { ref } from 'vue'
import { type PassengerItem } from '@/passenger'
import type { PropType } from 'vue';
import {useRouter} from 'vue-router'
import {useMessageStore} from '@/stores/message';
const store = useMessageStore()
const props = defineProps ({
passenger: {
    type: Object as PropType<PassengerItem>,
        require: true
}
})

const router = useRouter()
function edit() {
store.updateMessage(props.passenger?.first_name+' the data have been successfully update' )
setTimeout(() => {
    store.resetMessage()
},3000)
router.push({
    name: 'passenger-list',
    params: {
        id: props.passenger?.id
    }
})
}
</script>
<template>
    <div v-if="passenger">
        <p>first name: {{ passenger.first_name }} last name: {{ passenger.last_name }} email: {{ passenger.email }}</p>
        <p>gender: {{ passenger.gender  }} ip: {{ passenger.ip_address }} Source: {{  passenger.Source }}</p>
        <p>Destination: {{ passenger.Destination  }} travelDate: {{ passenger.travelDate }} airlineId: {{  passenger.airlineId }}</p>
        <button @click="edit">Edit</button>
    </div>
</template>
