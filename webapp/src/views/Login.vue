<template>
    <div class="auth-bg">
        <div
            class="container h-100 d-flex align-items-center justify-content-center flex-column"
        >
            <h1 class="auth-header">漢字 club</h1>
            <div class="shadow-lg p-3 bg-white rounded" style="width: 18rem">
                <div class="card-body">
                    <form @submit.prevent="submit">
                        <div class="alert alert-warning" v-if="error != null">
                            {{ error }}
                        </div>

                        <div class="form-group">
                            <label for="username">Username</label>
                            <input
                                id="username"
                                class="form-control"
                                type="text"
                                placeholder="Username"
                                v-model="form.username"
                            />
                        </div>

                        <div class="form-group">
                            <label for="password">Password</label>
                            <input
                                id="password"
                                class="form-control"
                                type="password"
                                placeholder="Password"
                                v-model="form.password"
                            />
                        </div>

                        <div class="form-group form-check">
                            <input
                                type="checkbox"
                                class="form-check-input"
                                id="rememberMe"
                                v-model="form.rememberMe"
                            />
                            <label class="form-check-label" for="rememberMe"
                                >Remember me</label
                            >
                        </div>

                        <button type="submit" class="btn btn-primary card-link">
                            Login
                        </button>
                        <router-link to="/register" class="card-link"
                            >Create account</router-link
                        >
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { mapActions } from 'vuex';

function checkFormEmpty(obj) {
    for (let key in obj) {
        let val = obj[key];

        if (!val.trim) continue;
        if (val.trim() === '') return true;
    }
    return false;
}

export default {
    name: 'Login',
    components: {},
    data() {
        return {
            form: {
                username: '',
                password: '',
                rememberMe: false
            },
            error: null
        };
    },
    methods: {
        ...mapActions(['Login']),
        async submit() {
            if (checkFormEmpty(this.form)) {
                return;
            }

            try {
                this.error = null;
                await this.Login(this.form);
                this.$router.push('/');
            } catch (e) {
                this.error = 'Invalid credentials';
            }
        }
    }
};
</script>

<style scoped>
@import url('../assets/auth.css');
</style>
