<template>
    <modals
            title="Modal with form"
            @closeModal="$emit('close')"
    >
        <div slot="body">
            <form action="#" @submit.prevent="onSubmit">
                <div class="form-item" :class="{errorInput: $v.name.$error}">
                    <label>Name</label>
                    <p class="errorText" v-if="!$v.name.required">File is required!</p>
                    <p class="errorText" v-if="!$v.name.minLength">Name must have at lease 4!</p>
                    <input
                        :class="{error: $v.name.$error}"
                        v-model="$v.name.$model"
                    >
                </div>
                <div class="form-item" :class="{errorInput: $v.email.$error}">
                    <label>Email</label>
                    <p class="errorText" v-if="!$v.email.required">Email is required!</p>
                    <p class="errorText" v-if="!$v.email.email">Email is not valid!</p>
                    <input
                        :class="{error: $v.email.$error}"
                        v-model="$v.email.$model"
                    >
                </div>
                <button class="btn btnPrimary" type="submit">Submit</button>
            </form>
        </div>
    </modals>
</template>

<script>
    import modals from './Modal';
    import { required, minLength, email } from 'vuelidate/lib/validators'

    export default {
        components: {
            modals
        },
        data() {
            return {
                name: '',
                email: ''
            }
        },
        validations: {
            name: {
                required,
                minLength: minLength(4)
            },
            email: {
                required,
                email
            }
        },
        methods: {
            onSubmit(){
               this.$v.$touch();
               if(!this.$v.$invalid){
                   const user = {
                       name: this.name,
                       email: this.email
                   };

                   this.name = '';
                   this.email = '';
                   this.$v.$reset();

                   this.$emit('close')
               }
            }
        }
    }
</script>

<style lang="sass">

    .errorText
        display: none
        margin-bottom: 8px
        font-size: 14px
        color: tomato

        .errorInput &
            display: block

    input.error
        border-color: tomato

</style>