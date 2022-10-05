<template>

    <div class="logIn_user">
        
        <div class="container_logIn_user">
            <img src="../assets/logo.png">
            <h1>HomeCare</h1>
            
            <h3>Personas</h3>

            <form v-on:submit.prevent="processLogInUser" >
                <input type="text" v-model="user.username" placeholder="Usuario">
                <br>
                <input type="password" v-model="user.password" placeholder="Contraseña">
                <br>
                <br>
                <br>
                <label>Seleccione su perfil:</label>
                <br>
                <select name="nombre">
                    <option>Paciente</option>
                    <option>Medico</option>
                    <option>Enfermero</option>
                    <option>Auxiliar</option>
                    <option>Familiar</option>
                </select>

                <button type="submit">INGRESAR</button>
                
            </form>
                <br>
                <br>
            <h3>CodeGeeks</h3>

        </div>
        <div class="container_img">
            <img src="../assets/happy-doctor-holding-clipboard-with-patients.jpg">
        </div>

        
    </div>

    
    <div class="container_texto_login">
        <h2>Siempre atentos a tú</h2>
        <h1>Salud</h1>

</div>

</template>

<script>
import axios from 'axios';

export default {
    name: "LogIn",
    
    data: function(){
        return {
            user: {
                username:"",
                password:""
            }
        }
    },

    methods: {
        processLogInUser: function(){
            axios.post(
                "https://mision-tic-bank-be.herokuapp.com/login/",
                this.user,
                {headers: {}}
                )
                .then((result) => {
                    let dataLogIn = {
                        username: this.user.username,
                        token_access: result.data.access,
                        token_refresh: result.data.refresh,
                    }
                    
                    this.$emit('completedLogIn', dataLogIn)
                })
                .catch((error) => {
                
                    if (error.response.status == "401")
                        alert("ERROR 401: Credenciales Incorrectas.");
                        
                    });
        }
    }
}

</script>

<style>


    .logIn_user{
        margin: 0;
        padding: 0%;
        height: 100%;
        width: 100%;
        justify-content: center;
        align-items:center;

    }

    .container_img{
        position: absolute;
        right: 0px; 
        top: 0px; 
        z-index: 1;
    }
    
    .container_img  img{
     max-width: 100%;
     max-height: 100%;
     height: 962px;
     width: auto;
    }

    .container_logIn_user {
        position: absolute; 
        left: 0px; 
        top: 0px;
        z-index: 3;
        width: 38%;
        height: 100%;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-color: #7ec544;
        vertical-align: top;
        display: flex;
        box-shadow: 5px 5px 15px rgb(184, 184, 184);
    }

    .container_logIn_user img {
        margin: 0;
        padding: 0%;
        height: 100px;
        width: 90px;
    }

  

    .container_texto_login {
        padding-right: 8%;
        padding-left: 8%;
        padding-top: 1%;
        position: absolute; 
        right: 0px; 
        top: 700px;
        z-index: 2;
        background-color:#037e8c;
        box-shadow: 5px 5px 15px rgb(20, 39, 53);

    }

    .container_texto_login h1 {
        color: #7ec544;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        align-items: center;
        text-align:right;
        font-size:600%;
        line-height: 0%;
        margin-top: 20%;


    }

    .container_texto_login h2 {
        text-align:right;
        color: #ffffff;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        font-size:120%;
        line-height: 100%;
        


    }

    .logIn_user h3{
        color: #eaeaea;
        font-family: Tahoma;


    }

    .logIn_user h1{
        margin: 5px;
        padding: 0%;
        color: #ffffff;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        align-items: center;
        font-size:250%;
    }

    .logIn_user form{
        width: 50%;
    }

    .logIn_user input{
        height: 40px;
        width: 100%;
        box-sizing: border-box;
        padding: 10px 20px;
        margin: 5px 0;
        text-align:center;

        background-color:#7ec544;
        color: #ffffff;
        border-top: none;
        border-right:none;
        border-left: none;
        border-color: #ffffff;
        opacity: 50%;
    }

    .logIn_user input:focus {
        background-color: #ffffff;
        color: #037e8c;
        border-style:hidden;
        border-color: #86D149;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        border-top: none;
        border-right:none;
        border-left: none;
        border-color: #ffffff;
        outline-offset: 0px;
        outline: none;

    }

    ::placeholder { 
        color: #ffffff;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        
    }

    .logIn_user label{
        color: #b4db98;
        text-align: center;
        font-family: 'Trebuchet MS';
        padding: 20px 100px;
    }

    .logIn_user select {
     background-color: #ffffff;
     border: none;
     height: 35px;
     padding: 5px 30px;
     width: 100%;
     color: #7ec544;
     opacity: 50%;
     text-align: left;
     border-radius: 10px;
  }

  .logIn_user select:focus {
    background-color: #ffffff;
        color: #037e8c;
        border-color: #86D149;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        border-top: none;
        border-right:none;
        border-left: none;
        border-color: #ffffff;
        outline-offset: 0px;
        outline: none;
        opacity: 50%;
  }

    .logIn_user button{
        width: 100%;
        height: 80px;
        color: #ffffff;
        background: #037e8c;
        border: 1px;
        border-radius: 10px;
        padding: 10px 20px;
        margin: 50px 0;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        font-size: large;
    }

    .logIn_user button:hover{
        color: #55852E;
        background: #ffffff;
        border: 0px;
    }

</style>