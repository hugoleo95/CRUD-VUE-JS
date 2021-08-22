<template>
<div class="container">
	<div class="card">
		<div class="card-header">
			Empleados
		</div>
		<div class="card-body">
		<table class="table">
		<tr>
			<td>ID</td>
			<td>NOMBRE</td>
			<td>CORREO</td>
			<td>OPCIONES</td>
		</tr>
		<tbody>
		<tr v-for="empleado in empleados" :key="empleado.id"><!-- indico la llave es id -->
			<td>{{empleado.id}}</td>
			<td>{{empleado.nombre}}</td>
			<td>{{empleado.correo}}</td>
			<td>
				<div class="btn-group" role="group" aria-label="">
			<router-link class="btn btn-primary" :to="{name:'Editar',params:{id:empleado.id}}">Editar</router-link>
			<button type="button" class="btn btn-danger" v-on:click="borrarEmpleado(empleado.id)">Borrar</button>	
				</div>
			
			</td>
		</tr>
		</tbody>
	</table>	
		</div>
		
	</div>
	
</div>

</template>

<script type="text/javascript">
	export default {
		data(){
		return {
		empleados:[]
			}
		},
		created:function(){

			this.consultarEmpleados();//llamo a mi metodo
		},
		methods:{
			//http://localhost/empleados-main/api-empleados.php
			consultarEmpleados(){
				fetch('http://localhost/empleados-main/api-empleados.php')
				.then(respuesta=>respuesta.json())//aqio recibimos la respueta de json
				.then((datosRespuesta)=>{//aqui creamos una  variable para recibir los datos
					console.log(datosRespuesta)//mostramos por consola
				
				this.empleados=[]
				if(typeof datosRespuesta[0].success==='undefined'){//aqui veo si el arreglo no viene vacio
					this.empleados=datosRespuesta;//si hay se asigna a variable empleados

				}
				})
				.catch(console.log)
			},
			borrarEmpleado(id){
				console.log(id);
				fetch('http://localhost/empleados-main/index.php?borrar='+id)
				.then(respuesta=>respuesta.json())//aqio recibimos la respueta de json
				.then((datosRespuesta)=>{//aqui creamos una  variable para recibir los datos
					console.log(datosRespuesta)//mostramos por consola
				
				window.location.href="Listar"
				})
				.catch(console.log)
			}
		}
}
</script>

<style scoped type="text/css">
	
</style>