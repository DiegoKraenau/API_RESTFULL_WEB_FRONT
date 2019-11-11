<template>
  <html lang="en">
<head>
</head>
<body>

 <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
  <a class="navbar-brand" href=""  v-on:click.prevent="rapi">RapiSolver</a>
  <ul class="navbar-nav">
    <li class="nav-item">
      <a class="nav-link" href="" v-on:click.prevent="miperfil">Mi perfil</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" href="" >Publicar Servicio</a>
    </li>
     <li class="nav-item">
      <a class="nav-link" href="" v-on:click.prevent="buscarServicio">Buscar Servicio</a>
    </li>
     <li class="nav-item">
       <a class="nav-link" href="" v-on:click.prevent="buscarPersonas">Buscar Personas</a>
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
            },
            usuario:null

        }
    },
    mounted(){
        this.getCategorias();
        this.getSupplier();
        this.getUsuario();
    },
    methods:{
        getCategorias(){
            axios.
                get('https://localhost:5001/api/servicecategories')
                    .then(response=>{
                        this.categorias=response.data;
                        
                    })
                    .catch(e=>console.log(e))
        },
        getSupplier(){
            axios.
                get("https://localhost:5001/api/suppliers/searchOrginalByUserId/"+this.$route.params.id)
                    .then(response=>{
                        this.supplier=response.data
                    })
                    .catch(e=>console.log(e))
        },
        getUsuario(){
            axios.
                get("https://localhost:5001/api/rapiusers/"+this.$route.params.id)
                    .then(response=>{
                        this.usuario=response.data;
                        if(this.usuario.rolId==1){
                            alert("Usted no tiene una subscripcion para poder publicar servicios");
                            window.location.href="/Principal/"+this.$route.params.id
                        }
                        
                    })
                    .catch(e=>console.log(e))
        },
        post:function(){
            this.$http.post('https://localhost:5001/api/servicedetails',{
                supplierId: parseInt(this.supplier.supplierId),
                serviceName: this.servicio.name,
                description: this.servicio.description,
                cost: this.servicio.cost,
                categoryName: this.servicio.categoryName

            }).then(function(data){
                alert ("Se ha registrado con exito.");
                console.log(data);
            });
        },
        rapi:function(){
            window.location.href="/Principal/"+this.$route.params.id
        },
        buscarServicio:function(){
            window.location.href="/listarServicios/"+this.$route.params.id
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
#formulario {
	position: relative !important;
	left: 30% !important;
}
#labelCrearUsuario{
	position: relative !important;
	left: 30% !important;
}

</style>