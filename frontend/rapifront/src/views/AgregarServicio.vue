<template>
  <html lang="en">
<head>
</head>
<body>

 <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
  <a class="navbar-brand" href="#">RapiSolver</a>
  <ul class="navbar-nav">
    <li class="nav-item">
      <a class="nav-link" href="#">Mi perfil</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="" >Publicar Servicio</a>
    </li>
     <li class="nav-item">
      <a class="nav-link" href="#">Buscar Servicio</a>
    </li>
     <li class="nav-item">
      <a class="nav-link" href="#">Buscar Personas</a>
    </li>
  </ul>
</nav>

<div id="labelCrearUsuario"><h2>Registro Servicio</h2></div><br>
	<form id="formulario" >
		<div class="form-group" >
			<label >Nombre:</label> <input type="text" class="form-control col-lg-3 col-md-3 col-xs-12" placeholder="Ingrese nombre del servicio" v-model="servicio.name"> 
		</div>
		<div class="form-group" >
			<label >Descripcion:</label> <br><textarea  class="form-control col-lg-3 col-md-3 col-xs-12" name="comentarios" rows="10" cols="40" v-model="servicio.description">Escribe aquí tus comentarios</textarea>   
		</div>
		<div class="form-group" >
			<label >Costo:</label> <input type="text" class="form-control col-lg-3 col-md-3 col-xs-12" placeholder="Ingrese el costo del servicio" v-model="servicio.cost" > 
		</div>
        <div class="form-group" >
			<label >Categoria:</label><br>
           <select class="browser-default custom-select form-control col-lg-3 col-md-3 col-xs-12" v-model="servicio.categoryName">
                <option selected >Seleccion la categoria</option>
                <option v-for="categoria in categorias" :key="categoria.serviceCategoryId">{{categoria.categoryName}}</option>
            </select>
		</div>
		<div class="form-group" >
			
		</div>
         <button v-on:click.prevent="post" class="btn btn-primary">Agregar</button>
	</form>


</body>
</html>
</template>

<script>
import axios from 'axios'
export default {
 data(){
        return{
            servicio:{
                 name: "",
                 description: "",
                 cost: "",
                 categoryName: ""
            },
            categorias:null,
            supplier:null,
            servicioDetalle:{
                supplierId: "",
                usuarioId: "",
                serviceName: "",
                description: "",
                cost: "",
                categoryName: ""
            }

        }
    },
    mounted(){
        this.getCategorias();
        this.getSupplier();
    },
    methods:{
        getCategorias(){
            axios.
                get('https://localhost:5001/api/ServiceCategory')
                    .then(response=>{
                        this.categorias=response.data;
                        console.log(this.$route.params.id)
                        
                    })
                    .catch(e=>console.log(e))
        },
        getSupplier(){
            axios.
                get("https://localhost:5001/api/Supplier/"+this.$route.params.id)
                    .then(response=>{
                        this.supplier=response.data
                    })
                    .catch(e=>console.log(e))
        },
        post:function(){
            this.$http.post('https://localhost:5001/api/ServiceDetails',{
                supplierId: parseInt(this.$route.params.id),
                serviceName: this.servicio.name,
                description: this.servicio.description,
                cost: this.servicio.cost,
                categoryName: this.servicio.categoryName

            }).then(function(data){
                alert ("Se ha registrado con exito.");
                console.log(data);
            });
        }
    }
}
</script>

<style>
#formulario {
	position: relative !important;
	left: 30% !important;
}
#labelCrearUsuario{
	position: relative !important;
	left: 30% !important;
}

</style>