<script setup>
import { Head, Link, useForm } from '@inertiajs/vue3';
import Input from '@/Components/form/Input.vue';


defineProps({
    canResetPassword: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
const handleShowPassword = () => {
    if (document.getElementById('onPass').classList.contains('hidden')) {
        document.getElementById('offPass').classList.add('hidden')
        document.getElementById('onPass').classList.remove('hidden')
        document.getElementById('password').type = "password"
    } else {
        document.getElementById('offPass').classList.remove('hidden')
        document.getElementById('onPass').classList.add('hidden')
        document.getElementById('password').type = "text"
    }
}
</script>

<template>
    <Head title="Log in" />
    <div class="min-h-screen flex justify-center items-center overflow-hidden " style="background-image: url('/assets/images/background/bg-auth-2.webp')">
    <div>
        <!-- <img class="w 2xl:w-56 mx-auto" src="{{ asset('assets/images/logo.webp') }}" alt=""> -->
        <div class="bg-white rounded shadow mx-4 md:mx-0 px-4 py-2 md:w-[400px] transition-all duration-400 ease-in-out">
            <!-- <div class="mt-4"><img src="{{asset('assets/img/logo.png')}}" alt=""></div> -->
            <div class="text-center mt-4">
                <h1 class="text-[22px] leading-7 font-semibold mb-1 px-2"> Login</h1>
            </div>
            <div class="text-center text-sm mt-6">
                <span>Silahkan Login Terlebih Dahulu !!</span>
                <span class="text-cyan-500"></span>
            </div>
            <form class="px-4 mt-4" @submit.prevent="submit">
                <div class="mb-1 ">
                    <div class="mb-4">
                        <Input
                            id="email"
                            type="text"
                            class="mt-1 block w-full"
                            v-model="form.email"
                            required
                            autofocus
                            placeholder="username"
                            autocomplete="off"
                        />
                        <p v-if="form.errors.email" class="text-cyan-500 text-sm">{{ form.errors.email }}</p>
                    </div>
                </div>

                <div class="mb-1 ">
                    <div class="relative mb-4">
                        <Input
                            id="password"
                            type="password"
                            class="mt-1 block w-full"
                            v-model="form.password"
                            required
                            autofocus
                            placeholder="password"
                            autocomplete="off"
                        />
                        <div @click="handleShowPassword()" class="absolute top-0 right-0 p-2 h-full text-sm font-medium text-whit cursor-pointer">
                            <svg id="onPass" width="18" height="18" fill="currentColor" class="text-gray-800" viewBox="0 0 16 16">
                                <path d="M10.5 8a2.5 2.5 0 1 1-5 0 2.5 2.5 0 0 1 5 0z" />
                                <path d="M0 8s3-5.5 8-5.5S16 8 16 8s-3 5.5-8 5.5S0 8 0 8zm8 3.5a3.5 3.5 0 1 0 0-7 3.5 3.5 0 0 0 0 7z" />
                            </svg>

                            <svg id="offPass" width="18" height="18" fill="currentColor" class="hidden text-gray-800" viewBox="0 0 16 16">
                                <path d="m10.79 12.912-1.614-1.615a3.5 3.5 0 0 1-4.474-4.474l-2.06-2.06C.938 6.278 0 8 0 8s3 5.5 8 5.5a7.029 7.029 0 0 0 2.79-.588zM5.21 3.088A7.028 7.028 0 0 1 8 2.5c5 0 8 5.5 8 5.5s-.939 1.721-2.641 3.238l-2.062-2.062a3.5 3.5 0 0 0-4.474-4.474L5.21 3.089z" />
                                <path d="M5.525 7.646a2.5 2.5 0 0 0 2.829 2.829l-2.83-2.829zm4.95.708-2.829-2.83a2.5 2.5 0 0 1 2.829 2.829zm3.171 6-12-12 .708-.708 12 12-.708.708z" />
                            </svg>
                        </div>
                        <p v-if="form.errors.password" class="text-cyan-500 text-sm">{{ form.errors.password }}</p>
                    </div>
                </div>


                <div class="w-full mt-2">
                    <button type="submit" class="rounded text-xs w-full shadow-md bg-cyan-600
                    hover:bg-cyan-800 px-6 py-2 text-white outline-cyan-800" :disabled="form.processing">Sign In
                    </button>
                </div>
            </form>
            <div class="flex px-4 mt-2 mb-8 ">
                <Link :href="route('register')" class="text-xs text-cyan-600 hover:text-cyan-800">
                    Belum Memiliki Akun?
                </Link>
            </div>

        </div>
    </div>
</div>
</template>
