<template>
    <div>
        <span>partner order id</span>
        <input v-model="partner_order_id">
    </div>
    <div>
        <button @click="openKakaopay">window open popup link (kakaopay)</button>
    </div>
</template>

<script>
import axios from 'axios'
import { ref, onMounted, onUnmounted } from 'vue'

export default {
    setup(){

        /* ------------------ vue cycle hook --------------------*/

        onMounted(() => {
            window.addEventListener("message", (e) => {
                if(e.origin == `${baseURL}` && e.data == 'callbackFn'){
                    callbackFn();
                }
                console.log(e)
            }, false)
        })

        onUnmounted(() => {
            window.removeEventListener("message")
        })

        /* ----------------------------------------------------- */


        const baseURL = "http://localhost:8080"

        const getRandomNumber = () => {
            return (Math.random() + 1).toString(36).substring(2);
        }

        const partner_order_id = ref(getRandomNumber())

        const openKakaopay = async () => {

            let redirectUrl = await axios.post(`${baseURL}/api/v1/common/kakaopay`, {
                    cid: "TC0ONETIME",
                    partner_order_id: partner_order_id.value,
                    partner_user_id: "partner_user_id",
                    item_name: "test item name",
                    quantity: "100",
                    total_amount: "22000",
                    vat_amount: "10",
                    tax_free_amount: "10",
                }).then(res => res.data)

            partner_order_id.value = getRandomNumber()  // random string generate
            window.open(redirectUrl, "_blank", "width=500,height=700;")
        }

        const callbackFn = () => {
            alert("kakaopay 결제 완료")
        }

        return {
            openKakaopay,
            callbackFn,
            partner_order_id,
        }
    }

}
</script>

<style>

</style>