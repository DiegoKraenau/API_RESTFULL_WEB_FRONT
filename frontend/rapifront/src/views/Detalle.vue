<template>
   <html lang="en">
<head>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
</head>
<body>

    <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
    <a class="navbar-brand" href="#">RapiSolver</a>
  <ul class="navbar-nav">
    <li class="nav-item">
      <a class="nav-link" href="#">Mi perfil</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="#">Publicar Servicio</a>
    </li>
     <li class="nav-item">
      <a class="nav-link" href="#">Buscar Servicio</a>
    </li>
     <li class="nav-item">
      <a class="nav-link" href="#">Buscar Personas</a>
    </li>
  </ul>
</nav>
<br>
<div class="container">
		<h2>Detalles del Servicio</h2>
		<div class="card" id="card1">
			<div class="card-header text-white bg-secondary">Datos Servicio</div>
			<div class="card-body">
				<h3>Servicio:</h3>
				<ul class="list-group" v-for="detalle in detalles" :key="detalle.serviceDetailsId">
					<li class="list-group-item">Nombre:  {{detalle.serviceName}}</li>
					<li class="list-group-item">Categoria:  {{detalle.categoryName}}</li>
					<li class="list-group-item">Costo:  {{detalle.cost}}</li>
          <li class="list-group-item">Descripcion:  {{detalle.description}}</li>
				</ul>
				<br>
			
				<a  :href="'/listarServicios'" class="btn btn-success">Regresar</a>
			</div>
		</div>
	</div>

 <div class="card" id="cardSupplier">
   <div class="card-header text-white bg-secondary">Datos Proveedor</div>
              <img src="../assets/img_avatar.png" alt="Avatar" style="width:100%">
                 <div class="container"  v-for="detalle in detalles" :key="detalle.serviceDetailsId">
                         <h4><b>{{detalle.name}}</b></h4> 
                        <h6>Puntaje</h6>
                          <span class="fa fa-star checked"></span>
                          <span class="fa fa-star checked"></span>
                          <span class="fa fa-star checked"></span>
                          <span class="fa fa-star"></span>
                          <span class="fa fa-star"></span>
                          <br>
                          <br>
                        <a :href="'/perfil/' + detalle.supplierId +'/'+ id2" class="btn btn-primary">Ver perfil</a>
                        <br>
                        <br>
                 </div>     
   </div>


</body>
</html>
</template>

<script>
import axios from 'axios'
export default {
  data(){
        return{
      detalles:null,
      id2:this.$route.params.id2

        }
    },
    mounted(){
        this.getDetalles();
    },
    methods:{
        getDetalles(){
            axios.
                get("https://localhost:5001/api/ServiceDetails/"+this.$route.params.id)
                    .then(response=>{
                        this.detalles=response.data
                    })
                    .catch(e=>console.log(e))
        }
    }
}
</script>

<style>
.checked {
  color: orange;
}
#cardSupplier{
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
   width: 20%;
  max-width: 300px;
  height: 300px;
  top: -390px;
  left: 1000px;
}
#card1 {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 50%;
}
img_avatar.png
.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.container {
  padding: 2px 16px;
}
</style>