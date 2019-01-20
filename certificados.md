---
layout: page
title: Certificados
subtitle: Verifica tu certificado por su código
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
				var emb2 = '" width="800" height="550" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen></iframe>';
				messageBox.innerHTML = emb1 + myJson[codeInput.value] + emb2;
				codeInput.value = "";
			});
	}
</script>