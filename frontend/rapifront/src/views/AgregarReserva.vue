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

<div id="labelCrearUsuario"><h2>Registro Reserva</h2></div><br>
<form id="formulario" >
		<div class="form-group" >
			<label >Descripcion:</label> <br><textarea  class="form-control col-lg-3 col-md-3 col-xs-12" name="comentarios" rows="10" cols="40" v-model="reserva.note">Escribe aquí tus comentarios</textarea>   
		</div>
        <div class="form-group" >
			<label >Fecha:</label><br>
           <input class="form-control col-lg-3 col-md-3 col-xs-12" type="date" name="fecha" v-model="reserva.fecha">
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
             reserva:{
                 servicioId:"",
                 usuarioId:"",
                 supplierId:"",
                 fecha:"",
                 note:""
             },
             detalles:null

        }
    },
  mounted(){
        this.getDetalles();
  },  
  methods:{
        rapi:function(){
			window.location.href="/Principal/"+this.$route.params.id2
        },
        buscarServicio:function(){
			window.location.href="/listarServicios/"+this.$route.params.id2
        },
        publicarServicio:function(){
			window.location.href="/agregarServicio/"+this.$route.params.id2
         },
        buscarPersonas:function(){
			window.location.href="/buscarPersonas/"+this.$route.params.id2
        },
        miperfil:function(){
			window.location.href="/miPerfil/"+this.$route.params.id2
        },
        getDetalles(){
            axios.
                get("https://localhost:5001/api/servicedetails/searchByID/"+this.$route.params.id)
                    .then(response=>{
                        this.detalles=response.data;                        
                    })
                    .catch(e=>console.log(e))
        },
        post:function(){
            
            this.$http.post('https://localhost:5001/api/reservations',{
                servicioId: parseInt(this.detalles.servicioId),
                usuarioId: parseInt(this.$route.params.id2),
                note: this.reserva.note,
                supplierId: parseInt(this.detalles.supplierId),
                fecha: this.reserva.fecha

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