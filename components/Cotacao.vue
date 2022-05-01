<template>
	<div>


	<div class="flex justify-center">
	  <div class="mb-3 xl:w-96">
	    <label for="exampleFormControlInput1" class="form-label inline-block mb-2 text-gray-700" >Nome do ativo</label>
	    <input
		onkeyup="autocompletar()"
		type="text" name="ativo" id="ativo" placeholder="Digite o nome do ativo"
	      class="form-control block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none">

		  <ul id="list" class="bg-white rounded-lg border border-gray-200 w-96 text-gray-900">

		  </ul>
	<script>

	async function autocompletar(){
	const list = document.getElementById('list');
		var entrada=document.getElementById('ativo').value.trim().toLowerCase();
		if(entrada.length<1){
			list.innerHTML='';
		}
		const response = await fetch(
			"ativos.json"
		);
		const ativos = await response.json();

		ativos.forEach((ativo) => {
		      if(entrada == ativo.nome.toLowerCase() || entrada == ativo.codigo.toLowerCase()){
		        const li = document.createElement('li');
				li.className='px-6 py-2 border-b border-gray-200 w-full';
		        li.innerHTML= `<a href="javascript:adicionarALista('${ativo.nome}','${ativo.codigo}')">${ativo.nome} (${ativo.codigo})</a>`;
		        list.appendChild(li);
		      }
		    });


	}


	</script>
	  </div>
	</div>


	<br>
	<div class="flex space-x-2 justify-center">
	<button onclick="adicionarALista()" type="button" class="inline-block px-6 py-2.5 bg-blue-600 text-white font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-blue-700 hover:shadow-lg focus:bg-blue-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-blue-800 active:shadow-lg transition duration-150 ease-in-out">
	Adicionar a lista
	</button>
	</div>
<br><br>
	<div class="flex justify-center">
	<ul id="listaDeAtivos" class="bg-white rounded-lg border border-gray-200 w-96 text-gray-900">
	</ul>
	</div>

	<script>
	async function adicionarALista(nome,codigo){
		const list = document.getElementById('list');
		list.innerHTML='';
		if(!codigo){
			var codigo=document.getElementById("ativo").value;

			const response = await fetch(
				"ativos.json"
			);
			const ativos = await response.json();

			ativos.forEach((ativo) => {
		      if(codigo.toLowerCase() == ativo.nome.toLowerCase() || codigo.toLowerCase() == ativo.codigo.toLowerCase()){
			  	codigo=ativo.codigo;
				nome=ativo.nome;
		      }
		    });

		}
		document.getElementById("ativo").value='';
		const response = await fetch(
		//codigo+".json"
		"https://rest.coinapi.io/v1/exchangerate/"+codigo+"/USD?apikey=081284B6-2E06-4BAF-97BA-18265DAE4751"
		);
		const json = await response.json();
		var html=document.getElementById('listaDeAtivos').innerHTML;
		var valor='<li class="px-6 py-2 border-b border-gray-200 w-full">'+nome+' ('+codigo+') $' + json.rate+'</li>';
		document.getElementById('listaDeAtivos').innerHTML=html+valor
	}
	adicionarALista('Bitcoin','BTC');
	</script>
	</div>
</template>
