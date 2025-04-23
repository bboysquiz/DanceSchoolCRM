<template>
    <!-- eslint-disable-next-line vue/max-attributes-per-line -->
    <q-layout>
        <q-inner-loading :showing="loading" class="login-layout__loading">
            <q-spinner-gears size="50px" color="primary" z-index="1000" />
        </q-inner-loading>
        <q-page-container>
            <q-page class="login-layout__container text-white text-center q-pa-md flex flex-center login">
                <q-banner v-show="error" inline-actions class="text-white bg-red"
                    :style="'position: fixed; top: 0; left: 0; width: 100%;'">
                    Ошибка авторизации. Проверьте введённые данные
                </q-banner>
                <div class="column q-pa-lg">
                    <div class="row login-containter">
                        <q-card flat class="login-layout__card">
                            <q-card-section class="login-layout__logo-section">
                                <span>LOGO</span>
                            </q-card-section>
                            <q-card-section class="login-layout__credentials-section">
                                <q-form class="q-px-sm q-pt-xl" :style="'padding-top: 0;'">
                                    <q-input :style="'border-radius:4px; margin: 40px 0 16px 0;'" square
                                        v-model="form.username" type="email" label="Имя пользователя"
                                        class="input-login">
                                        <template v-slot:prepend>
                                            <q-icon :style="'margin-left:16px;'">
                                                <svg width="24" height="24" viewBox="0 0 24 24" fill="none"
                                                    xmlns="http://www.w3.org/2000/svg">
                                                    <circle cx="12" cy="7" r="3" stroke="#474A52" stroke-width="1.4" />
                                                    <path
                                                        d="M4 19.0758C4 15.0483 8.75977 14 12 14C15.2402 14 20 15.0483 20 19.0758C20 19.5862 19.5862 20 19.0758 20H4.92424C4.4138 20 4 19.5862 4 19.0758Z"
                                                        stroke="#474A52" stroke-width="1.4" />
                                                </svg>
                                            </q-icon>
                                        </template>
                                    </q-input>
                                    <q-input :style="'border-radius:4px;'" square v-model="form.pass" type="password"
                                        label="Пароль" @keyup.enter="auth()" class="input-password">
                                        <template v-slot:prepend>
                                            <q-icon :style="'margin-left:16px;'">
                                                <svg width="24" height="24" viewBox="0 0 24 24" fill="none"
                                                    xmlns="http://www.w3.org/2000/svg">
                                                    <path
                                                        d="M15 9V6C15 4.34315 13.6569 3 12 3C10.3431 3 9 4.34315 9 6V9M8 21H16C17.6569 21 19 19.6569 19 18V12C19 10.3431 17.6569 9 16 9H8C6.34315 9 5 10.3431 5 12V18C5 19.6569 6.34315 21 8 21ZM13 15C13 15.5523 12.5523 16 12 16C11.4477 16 11 15.5523 11 15C11 14.4477 11.4477 14 12 14C12.5523 14 13 14.4477 13 15Z"
                                                        stroke="#646476" stroke-width="1.4" stroke-linecap="round"
                                                        stroke-linejoin="round" />
                                                </svg>
                                            </q-icon>
                                        </template>
                                    </q-input>
                                </q-form>
                            </q-card-section>



                            <q-card-actions class="q-px-lg" :style="'position: absolute; bottom: 5%; width: 100%;'">
                                <q-btn unelevated size="lg"
                                    :style="'background: #4E6DAF; height: 48px; color: white; border-radius: 8px; font-weight: 500; font-size: 16px; line-height: 18px;'"
                                    class="full-width" label="Войти" @click="auth()" />
                                <q-btn unelevated size="lg"
                                    :style="'background: #4E6DAF; height: 48px; color: white; border-radius: 8px; font-weight: 500; font-size: 16px; line-height: 18px; margin-top: 20px;'"
                                    class="full-width" label="Регистрация" to="/signup" />
                            </q-card-actions>
                        </q-card>
                    </div>
                </div>
            </q-page>
        </q-page-container>
    </q-layout>
</template>

<script setup lang="ts">
import { ref } from 'vue';
// import { useRouter } from 'vue-router';
// import { useUserStore } from 'src/stores/user-store';
// const store = useUserStore();
const loading = ref(false);
// const router = useRouter();
const error = ref();
const form = ref({
    username: '',
    pass: '',
});
const auth = () => {
    loading.value = true;
    error.value = '';
    // setTimeout(() => {
    //     store.authUser({
    //         username: form.value.username,
    //         password: form.value.pass
    //     })
    //         .then((res) => {
    //             // const refreshToken = res.data.refresh_token;
    //             // localStorage.setItem('refreshToken', refreshToken);
    //             console.log('access', res)
    //         })
    //         .then(() => {
    //             router.push('/').then(() => loading.value = false);
    //         })
    //         .catch((e) => {
    //             console.log(e)
    //             if (e.response) {
    //                 loading.value = false;
    //                 error.value = e.response.data;
    //             }
    //         });
    // }, 250);
}



</script>
<style>
.login {
    border: none;
    background-image: url('assets/desktop-background.png');
    background-repeat: no-repeat;
    background-size: cover;
    backdrop-filter: blur(4px);
    justify-content: center;
}

.login-layout__container {
    overflow-y: auto;
    height: 100vh;
    position: relative;
}

.login-layout__card {
    width: 480px;
    height: 480px;
    border: none;
    background: #FFFFFFe5;
    border-radius: 8px;
}

.login-layout__loading {
    position: absolute !important;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 1000;
}


@media screen and (max-width: 768px) {
    .login-layout__card {
        width: 90vw;
    }

    .login-containter {
        width: 90vw;
    }

}

@media screen and (max-width: 850px) {
    .login-layout__card {
        height: 360px;
    }

    .login-layout__credentials-section {
        padding-top: 0;
        margin-top: -33px;
    }

    .login-layout__logo-section {
        padding-bottom: 0;
    }

}
</style>