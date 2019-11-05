<template>
  <html lang="en">
<head>
</head>
<body>

 <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
    <a class="navbar-brand" href="#" v-on:click.prevent="rapi">RapiSolver</a>
  <ul class="navbar-nav">
    <li class="nav-item">
      <a class="nav-link" href="#">Mi perfil</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#"  v-on:click.prevent="publicarServicio">Publicar Servicio</a>
    </li>
     <li class="nav-item">
      <a class="nav-link" href="" v-on:click.prevent="buscarServicio">Buscar Servicio</a>
    </li>
     <li class="nav-item">
      <a class="nav-link" href="" v-on:click.prevent="buscarPersonas">Buscar Personas</a>
    </li>
  </ul>
</nav>


<br>
<br>
<br>
<h2 style="text-align:center">Paquete de membresía</h2>
<p style="text-align:center">Escoge tu paquete ideal para publicar tus servicios</p>

<div class="columns">
  <ul class="price">
    <li class="header">Basic</li>
    <li class="grey">30 S/ por 1 mes</li>
    <li>Poder publicar servicios ilimitados durante 1 mes</li>
    <li>No existe descuento</li>
 
    <li class="grey"><a href="#" class="button">Sign Up</a></li>
  </ul>
</div>

<div class="columns">
  <ul class="price">
    <li class="header" style="background-color:#4CAF50">Pro</li>
    <li class="grey">160 S/ por 6 meses</li>
    <li>Poder publicar servicios ilimitados durante 6 mes</li>
    <li>Existe un descuento de 20 soles</li>
 
    <li class="grey"><a href="#" class="button">Sign Up</a></li>
  </ul>
</div>

<div class="columns">
  <ul class="price">
    <li class="header">Premium</li>
    <li class="grey">320 S/ por 1 año</li>
    <li>Poder publicar servicios ilimitados durante 1 año</li>
    <li>Existe un descuento de 40 soles</li>
 
    <li class="grey"><a href="#" class="button">Sign Up</a></li>
  </ul>
</div>


</body>
</html>
</template>

<script>
export default {
methods:{
        rapi:function(){
			window.location.href="/Principal/"+this.$route.params.id
        },
        buscarServicio:function(){
			window.location.href="/listarServicios/"+this.$route.params.id
        },
        publicarServicio:function(){
			window.location.href="/agregarServicio/"+this.$route.params.id
    },
    buscarPersonas:function(){
			window.location.href="/buscarPersonas/"+this.$route.params.id
        }
    }
}
</script>

<style>
* {
  box-sizing: border-box;
}

.columns {
  float: left;
  width: 33.3%;
  padding: 8px;
}

.price {
  list-style-type: none;
  border: 1px solid #eee;
  margin: 0;
  padding: 0;
  -webkit-transition: 0.3s;
  transition: 0.3s;
}

.price:hover {
  box-shadow: 0 8px 12px 0 rgba(0,0,0,0.2)
}

.price .header {
  background-color: #111;
  color: white;
  font-size: 25px;
}

.price li {
  border-bottom: 1px solid #eee;
  padding: 20px;
  text-align: center;
}

.price .grey {
  background-color: #eee;
  font-size: 20px;
}

.button {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 10px 25px;
  text-align: center;
  text-decoration: none;
  font-size: 18px;
}

@media only screen and (max-width: 600px) {
  .columns {
    width: 100%;
  }
}
</style>