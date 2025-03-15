<!--<script setup>-->
<!--import { computed, onMounted, ref } from 'vue';-->
<!--import { useRoute, useRouter } from 'vue-router';-->
<!--import { useApplicationStore } from '@/stores/application.js';-->

<!--const router = useRouter();-->
<!--const route = useRoute();-->
<!--const store = useApplicationStore();-->
<!--const formDataRef = ref({-->
<!--    "date": "",-->
<!--    "location": ""-->
<!--});-->

<!--const userId = ref(null);-->
<!--onMounted(()=>{-->
<!--    userId.value = store.userData.id;-->
<!--})-->
<!--const token = store.userData.accessToken;-->

<!--const isValidText = (text) => {-->
<!--    // Regular expression to match only text with spaces and no numbers-->
<!--    return /^[A-Za-z\s]*$/.test(text);-->
<!--};-->
<!--const onSubmit = async() => {-->
<!--    if (formDataRef.value.location && !isValidText(formDataRef.value.location)) {-->
<!--        alert('Location should not contain numbers!');-->
<!--        return;-->
<!--    }-->
<!--    try {-->
<!--        const response = await fetch(`http://localhost:9090/donationrequest/${userId.value}/new`, {-->
<!--        method: 'POST',-->
<!--            headers: {-->
<!--            'Content-Type': 'application/json',-->
<!--                'Authorization': `Bearer ${token}`,-->
<!--        },-->
<!--            body: JSON.stringify(formDataRef.value),-->
<!--    });-->
<!--    if (response.ok) {-->
<!--        const data = await response.json();-->
<!--        console.log(data); // Log the response data if needed-->
<!--        // Handle success, update UI or perform other actions-->
<!--        alert('Donation Request Created !');-->
<!--    } else {-->
<!--        // Handle error-->
<!--        console.error('Error creating Donation Request');-->
<!--    }-->
<!--} catch (error) {-->
<!--    console.error('An unexpected error occurred:', error);-->
<!--}-->
<!--};-->

<!--</script>-->


<!--<template>-->
<!--    <div class="container mb-4">-->
<!--        <h1>New Donation Request</h1>-->
<!--    </div>-->
<!--&lt;!&ndash;    <div>&ndash;&gt;-->
<!--&lt;!&ndash;        <pre>{{ data }}</pre>&ndash;&gt;-->
<!--&lt;!&ndash;    </div>&ndash;&gt;-->
<!--    <div class="container mb-4">-->
<!--        <div class="mb-2">-->
<!--            <label for="date">Date</label>-->
<!--            <input class="form-control" id="date" v-model="formDataRef.date" type="date" />-->
<!--        </div>-->
<!--        <div class="mb-2" :class="{ 'has-error': formDataRef.location && !isValidText(formDataRef.location)}">-->
<!--            <label for="location">Location</label>-->
<!--            <input class="form-control" id="location" v-model="formDataRef.location" type="text" />-->
<!--        </div>-->
<!--        <div class="">-->
<!--            <button class="btn btn-primary" @click="onSubmit" type="button">Submit Form</button>-->
<!--        </div>-->
<!--    </div>-->
<!--</template>-->

<!--<style>-->
<!--.has-error input[type="text"] {-->
<!--    border-color: red;-->
<!--}-->
<!--</style>-->


<script setup>
import { ref, computed, onMounted } from 'vue';
import { useRemoteData } from '@/composables/useRemoteData.js';
import { useApplicationStore } from '@/stores/application.js';
const formDataRef = ref({
    "date": "",
    "location": ""
});

const urlRef = ref(null);
const authRef = ref(true);
const methodRef = ref('POST');
const store = useApplicationStore();


const userIdRef = ref(null);

const { data, performRequest } = useRemoteData(urlRef, authRef, methodRef, formDataRef);

const isValidText = (text) => {
    // Regular expression to match only text with spaces and no numbers-->
    return /^[A-Za-z\s]*$/.test(text);
};

onMounted(() => {
    userIdRef.value = store.userData.id;
    urlRef.value = 'http://localhost:9090/donationrequest/' + userIdRef.value + '/new';
});


const submitForm = async () =>{
    if (formDataRef.value.location && !isValidText(formDataRef.value.location)) {
        alert('Provide a valid email!');
        return;
    }
    await performRequest();

};
</script>


<template>
    <div class="mb-4">
        <tbody v-if="loading">
        <tr>
            <td colspan="5">Loading...</td>
        </tr>
        </tbody>
    </div>
    <div>
        <div v-if="data && data.success" class="alert alert-success">
            Donation Request Created!
        </div>
        <div v-else-if="data && data.error" class="alert alert-danger">
            Creating new Donation Request Failed. Please try again.
        </div>
    </div>
    <div>
        <div class="mb-2">
            <label for="date">Date: </label>
            <input class="form-control" type="date" id="date" v-model="formDataRef.date"/>
        </div>
        <div class="mb-2" :class="{ 'has-error': formDataRef.location && !isValidText(formDataRef.location)}">
            <label for="location">Location: </label>
            <input class="form-control" id="location" v-model="formDataRef.location" type="text" />
        </div>
        <button @click="submitForm" type="submit">Submit</button>
    </div>
</template>

<style>
.has-error input[type="text"] {
    border-color: red;
}
</style>