<template>
    <div class="wrapper">
        <div class="wrapper-content">
            <section>
                <div class="container">
                    <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
                    <modals
                        title="First Modal"
                        v-show="modalFirst"
                        @closeModal="modalFirst = false"
                    >
                       <div slot="body">

                       </div>
                    </modals>
                </div>
            </section>
        </div>
    </div>
</template>

<script>
    import modals from './components/Modal';

    export default {
        name: 'App',
        components: {
            modals
        },
        data() {
            return {
                modalFirst: false
            }
        }
    }
</script>

<style>

</style>
