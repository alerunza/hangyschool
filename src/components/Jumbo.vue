<script setup>
import { ref } from 'vue';
import { RouterLink, RouterView } from "vue-router";
const props = defineProps(['theme'])

</script>

<script>
const previousLang = localStorage.lang || "Italiano";

export default {
    created() {
        if (previousLang) {
            this.$i18n.locale = previousLang;
        }
        else {
            this.$i18n.locale = "Italiano";
        }
    },
    methods: {
        saveLocale(locale) {
            localStorage.setItem("lang", locale);
        },
        changeLocale(locale) {
            this.$i18n.locale = locale;
            this.$emit("locale-changed", locale);
        }
    },
};
</script>

<template>
    <section id="home">
        <div class="container h-75">
            <div class="row h-100">
                <div class="col h-100 d-flex flex-column align-items-center justify-content-center">
                    <img v-if="props.theme" class=" img-fluid" src="../assets/images/HangManGameWhite.svg"
                        alt="HangMan-Logo" height="">
                    <img v-else class="img-fluid" src="../assets/images/HangManGame.svg" alt="HangMan-Logo" height="">

                    <p class="fs-3 w-50 mx-auto text-center" v-html="$t('jumbotron.gameDescription')"></p>
                    <div class="d-flex flex-column gap-2 mb-3">
                        <!-- <a type="button" href="#about" class="btn btn-primary btn-lg">{{ $t("jumbotron.learnMore")
                        }}</a> -->
                        <RouterLink to="/leaderboard" class="btn btn-primary btn-lg">{{ $t("jumbotron.playNow") }} <span
                                class="badge rounded-pill text-bg-warning">beta</span></RouterLink>
                        <!--                         <button id="disabled" type="button" class="btn btn-primary btn-lg" disabled>{{
                            $t("jumbotron.playNow")
                        }}<span class="badge rounded-pill text-bg-warning">WIP</span></button> -->
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
section {
    background-color: #ffffff;
    border-bottom: 5px solid red;
    box-shadow: 0 30px 30px 0 #ff000029;
}

.btn-primary {
    background-color: #FF4D4D;
    border-color: #FF4D4D;
    font-size: 1.1rem;
}

.btn-primary:hover {
    background-color: #B33636;
    border-color: #FF4D4D;
}

.btn-primary:active {
    background-color: #4e0909;
    border-color: #FF4D4D;
}

#disabled {
    background-color: #ffd3d3;
    color: #FF4D4D;
    border-color: #FF4D4D;
    cursor: not-allowed !important;
}

#dropdownMenuButton2:hover {
    color: #b33636;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}

a.dropdown-item:active {
    background-color: #ec9c9c;
}

.dropdown-menu {
    min-width: 7.2rem;
}

.dropdown-item.active {
    background-color: #e64343;
}

.btn-link {
    color: #ff4d4d;
}

.btn-link:hover {
    color: #b33636;
}
</style>