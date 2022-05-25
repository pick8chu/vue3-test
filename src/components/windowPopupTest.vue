<template>
    <div>
        <span>partner order id</span>
        <input v-model="partner_order_id">
    </div>
    <div>
        <button @click="onOpneWindow">window open popup link (kakaopay)</button>
        <button @click="onCloseWindow">window close popup link (kakaopay)</button>
    </div>
</template>

<script>
import axios from 'axios'
// import { onMounted } from 'vue'
import { ref } from 'vue'

export default {
    setup(){

        const getRandomNumber = () => {
            return (Math.random() + 1).toString(36).substring(2);
        }


        // doesn't have to be reactive -> ref/reactive no need
        let windowPopup = null
        let partner_order_id = ref(getRandomNumber())

        const onOpneWindow = async () => {

            let redirectUrl = await axios.post('http://localhost:8080/api/v1/common/kakaopay', {
                    // baseURL: "http://localhost:8080",
                    cid: "TC0ONETIME",
                    partner_order_id: partner_order_id.value,
                    partner_user_id: "partner_user_id",
                    item_name: "동대문엽기떡볶이",
                    quantity: 1,
                    total_amount: 22000,
                    vat_amount: 0,
                    tax_free_amount: 0,
                    // approval_url: `http://localhost:8080/api/v1/common/kakaopay/success`,
                    // fail_url: "http://localhost:8080/api/v1/common/kakaopay/fail",
                    // cancel_url: "http://localhost:8080/api/v1/common/kakaopay/cancel",
                }, {
                // config
                // headers: {
                //     // "Content-type": "application/json",
                //     // "Access-Control-Allow-Origin" : "*"
                // }
            }).then(res => res.data)

            console.log(redirectUrl)
            // random string generate
            partner_order_id.value = getRandomNumber();

            windowPopup = window.open(redirectUrl, "_blank", "width=500,height=700;")
        }

        const onCloseWindow = () => {
            windowPopup.close()
        }

        const callbackFn = () => {
            alert("done");
        }

        return {
            onOpneWindow,
            onCloseWindow,
            callbackFn,
            partner_order_id
        }
    }

}
</script>

<style>

</style>