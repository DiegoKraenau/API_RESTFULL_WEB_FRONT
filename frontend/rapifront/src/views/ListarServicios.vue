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

<br/>
<br/>


	<div class="container">
		<div class="card">
			<div class="card-header text-white bg-secondary">SERVICIOS</div>
			<div class="card-body">
                <div class="form-inline">
					<form >
						<div class="row">
							<div class="col-8">
								<input id="inputServicioNombre" type="text"
								class="form-control" name="servicioNombre"
								placeholder="Buscar por nombre">
							</div>
							<div class="col">
								<button type="submit" class="btn btn-danger">Buscar</button>
							</div>
						</div>
					</form>
                        <div class="col">
							<button type="button" class="btn btn-success" data-toggle="modal" data-target="#myModal">Nuevo</button>
				
                     <div id="myModal" class="modal fade" role="dialog">
                        <div class="modal-dialog">
                         <!-- Registra nuevo servicio-->
                            <div class="modal-content">
                              <div class="modal-header">
                                 
                                 <h4 class="modal-title">Servicio</h4>
                                 <button type="button" class="close" data-dismiss="modal">&times;</button>
                              </div>
                                <div class="modal-body">
								<p>Nombre Servicio</p>
                                <input id="nombre" type="text" class="form-control" name="servicioNombre">
                                <p> Descripcion </p>
                                <input id="descripcion" type="text" class="form-control" name="servicioDescripcion">
                                <p> Costo </p>
                                <input id="costo" type="text" class="form-control" name="servicioCosto">
                                <p> Categoria </p>
                                <input id="categoria" type="text" class="form-control" name="servicioCategoria">
                                </div>
                            <div class="modal-footer">
                                <button type="button" class="btn btn-primary" data-dismiss="modal">Registrar</button>
                                <button type="button" class="btn btn-danger" data-dismiss="modal">Cancelar</button>

                            </div>
                     </div>

  </div>
</div>
                        
                        
                        
                        </div>
                </div>	
			</div>
				<div class="table responsive">
					<table class="table table-striped">
						<thead class="thead-dark">
							<tr>
								<th>Id</th>
								<th>Nombre</th>
								<th>Categoria</th>
								<th>Costo</th>
								<th>Detalle</th>								
							</tr>
						</thead>
						<tbody>
							<tr v-for="detalle in detalles" :key="detalle.serviceDetailsId">
								<td >{{detalle.serviceDetailsId}}</td>
								<td >{{detalle.serviceName}}</td>
								<td >{{detalle.categoryName}}</td>
								<td >{{detalle.cost}}</td>
								<td><a :href="'/detalle/' + detalle.serviceDetailsId" class="btn btn-success">Detalle</a>
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
            search:"",
            editedIndex: -1,


            //Model
            id:"",
            nombreServicio:"",
            descripcionServicio:"",
            costoServicio:"",
            categoriaServicio:""
        
        };
    },
    mounted(){
        this.getDetalles();
    },
    methods:{
        getDetalles(){
            axios.
                get('https://localhost:5001/api/ServiceDetails')
                    .then(response=>{
                        this.detalles=response.data
                    })
                    .catch(e=>console.log(e))
        },

    
        close(){
            this.dialog = false;
        },

        limpiar(){
            this.id = "";
            this.nombreServicio = "";
            this.descripcionServicio="";
            this.costoServicio = "";
            this.categoriaServicio = "";
        },
        guardar(){
            let me = this;

            axios.post("api/Servicio",{

                nombreServicio : me.nombreServicio,
                
            })
        }


    }

}
</script>

<style>

</style>