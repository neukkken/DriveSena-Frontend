<template>
    <div class="LoginContainerMain">
        <form action="" class="LoginFormContainer">
            <div class="title">
                <h1>Welcome Back!</h1>
                <p>Log In to continue</p>
            </div>
            <input v-model="usernameInput" type="text" placeholder="username">
            <input v-model="passwordInput" type="password" placeholder="password">
            <input v-model="emailInput" type="email" placeholder="email">
            <p>Do not have an <a href="/register">account?</a></p>
            <p>Forgot your <a href="">password?</a></p>
            <button type="button" @click="login">Log In</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'LoginForm',
    data() {
        return {
            usernameInput: '',
            passwordInput: '',
            emailInput: ''
        }
    },
    methods: {
        async fetchData() {
            try {
                const response = await fetch('http://localhost:3000/users');
                if (!response.ok) {
                    throw new Error('Error al cargar los datos');
                }
                this.usuariosRegistrados = await response.json(); // Almacenamos el array de usuarios directamente
            } catch (error) {
                console.error(error);
            }
        },

        login() {
            let data = this.fetchData()
            console.log('tal', data)
        }
    }
}
</script>

<style scoped>
.LoginContainerMain {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 80vh;
}

.LoginFormContainer .title {
    width: 80%;
}

.LoginFormContainer p {
    margin: 5px 0px;
}

.LoginFormContainer {
    border-radius: 5px;
    box-shadow: 7px 7px 0px #000;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: fit-content;
    width: 300px;
    border: solid 2px #000;
    padding: 20px 0px;
}

.LoginFormContainer input {
    font-weight: bold;
    font-size: 16px;
    box-shadow: 5px 5px 0px #000;
    margin: 10px 0;
    border: solid 2px;
    border-radius: 5px;
    width: 70%;
    padding: 10px 20px;
}

.LoginFormContainer button {
    font-weight: bold;
    font-size: 16px;
    box-shadow: 5px 5px 0px #000;
    margin: 10px 0;
    border: solid 2px;
    border-radius: 5px;
    width: 40%;
    padding: 10px 20px;
    transition: 0.1s ease-in-out;
}

.LoginFormContainer button:active {
    transform: translate(5px, 5px);
    box-shadow: none;
}
</style>