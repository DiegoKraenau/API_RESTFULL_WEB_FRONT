<template>
   <html lang="en">
<head>
</head>
<body>
	

    <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
    <a class="navbar-brand" href="" v-on:click.prevent="rapi">RapiSolver</a>
  <ul class="navbar-nav">
    <li class="nav-item">
      <a class="nav-link" href="" v-on:click.prevent="miperfil">Mi perfil</a>
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

<br/>
<br/>


	<div class="container">
		<div class="card">
			<div class="card-header text-white bg-secondary" >Buscar Servicios</div>
			<div class="card-body">
                <div class="form-inline">
					<form >
						<div class="row">
							<div class="col-8">
								<input  type="text" class="form-control" id="servicioNombre" name="servicioNombre" placeholder="Buscar por nombre"  v-model="busqueda.nombre">
							</div>
							<div class="col">
								<button type="submit" class="btn btn-danger"  v-on:click.prevent="buscar">Buscar</button>
							</div>
						</div>
					</form>
                </div>	
				<br>
				<input type="radio"  v-on:click.prevent="ordenarBajoCosto" > Ordenar por bajo Costo<br>
			</div>
			
				<div class="table responsive">
					<table class="table table-striped">
						<thead class="thead-dark">
							<tr>
								<th>Id</th>
								<th>Nombre</th>
								<th>Categoria</th>
								<th>Cost</th>
								<th>Detalle</th>								
							</tr>
						</thead>
						<tbody>
							<tr v-for="detalle in detalles" :key="detalle.serviceDetailsId">
								<td >{{detalle.serviceDetailsId}}</td>
								<td >{{detalle.serviceName}}</td>
								<td >{{detalle.categoryName}}</td>
								<td >{{detalle.cost}}</td>
								<td><a :href="'/detalle/' + detalle.serviceDetailsId +'/'+ id2" class="btn btn-success">Detallle</a>
								</td>								
							</tr>
						</tbody>
					</table>
				</div>
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
			busqueda:{
				nombre:""
			},
			id2:this.$route.params.id

        }
    },
    mounted(){
        this.getDetalles();
    },
    methods:{
        getDetalles(){
            axios.
                get('https://localhost:5001/api/servicedetails')
                    .then(response=>{
                        this.detalles=response.data
                    })
                    .catch(e=>console.log(e))
		},
		buscar:function(){
			this.detalles=null;
            axios.
                get('https://localhost:5001/api/servicedetails/'+this.busqueda.nombre+'/servicios')
                    .then(response=>{
                        this.detalles=response.data
                    })
                    .catch(e=>console.log(e))
		},
		ordenarBajoCosto:function(){

			var value = document.getElementById('servicioNombre').value;
            if (value.lenght == 0) {
                    axios.
                get('https://localhost:5001/api/servicedetails/all/lowcost')
                    .then(response=>{
                        this.detalles=response.data
                    })
                    .catch(e=>console.log(e))
            } 
			
			if (value.lenght != 0) {
                   axios.
                get('https://localhost:5001/api/servicedetails/'+this.busqueda.nombre+'/lowcostAndname')
                    .then(response=>{
                        this.detalles=response.data
                    })
                    .catch(e=>console.log(e))
            } 
        },
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
		},
        miperfil:function(){
			window.location.href="/miPerfil/"+this.$route.params.id
        }
    }

}
</script>

<style>

</style>