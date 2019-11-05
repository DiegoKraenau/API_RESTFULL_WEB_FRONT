<template>
 <html lang="en">
<head>
</head>
<body>

 <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
    <a class="navbar-brand" href="#" v-on:click.prevent="rapi">RapiSolver</a>
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

<div id="labelCrearUsuario"><h2>Editar Servicio</h2></div><br>
<form id="formulario" >
		<div class="form-group" >
			<label >Nombre:</label> <input  type="text" id="lbl1" class="form-control col-lg-3 col-md-3 col-xs-12"  placeholder="Ingrese nombre del servicio"  v-model="servicio.name"> 
		</div>
		<div class="form-group" >
			<label >Descripcion:</label> <br><textarea id="lbl2" class="form-control col-lg-3 col-md-3 col-xs-12" name="comentarios" rows="10" cols="40" v-model="servicio.description">Escribe aquí tus comentarios</textarea>   
		</div>
		<div class="form-group" >
			<label >Costo:</label> <input type="text" id="lbl3" class="form-control col-lg-3 col-md-3 col-xs-12" placeholder="Ingrese el costo del servicio" v-model="servicio.cost" > 
		</div>
        <div class="form-group" >
			<label >Categoria:</label><br>
           <select class="browser-default custom-select form-control col-lg-3 col-md-3 col-xs-12" v-model="servicio.categoryName">
                <option selected >Seleccion la categoria</option>
                <option  v-for="categoria in categorias" :key="categoria.serviceCategoryId">{{categoria.categoryName}}</option>
            </select>
		</div>
		<div class="form-group" >
			
		</div>
         <button v-on:click.prevent="edit" class="btn btn-primary">Editar</button>
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
            serviciobefore:null

        }
    },
    mounted(){
        this.getCategorias();
        this.getServicio();
        
    },
    methods:{
        getCategorias(){
            axios.
                get('https://localhost:5001/api/ServiceCategories')
                    .then(response=>{
                        this.categorias=response.data;
                        
                    })
                    .catch(e=>console.log(e))
        },
        getServicio(){
            axios.
                get('https://localhost:5001/api/ServiceDetails/'+this.$route.params.id2)
                    .then(response=>{
                        this.serviciobefore=response.data;
                        console.log(response.data)
                        document.getElementById('lbl1').value =response.data[0].serviceName;
                        document.getElementById('lbl2').value =response.data[0].description;
                        document.getElementById('lbl3').value =response.data[0].cost;
                      
                    })
                    .catch(e=>console.log(e))
             
        },
        post:function(){
            this.$http.post('https://localhost:5001/api/ServiceDetails',{
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
        },
        edit:function(){
             this.$http.put('https://localhost:5001/api/Servicios',{
                servicioId: parseInt(this.$route.params.id2),
                name: this.servicio.name,
                description: this.servicio.description,
                cost: this.servicio.cost,
                categoryName:this.servicio.categoryName

            }).then(function(data){
                alert ("Se ha editado con exito.");
                window.location.href="/miPerfil/"+this.$route.params.id
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