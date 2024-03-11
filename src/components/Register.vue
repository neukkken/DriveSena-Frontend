<template>
    <div class="containerRegisterMain">
        <form class="RegisterContainer" id="RegisterForm">
            <div class="title">
                <h1>Register,</h1>
                <p>Sign up to continue</p>
            </div>
            <input v-model="usernameInput" required type="text" placeholder="username" id="usernameInputRegister">
            <input v-model="passwordInput" required type="password" placeholder="password" name=""
                id="passwordInputRegister">
            <input v-model="confirmPasswordInput" required type="password" placeholder="confirm password" name=""
                id="confirmPasswordInputRegister">
            <input v-model="emailInput" required type="email" placeholder="email" name="" id="emailInputRegister">
            <p>Already have an account? <a href="/login">Login</a></p>
            <button type="button" @click="register">Register</button>
        </form>
    </div>
</template>

<script>

export default {
    name: 'RegisterForm',
    data() {
        return {
            usernameInput: '',
            passwordInput: '',
            confirmPasswordInput: '',
            emailInput: '',
        }
    },
    methods: {
        changeLogin() {
            this.$router.push('/login');
        },


        register() {


            if (this.usernameInput == '' || this.passwordInput == '' || this.confirmPasswordInput == '' || this.emailInput == '') {
                alert('Todos los campos son obligatorios')
            } else if (this.passwordInput != this.confirmPasswordInput) {
                alert('las contrasenas no coinciden')
            } else if (this.passwordInput.length < 8) {
                alert('la contrasena debe ser mayor o igual a 8 caracteres')
            } else {
                //enviar datos al backend

                fetch('http://localhost:3000/users', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        username: this.usernameInput,
                        password: this.passwordInput,
                        email: this.emailInput
                    })
                })
                    .then(response => response.json())
                    .then(data => { console.log(data)})
                    .catch(error => console.error(error))
                {
                    alert('Usuario registrado exitosamente')
                    this.changeLogin()
                }


            }
        }

    }
}


</script>

<style scoped>
.containerRegisterMain {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 80vh;
}

.RegisterContainer {
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

.RegisterContainer input{
    font-weight: bold;
    font-size: 16px;
    box-shadow: 5px 5px 0px #000;
    margin: 10px 0;
    border: solid 2px;
    border-radius: 5px;
    width: 70%;
    padding: 10px 20px;
}

.RegisterContainer button {
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

.RegisterContainer button:active {
    transform: translate(5px, 5px);
    box-shadow: none;
}
</style>