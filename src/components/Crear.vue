<template>

<div class="container">
<div class="card">
		<div class="card-header">
			Agregar Nuevo Empleado
		</div>
		<div class="card-body">
		<form v-on:submit.prevent="agregarRegistro()"><!-- llamamos a la funcion  -->
			<div class="form-group">
				<label for="nombre">Nombre:</label>
				<input type="text" required="required" class="form-control" v-model="empleado.nombre" name="nombre" id="nombre" aria-describedby="helpId" placeholder="Nombre">
				<small id="helpId" class="form-text text-muted">Escribe el nombre del empleado</small>
				
			</div>
			<div class="form-group">
				<label for="nombre">Correo:</label>
				<input type="text" required="required" class="form-control" v-model="empleado.correo" name="correo" id="correo" aria-describedby="helpId" placeholder="Correo">
				<small id="helpId" class="form-text text-muted">Escribe el correo del empleado</small>
				
			</div>
			<div class="btn-group" role="group" arial-label="">

			<button type="submit" class="btn btn-success">Agregar</button>
			

			<router-link :to="{name: 'Listar'}" class="btn btn-warning">Cancelar</router-link>
				
			</div>
		</form>
		</div>
	</div>

</div>

</template>

<script type="text/javascript">
	export default {

		data(){
			return{
				empleado:{//el objeto

				}
			}
		},
		methods:{
			agregarRegistro(){//funcion para agregar
				console.log(this.empleado);

				var datosEnviar={nombre:this.empleado.nombre,correo:this.empleado.correo}//asignamos los datos a variables

				fetch('http://localhost/empleados-main/index.php?insertar=1', {//funciones de php
					method:"POST",//por el metodo post php
					body:JSON.stringify(datosEnviar)//se envia a la url
				})
				.then(respuesta=>respuesta.json())//aqio recibimos la respueta de json
				.then((datosRespuesta=>{
					console.log(datosRespuesta);
					window.location.href='Listar'//para que vaya al listar
				}))
			}
		}
}
</script>

<style scoped type="text/css">
	
</style>