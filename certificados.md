---
layout: page
title: Certificados
subtitle: Verifica tu certificado con su código
---
<center>
	<input id="code" type="text">
	<input type="submit" value="Verificar" onclick="insert()" />
	<p></p>
	<div id="display"></div>
</center>

<script type="text/javascript">
	function insert(){
		fetch("../codes.json")
			.then(function(response){
				return response.json();
			})
			.then(function(myJson){
				var codeInput = document.getElementById("code");
				var messageBox = document.getElementById("display");
				var emb1 = '<iframe src="';
				var emb2 = '" width="837" height="650" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>';
				if(myJson[codeInput.value] !== undefined){
					messageBox.innerHTML = '<font color="green">CÓDIGO VÁLIDO\n</font>'
					messageBox.innerHTML += emb1 + myJson[codeInput.value] + emb2;
				} else{
					messageBox.innerHTML = '<font color="red">CÓDIGO INVÁLIDO</font>';
				}
				codeInput.value = "";
			});
	}
</script>