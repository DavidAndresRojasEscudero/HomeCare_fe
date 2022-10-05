<template>
    <body class="body">
    <header class="container_menu">
    <h2>AUXILIAR</h2>
    <br>
    <br>
    

        <nav>
            <ul class="menu">
                <li><a href="#">Registro</a></li>
                <li><a href="#">Consulta de pacientes</a></li>
                <li><a href="#">asignación de medicos</a></li>
                <li><a href="#">asignación de enfermeros</a></li>
                </ul>
        </nav>

    </header>
    <div class="container_logo">
        <img src="../assets/Homecarelogo.png">
    </div>

        <div class="container_registro">
            <h2>Registro</h2>

            <form v-on:submit.prevent="processSignUp" >
                <h3>Cuenta de usuario</h3>
                <br>
                <input type="text" v-model="user.username" placeholder="cuenta de usuario">
                <br>

                <input type="password" v-model="user.password" placeholder="Contraseña">
                <br>
                <br>
                <label>Seleccione el tipo de usuario</label>
                <br>
                <select name="nombre">
                    <option>Paciente</option>
                    <option>Medico</option>
                    <option>Enfermero</option>
                    <option>Auxiliar</option>
                    <option>Familiar</option>
                </select>
                <br>
                <br>
                <br>

                <h3>Registro de datos</h3>
                <br>
                <input type="text" v-model="user.nombre" placeholder="Nombres">
                <br>

                <input type="text" v-model="user.apellido" placeholder="Apellidos">
                <br>

                <input type="text" v-model="user.id" placeholder="Identificación">
                <br>
                <input type="number" v-model="user.telefono" placeholder="Telefono">
                <br>
                
                <input type="email" v-model="user.email" placeholder="Correo">
                <br>

                <input type="text" v-model="user.direccion" placeholder="direccion">
                <br>

                
                <button type="submit">Registrar</button>
            </form>
        </div>
    </body>

</template>

<script>
import axios from 'axios';

function mostrar() {
    document.getElementById("sidebar").style.width = "300px";
    document.getElementById("contenido").style.marginLeft = "300px";
    document.getElementById("abrir").style.display = "none";
    document.getElementById("cerrar").style.display = "inline";
}

function ocultar() {
    document.getElementById("sidebar").style.width = "0";
    document.getElementById("contenido").style.marginLeft = "0";
    document.getElementById("abrir").style.display = "inline";
    document.getElementById("cerrar").style.display = "none";
}

export default {
    name: "SignUp",

    data: function(){
        return {
            user: {
                username: "",
                password: "",
                name: "",
                email: "",
                account: {
                    lastChangeDate: (new Date()).toJSON().toString(),
                    balance: 0,
                    isActive: true
                }
            }
        }
    },

    methods: {
        processSignUp: function(){
            axios.post(
                "http://localhost:8080",
                this.user,
                {headers: {}}
            )
                .then((result) => {
                    let dataSignUp = {
                        username: this.user.username,
                        token_access: result.data.access,
                        token_refresh: result.data.refresh,
                    }
                    
                    this.$emit('completedSignUp', dataSignUp)
                })
                .catch((error) => {
                    console.log(error)
                    alert("ERROR: Fallo en el registro.");
                });
        }
    }
}



</script>



<style>
      .body{
        margin: 0;
        padding: 0%;
        height: 100%;
        width: 100%;
        justify-content: top;
        align-items:center;

    }

    .container_menu {
        position: absolute; 
        left: 0px; 
        top: 0px;
        z-index: 3;
        width: 20%;
        height: 100%;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-color: #7ec544;
        vertical-align: top;
        display: flex;
        box-shadow: 5px 5px 15px rgb(184, 184, 184);
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;

    }

    .container_menu h2 {
        color: #ffffff;
        align-items: center;
    }

    .container_logo{

        position: absolute; 
        right: 5%; 
        top: 2%;
        z-index: 2;
        background-color:transparent;



    }

    .container_logo img{
        margin: 0;
        padding: 0%;
        height: 59px;
        width: 228px;
    }

    .container_registro{
        border-style:groove;
        border-right: #ffffff;
        border-bottom: #ffffff;
        width: 35%;
        border-top: none;
        border-left: none;
        border-color: #ffffff;
        position: absolute;
        right: 35%; 
        top: 5%; 
        z-index: 1;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        border-radius: 2%;
        box-shadow: 5px 5px 30px rgb(203, 202, 202);
    }

    .container_registro form{
        width: 80%;

    }

    .container_registro input{
        height: 40px;
        width: 120%;
        box-sizing: border-box;
        padding:10px 5px;
        margin: 5px 0;
        text-align:left;

        background-color:transparent;
        color: #302e2e;
        border-top: none;
        border-right:none;
        border-left: none;
        border-color: #8d9596;

    }

    .container_registro input:focus {
        background-color: #ffffff;
        color: #000000;
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

    .container_registro select {
     background-color: #ffffff;
     border: none;
     height: 35px;
     padding: 5px 30px;
     width: 100%;
     color: #7ec544;
     text-align: left;
     border-radius: 10px;
    }

    ::placeholder { 
        color: #7ec544;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        
    }
    .container_registro button{
        width: 120%;
        height: 80px;
        color: #ffffff;
        background: #13c0e5;
        border: 1px;
        border-radius: 10px;
        padding: 10px 20px;
        margin: 50px 0;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        font-size: large;
    }

    .container_registro button:hover{
        color: #7ec544;
        background: #037e8c;
        border: 0px;
    }

</style>

