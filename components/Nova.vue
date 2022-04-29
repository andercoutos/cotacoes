<template>
<div>
<span id="valor">hello world</span>
<script src="https://code.jquery.com/jquery-3.5.0.js"></script>
<script>
function verValor() {
	var url="https://rest.coinapi.io/v1/exchangerate/BTC/USD?apikey=FD3DD3DE-FD89-4F89-B5CB-49F798890CEC";
	$.getJSON( url, function( json ) {
		$('#valor').html('Bitcoin = $' + json.rate);
	});
}
</script>
<br>
<button onclick="verValor()">Ver valor do Bitcoin</button>
</div>
</template>
