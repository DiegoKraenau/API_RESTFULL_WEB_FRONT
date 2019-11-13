<template>
<html lang="en">
<head>
    <!-- Custom fonts for this template -->
<link href="../static/vendor/fontawesome-free/css/all.min.css" rel="stylesheet"
	type="text/css">
<link href="https://fonts.googleapis.com/css?family=Montserrat:400,700"
	rel="stylesheet" type="text/css">
<link href='https://fonts.googleapis.com/css?family=Kaushan+Script'
	rel='stylesheet' type='text/css'>
<link
	href='https://fonts.googleapis.com/css?family=Droid+Serif:400,700,400italic,700italic'
	rel='stylesheet' type='text/css'>
<link
	href='https://fonts.googleapis.com/css?family=Roboto+Slab:400,100,300,700'
	rel='stylesheet' type='text/css'>

<!-- Custom styles for this template -->
<link href="../static/css/agency.min.css" rel="stylesheet">
</head>
<body>

<nav class="navbar navbar-expand-sm bg-dark navbar-dark">
  <a class="navbar-brand" id="logo" href="http://localhost:8080/Inicio">RapiSolver</a>
  <ul class="navbar-nav">
    <li class="nav-item">
      <a class="nav-link" href="http://localhost:8080/Inicio">Inicio Sesion</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">¿Quienes somos?</a>
    </li>
  </ul>
</nav>
    <div id="mensaje2" class="alert alert-success " style="display: none">
            <strong> <p class="padd-top" id="mensaje"></p></strong>
    </div>
    <div id="labelCrearUsuario"><h2>Registro de Usuario</h2></div><br>
 
	<form id="formulario" v-on:submit.prevent="post" >
        
		<div class="form-group" >
			<label >Nombre:</label> <input type="text" class="form-control col-lg-3 col-md-3 col-xs-12" placeholder="Ingrese Nombres" v-model="usuario.name" minlength="5" maxlength="40" required pattern="[A-Za-z]+"> 
		</div>
		<div class="form-group" >
			<label >Apellido:</label> <input type="text" class="form-control col-lg-3 col-md-3 col-xs-12" placeholder="Ingrese Apellidos" v-model="usuario.lastName"  minlength="5" maxlength="40" required pattern="[A-Za-z]+">  
		</div>
		<div class="form-group" >
			<label >Email:</label> <input type="email" class="form-control col-lg-3 col-md-3 col-xs-12" placeholder="Ingrese un email" v-model="usuario.email"> 
		</div>
        <div class="form-group" >
			<label >Contraseña::</label> <input type="password" class="form-control col-lg-3 col-md-3 col-xs-12" placeholder="Ingrese una contraseña" v-model="usuario.contraseña" minlength="5" maxlength="40" > 
		</div>

        <button  tyoe="submit"  class="btn btn-primary">Agregar</button>
	</form>




</body>
</html>
</template>

<script>
export default {
    data(){
        return{
            usuario:{
                 name: "",
                 lastName: "",
                 email: "",
                 phone: "",
                 age: "",
                 genger: "",
                 country: "",
                 state: "",
                 city: "",
                 address: "",
                 contraseña:""
            }

        }
    },
    methods:{
        post:function(){
            this.$http.post('https://localhost:5001/api/customers',{
                 name: this.usuario.name,
                 lastName: this.usuario.lastName,
                 email: this.usuario.email,
                 phone: this.usuario.phone,
                 age: this.usuario.age,
                 genger: this.usuario.genger,
                 country: this.usuario.country,
                 state: this.usuario.state,
                 city: this.usuario.city,
                 address: this.usuario.address,
                 contraseña:this.usuario.contraseña

            }).then(function(data){
                document.getElementById('mensaje2').style.display ='block'
                 document.getElementById('mensaje').innerHTML = 'Se acaba de registrar con exito , si desea inicie sesion.';
                 document.getElementById("formulario").reset();
                console.log(data);
            });
        },
        salir:function(){
         window.location.href="/Inicio"
        }
    }

}
</script>

<style>
#formulario {
	position: relative !important;
	left: 30% !important;
}

#ImagenLogo{
	width:400px;
    height:250px;
    border-radius:150px;
    position: relative !important;
	left: 30% !important;
    
}
#labelCrearUsuario{
	position: relative !important;
	left: 30% !important;
}
#logo {
    color: #fed136;
    font-family: 'Kaushan Script',-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif,'Apple Color Emoji','Segoe UI Emoji','Segoe UI Symbol','Noto Color Emoji';
}
#logo {
    display: inline-block;
    padding-top: .3125rem;
    padding-bottom: .3125rem;
    margin-right: 1rem;
    font-size: 1.25rem;
    line-height: inherit;
    white-space: nowrap;
}
</style>