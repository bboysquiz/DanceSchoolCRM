<template>
    <!-- eslint-disable-next-line vue/max-attributes-per-line -->
    <q-layout>
        <q-inner-loading :showing="loading" class="login-layout__loading">
            <q-spinner-gears size="50px" color="primary" z-index="1000" />
        </q-inner-loading>
        <q-page-container>
            <q-page class="login-layout__container text-white text-center q-pa-md flex login">
                <q-banner v-show="error" inline-actions class="text-white bg-red"
                    :style="'position: fixed; top: 0; left: 0; width: 100%;'">
                    Ошибка авторизации. Проверьте введённые данные
                </q-banner>
                <div>
                    <div class="login-containter">
                        <q-card flat class="login-layout__card">
                            <q-card-section class="login-layout__logo-section">
                                <span>LOGO</span>
                            </q-card-section>
                            <q-card-section class="login-layout__credentials-section">
                                <q-form class="q-px-sm q-pt-xl" :style="'padding-top: 0;'">
                                    <q-input :style="'border-radius:4px; margin: 40px 0 16px 0;'" square
                                        v-model="form.username" type="email" label="Логин"
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
                                        label="Пароль" @keyup.enter="signUp()" class="input-password">
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
                                    <q-input :style="'border-radius:4px; margin: 40px 0 16px 0;'" square
                                        v-model="form.username" type="text" label="Имя" class="input-login">
                                        <template v-slot:prepend>
                                            <q-icon :style="'margin-left:16px;'">
                                                <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960" width="24px" fill="#000">
                                                    <path d="M560-440h200v-80H560v80Zm0-120h200v-80H560v80ZM200-320h320v-22q0-45-44-71.5T360-440q-72 0-116 26.5T200-342v22Zm160-160q33 0 56.5-23.5T440-560q0-33-23.5-56.5T360-640q-33 0-56.5 23.5T280-560q0 33 23.5 56.5T360-480ZM160-160q-33 0-56.5-23.5T80-240v-480q0-33 23.5-56.5T160-800h640q33 0 56.5 23.5T880-720v480q0 33-23.5 56.5T800-160H160Zm0-80h640v-480H160v480Zm0 0v-480 480Z"/>
                                                </svg>
                                            </q-icon>
                                        </template>
                                    </q-input>
                                    <q-input :style="'border-radius:4px; margin: 40px 0 16px 0;'" square
                                        v-model="form.username" type="text" label="Фамилия" class="input-login">
                                        <template v-slot:prepend>
                                            <q-icon :style="'margin-left:16px;'">
                                                <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960" width="24px" fill="#000">
                                                    <path d="M560-440h200v-80H560v80Zm0-120h200v-80H560v80ZM200-320h320v-22q0-45-44-71.5T360-440q-72 0-116 26.5T200-342v22Zm160-160q33 0 56.5-23.5T440-560q0-33-23.5-56.5T360-640q-33 0-56.5 23.5T280-560q0 33 23.5 56.5T360-480ZM160-160q-33 0-56.5-23.5T80-240v-480q0-33 23.5-56.5T160-800h640q33 0 56.5 23.5T880-720v480q0 33-23.5 56.5T800-160H160Zm0-80h640v-480H160v480Zm0 0v-480 480Z"/>
                                                </svg>
                                            </q-icon>
                                        </template>
                                    </q-input>
                                    <q-input :style="'border-radius:4px; margin: 40px 0 16px 0;'" square
                                        v-model="form.username" type="text" label="Номер телефона" class="input-login">
                                        <template v-slot:prepend>
                                            <q-icon :style="'margin-left:16px;'">
                                                <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960" width="24px" fill="#000">
                                                    <path d="M798-120q-125 0-247-54.5T329-329Q229-429 174.5-551T120-798q0-18 12-30t30-12h162q14 0 25 9.5t13 22.5l26 140q2 16-1 27t-11 19l-97 98q20 37 47.5 71.5T387-386q31 31 65 57.5t72 48.5l94-94q9-9 23.5-13.5T670-390l138 28q14 4 23 14.5t9 23.5v162q0 18-12 30t-30 12ZM241-600l66-66-17-94h-89q5 41 14 81t26 79Zm358 358q39 17 79.5 27t81.5 13v-88l-94-19-67 67ZM241-600Zm358 358Z"/>
                                                </svg>
                                            </q-icon>
                                        </template>
                                    </q-input>
                                </q-form>
                            </q-card-section>



                            <q-card-actions class="q-px-lg" :style="'width: 100%;'">
                                <q-btn unelevated size="lg"
                                    :style="'background: #4E6DAF; height: 48px; color: white; border-radius: 8px; font-weight: 500; font-size: 16px; line-height: 18px;'"
                                    class="full-width" label="Зарегистрироваться" @click="signUp()" />
                                <q-btn unelevated size="lg"
                                    :style="'background: #4E6DAF; height: 48px; color: white; border-radius: 8px; font-weight: 500; font-size: 16px; line-height: 18px; margin-top: 20px;'"
                                    class="full-width" label="На страницу входа" to="/login" />
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
const signUp = () => {
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
    justify-content: center;
}


</style>