<template>
    <div>
        <span>partner order id</span>
        <input v-model="partner_order_id">
    </div>
    <div>
        <button @click="testKakaopaySingle">kakaopay single</button>
    </div>
    <div>
        <button @click="registerSubscription">register subscription</button>
    </div>
    <div>
        <button @click="testKakaopaySubscription">make subscription payment</button>
    </div>
</template>

<script>
import axios from 'axios'
import { ref } from 'vue'

export default {
    setup(){

        /* ------------------ vue cycle hook --------------------*/

        // onMounted(() => {
        //     window.addEventListener("message", (e) => {
        //         if(e.origin == `${baseURL}`){
        //             callbackFn(e.data);
        //         }
        //         console.log(e)
        //     }, false)
        // })

        // onUnmounted(() => {
        //     window.removeEventListener("message")
        // })

        /* ----------------------------------------------------- */


        const baseURL = "http://localhost:8080"

        const getRandomNumber = () => {
            return (Math.random() + 1).toString(36).substring(2);
        }

        const partner_order_id = ref(getRandomNumber())

        const openKakaopay = async (obj) => {

            let redirectUrl = await axios.post(`${baseURL}/api/v1/common/kakaopay${obj.uri}`, obj.param)
                .then(res => res.data)

            partner_order_id.value = getRandomNumber()  // random string generate
            window.open(redirectUrl, "_blank", "width=500,height=700;")
        }

        const testKakaopaySingle = () => {
            openKakaopay({
                uri: "/payments",
                param: {
                        // cid: "TC0ONETIME",
                        // partner_order_id: partner_order_id.value,
                        // partner_user_id: "partner_user_id",
                        parent_id: 'parentId',
                        subscription: false,
                        item_name: "test item name",
                        quantity: "100",
                        total_amount: "22000",
                        vat_amount: "10",
                        tax_free_amount: "10",
                    }
                })
        }

        
        const registerSubscription = () => {
            openKakaopay({
                uri: "/payments",
                param: {

                        parent_id: 'parentId',
                        subscription: true,
                        
                        item_name: "정기결제 테스트",
                        quantity: "0",
                        total_amount: "0",
                        tax_free_amount: "0",
                    }
                })
        }

        const testKakaopaySubscription = async () => {
            const res = await axios.post(`${baseURL}/api/v1/common/kakaopay/subscriptions`, {
                // cid: "TCSUBSCRIP",
                sid : "S29969ff652005080c8e",
                partner_order_id: partner_order_id.value,
                // SID를 발급 받은 첫 결제의 결제 준비 API로 전달한 값과 일치해야 함
                partner_user_id: "partnerUserId",
                item_name: "정기결제 테스트",
                quantity: "10",
                total_amount: "100000",
                tax_free_amount: "10000",
            }).then(res => res.data)

            console.log(res)
            alert(res)
        } 

        return {
            testKakaopaySingle,
            registerSubscription,
            testKakaopaySubscription,
            partner_order_id,
        }
    }

}
</script>

<style>

</style>