<script>
import { onMount } from "svelte";
import { writable } from 'svelte/store';
let proxy = "https://cors-anywhere.herokuapp.com/"
let url= proxy+'https://www.talenteca.com/api/v1/membership-plans'
//let url='https://jsonplaceholder.typicode.com/users'
let users=[];

const usuarios = async ()=>{
	const res=await fetch(url);
	
	users = await res.json()
	
	if (res.ok){
		console.log(users)
		return users;
	}else{
		throw new Error ('Error')
	}
}




let promise=usuarios();


let list = [
		{
			cantidad:'',
			precio:''
		}
]

let name = 'world';




const manejador = (e)=>{
	console.log("envio id")
}


</script>



<style>
	
</style>

<main>

{#await promise}
	 <h1>liadong</h1>
{:then users} 
	
	
	

	<form on:submit|preventDefault={manejador}>
			
			<table class="default">

				<tr>
			  
				  <td>ID</td>
			  
				  <td>Nombre</td>
			  
				  <td>Numero de unidades</td>

				  <td>Precio por unidad USD</td>

				  <td>Total usd</td>

				  <td>Precio por unidad MXN</td>

				  <td>Total MXN</td>

				  <td>Actualizar</td>

			  
				</tr>
			
				{#each users as item}
				<tr>
					
					
				  <td>{item.id}</td>
				 
				  <td>{item.name}</td>

				
				  <td><input type="text" id="cantidad" name="ncantidad" bind:value="{item.number_of_units}"></td>
				

				  {#each item[4],[item.prices] as item1}
				  	
				  		<td>{item1[0].per_unit}</td>
				  		<td>{item1[0].total}</td>

						
						<td><input type="text" id="numUni" name="numUni" bind:value="{item1[1].per_unit}"></td>
						<td><input type="text" id="TotalMx" name="TotalMx" value="{item1[1].total}"></td>
						
						<p> {item.number_of_units * item1[1].per_unit}</p>
				  {/each}
				        
				</tr>
				{/each}
				
			
			  </table>
			</form>
{/await}





</main>

