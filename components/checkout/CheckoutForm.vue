<template>
    <div id="checkout" class="checkout">
        <div class="checkout__wrapper">
            <div class="checkout__head">
                <h1 class="checkout__title">Checkout form</h1>
            </div>
            <form 
                class="form checkout__form"
                @submit.prevent="onSubmit"
            >
                <div class="form__item">
                    <h3>Personal information</h3>
                    <div class="form__line">
                        <div class="form__col">
                            <label class="form__label">First name</label>
                            <customInput 
                                :value="name" 
                                :error="!nameValid" 
                                :error-text="'error'" 
                                @oninput="name = $event, nameValid = true"
                            />
                        </div>
                        <div class="form__col">
                            <label class="form__label">Last name</label>
                            <customInput 
                                :value="lastName" 
                                :error="!lastNameValid" 
                                :error-text="'error'" 
                                @oninput="lastName = $event, lastNameValid = true"
                            />
                        </div>
                    </div>
                </div>

                <div class="form__item">
                    <h3>Contact information</h3>
                    <div class="form__line">
                        <div class="form__col">
                            <label class="form__label">Email for receipt</label>
                            <customInput 
                                :value="email" 
                                :error="!emailValid || !emailValidEmpty" 
                                :error-text="emailValidEmpty ? 'valid' : 'error'" 
                                @oninput="email = $event, emailValid = true, emailValidEmpty = true"
                            />
                        </div>
                        <div class="form__col">
                            <label class="form__label">Phone numbers</label>
                            <customInput 
                                :value="phone" 
                                :error="!phoneValid" 
                                :error-text="'error'" 
                                @oninput="phone = $event, phoneValid = true"
                            />
                        </div>
                        <div class="form__col">
                            <label class="form__label">Country</label>
                            <customInput 
                                :value="country" 
                                :error="!countryValid" 
                                :error-text="'error'" 
                                @oninput="country = $event, countryValid = true"
                            />
                        </div>
                        <div class="form__col">
                            <label class="form__label">Address</label>
                            <customInput 
                                :value="address" 
                                :error="!addressValid" 
                                :error-text="'error'" 
                                @oninput="address = $event, addressValid = true"
                            />
                        </div>
                    </div>
                </div>
              
                <div class="form__item">
                    <h3>Payment details</h3>
                    <div class="form__line">
                        <div class="form__col">
                            <label class="form__label">Credit card</label>
                            <customInput 
                                :value="card" 
                                :error="!cardValid" 
                                :error-text="'error'" 
                                placeholder="ХХХХ ХХХХ ХХХХ ХХХХ"
                                @oninput="card = $event, cardValid = true"
                            />
                        </div>
                        <div class="form__col">
                            <label class="form__label">CVV2 code</label>
                            <customInput 
                                :value="code" 
                                :error="!codeValid" 
                                :error-text="'error'" 
                                placeholder="XXX"
                                @oninput="code = $event, codeValid = true"
                            />
                        </div>
                    </div>
                </div>
                <button 
                    class="form__button"
                    type="submit"
                    :disabled="sending" 
                    v-if="!sending" 
                    aria-label="Submit"
                >
                    send
                </button>
                <div v-if="sending" class="success">success</div>
            </form>
        </div>
    </div>
</template>

<script>
import { mapState, mapMutations } from 'vuex'
import customInput from "~/components/CustomInput.vue";
import Vue from 'vue';

export default {
    props: ['data'],
    data() {  
        return {

            name: '',
            nameValid: true,

            lastName: '',
            lastNameValid: true,

            email: '',
            emailValid: true,
            emailValidEmpty: true,

            phone: '',
            phoneValid: true,

            country: '',
            countryValid: true,

            address: '',
            addressValid: true,

            card: '',
            cardValid: true,

            code: '',
            codeValid: true,

            success: false,
            sending: false,
        }
    },

    components: {  
        customInput
    },

    methods: {
        onSubmit() {
            let isValid = true

            if (!this.name) {
                isValid = false
                this.nameValid = false
            }

            if (!this.lastName) {
                isValid = false
                this.lastNameValid = false
            }

            if (!this.email) {
                isValid = false
                this.emailValidEmpty = false
            }

            if (this.email && !/^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(this.email)) {
                isValid = false
                this.emailValid = false
            }

            if (!this.phone) {
                isValid = false
                this.phoneValid = false
            }

            if (!this.country) {
                isValid = false
                this.countryValid = false
            }

            if (!this.address) {
                isValid = false
                this.addressValid = false
            }

            if (!this.card) {
                isValid = false
                this.cardValid = false
            }

            if (!this.code) {
                isValid = false
                this.codeValid = false
            }

            if (isValid) this.sendForm()
        },

        async sendForm() {
            this.sending = true 
            this.reset()
            console.log('send')
        },

        reset() {
            this.name = ''
            this.nameValid = true
            this.lastName = ''
            this.lastNameValid = true
            this.phone = ''
            this.phoneValid = true
            this.email = ''
            this.emailValid = true
            this.emailValidEmpty = true
            this.country = ''
            this.countryValid = true
            this.address = ''
            this.addressValid = true
            this.card = ''
            this.cardValid = true
            this.code = ''
            this.codeValid = true
        },

    },

    watch: {
       
    } 
}
</script>

<style lang="scss" scoped>
.checkout {
    padding: 40px 0;

    &__wrapper {
        width: 1366px;
        max-width: 100%;
        padding: 0 20px;
        margin: 0 auto;
    }

    &__head {
        display: flex;
        align-items: center;
        justify-content: center;
        -webkit-backdrop-filter: blur(5px);
        backdrop-filter: blur(5px);
        background-color: rgba(255, 255, 255, .6);
        border: 1px solid #fff;
        position: -webkit-sticky;
        position: sticky;
        top: 10px;
        padding: 14px 24px;
        border-radius: 16px;
        z-index: 3;
        margin-bottom: 20px;
    }

    .form {
        display: flex;
        gap: 20px;
        flex-direction: column;

        &__item {
            padding: 24px 24px;
            border-radius: 16px;
            background-color: #fff;
        }

        &__line{
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
            justify-content: space-between;
            position: relative;
            z-index: 1;
        }

        &__col {
            width: calc(50% - 10px);
        }

        &__label{
            display: block;
            width: 100%;
            font-weight: 300;
            font-size: 15px;
            line-height: 20px;
            letter-spacing: 0.01em;
            color: #005A71;
            margin-bottom: 12px;
            max-width: calc(100% - 136px);
        }

        &__button {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
            height: 100px;
            font-size: 32px;
            color: #EFF9FF;
            font-weight: 300;
            text-align: center;
            letter-spacing: -0.02em;
            border: none;
            outline: none;
            border-radius: 12px;
            background: #000;
            cursor: pointer;
            transition: background-color .35s ease;

            @media screen and (min-width: 1201px) {

                &:hover {
                    background-color: #016e19;
                }
            }
        }
    }


    .success {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100px;
        padding: 14px 14px;
        font-size: 24px;
        color: #016e19;
        border-radius: 12px;
        user-select: none;
        pointer-events: none;
    }


}
</style>
    