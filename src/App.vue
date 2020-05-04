<template>
    <div class="wrapper">
        <div class="wrapper-content">
            <section>
                <div class="container">

                    <!--first-modal-->
                    <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
                    <modals
                        title="First Modal"
                        v-show="modalFirst"
                        @closeModal="modalFirst = false"
                    >
                       <div slot="body">

                       </div>
                    </modals>

                    <!--second-modal-->
                    <button class="btn btnPrimary" @click="modalSecond.show = !modalSecond.show">Show first modal</button>
                    <modals
                        title="Modal with form"
                        v-show="modalSecond.show"
                        @closeModal="modalSecond.show = false"
                    >
                       <div slot="body">
                           <form action="#" @submit.prevent="submitSecondFrom">
                               <label>Name</label>
                               <input type="text" v-model="modalSecond.name">
                               <label>Email</label>
                               <input type="email" v-model="modalSecond.email" novalidate="novalidate">
                               <button class="btn btnPrimary" type="submit">Submit</button>
                           </form>
                       </div>
                    </modals>

                    <!--third-modal-->
                    <button class="btn btnPrimary" @click="modalValidate = !modalValidate">Form with validate</button>
                    <modalValidate
                        v-show="modalValidate"
                        @close="modalValidate=false"
                    />

                </div>
            </section>
        </div>
    </div>
</template>

<script>
    import modals from './components/Modal';
    import modalValidate from './components/ModalValidate';

    export default {
        name: 'App',
        components: {
            modals,
            modalValidate
        },
        data() {
            return {
                modalFirst: false,
                modalSecond: {
                    show: false,
                    name: '',
                    email: ''
                },
                modalValidate: false
            }
        },
        methods: {
            submitSecondFrom() {
                this.clearSecondFields();
                this.closeSecondModal();
            },
            clearSecondFields(){
                this.modalSecond.name = '';
                this.modalSecond.email = '';
            },
            closeSecondModal(){
                this.modalSecond.show = false;
            }
        }
    }
</script>

<style>

</style>
