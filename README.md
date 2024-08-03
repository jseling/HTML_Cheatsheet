HTML Cheatsheet

# Basic structure

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Page Title</title>
    <meta name="description" content="Roughly 155 characters">
    <link rel="stylesheet" type="text/css" href="mystyle.css">
    <script src="myscript.js"></script>
  </head>
  <body>
    <!-- Content -->
  </body>
</html>
```

# Javascript, DOM, Axios, Promises and Async/Await

```html
<!DOCTYPE html>
<html lang="pt-br">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>JS Cheatcheet</title>
  </head>
  
  <body>
	<div class='mainDiv'>
		<h1>GitHub</h1>
	</div>
	
	<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
	
	<script>
		//Axios documentation: https://github.com/axios/axios
	
		const mainDiv = document.querySelector('.mainDiv')
		
		const addRepository = (repository) => {				
			const newRepository = document.createElement('div')
			const newRepositoryStars = document.createElement('p')
			const newRepositoryLink = document.createElement('a')			
			
			newRepository.textContent  = repository.name
			
			newRepositoryStars.textContent  = 'Stars: ' + repository.stargazers_count
			
			newRepositoryLink.textContent = 'Link'
			newRepositoryLink.href = repository.html_url			
			
			newRepository.appendChild(newRepositoryStars)
			newRepository.appendChild(newRepositoryLink)
			
			mainDiv.appendChild(newRepository)			
		}

		const axiosAsPromise = () => {
			//const myPromise = axios.get('https://api.github.com/users/jSeling/repos')
			//myPromise.then(...).catch(...)
		
			axios.get('https://api.github.com/users/jSeling/repos')
			.then((response) => {
				console.log(response)				
				response.data.forEach(repository => {addRepository(repository)})						
			})
			.catch((error) => {
				console.log(error)
			})
		}
		
		const axiosAsAsyncAwait = async () => {
			const response = await axios.get('https://api.github.com/users/jSeling/repos')
			
			try
			{
				console.log(response)				
				response.data.forEach(repository => {addRepository(repository)})						
			}
			catch (error)
			{
				console.log(error)
			}
		}	

		const fetchAsPromise = () => {
			fetch('https://api.github.com/users/jSeling/repos')
			.then(response => response.json())
			.then((data) => {
				console.log(data)				
				data.forEach(repository => {addRepository(repository)})						
			})
			.catch((error) => {
				console.log(error)
			})
		}	

		const fetchAsAsyncAwait = async () => {
			const response = await fetch('https://api.github.com/users/jSeling/repos')
			const data = await response.json()
			
			try
			{
				console.log(data)				
				data.forEach(repository => {addRepository(repository)})						
			}
			catch (error)
			{
				console.log(error)
			}			

		}	
		const xhrModern = () => {
			//https://dev.to/attacomsian/introduction-to-xmlhttprequest-xhr-142j
			//http://zetcode.com/javascript/xmlhttprequest/
			
			const xhr = new XMLHttpRequest()
			
			xhr.onload = () => {
				if (xhr.status == 200) {
					const data = JSON.parse(xhr.response)				
					console.log(data);
					data.forEach(repository => {addRepository(repository)})
					
				} else {
					console.error('Error: ' + xhr.status)
				}
			}
			
			xhr.onerror = (error) => {
				console.error(error)
			}			
		
			xhr.open('GET', 'https://api.github.com/users/jSeling/repos')
			xhr.send();
		}	
		
		
		//axiosAsPromise()
		axiosAsAsyncAwait()
		//fetchAsPromise()
		//fetchAsAsyncAwait()
		//xhrModern()
		
	</script>
  </body>
</html>
```

## Old XMLHTTPRequest

```html
<!DOCTYPE html>
<html lang="pt-br">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>JS Cheatcheet</title>
  </head>
  
  <body>
    <div class = "mainDiv" >
		<h1>GitHub</h1>
	</div>
	
	<script>
		const mainDiv = document.querySelector('.mainDiv')
		
		var addRepository = function (repository) {				
			const newRepository = document.createElement('div')
			const newRepositoryStars = document.createElement('p')
			const newRepositoryLink = document.createElement('a')			
			
			newRepository.textContent  = repository.name
			
			newRepositoryStars.textContent  = 'Stars: ' + repository.stargazers_count
			
			newRepositoryLink.textContent = 'Link'
			newRepositoryLink.href = repository.html_url			
			
			newRepository.appendChild(newRepositoryStars)
			newRepository.appendChild(newRepositoryLink)
			
			mainDiv.appendChild(newRepository)			
		}
		
		var xhrOld = function(){
			//http://www.linhadecodigo.com.br/artigo/922/o-objeto-xmlhttprequest.aspx
			
			var getXHR = function() {
				if (window.XMLHttpRequest){
					console.log("XHR Native");
					return new XMLHttpRequest() //Opera, FireFox, IE 10+, etc
				} else {
					console.log("XHR ActiveX Object");
					return new ActiveXObject("Microsoft.XMLHTTP") //IE < 10
				}
			
			}
			
			const xhr = getXHR()
			
			xhr.onreadystatechange = function(){
				if (xhr.readyState == 4) {
				
					//JSON.parse IE 8+ https://caniuse.com/#feat=json
					//https://stackoverflow.com/questions/1787020/json-object-in-ie6-how/1788251
					
					const responseData = JSON.parse(xhr.responseText) 
					console.log(responseData)
					
					for (var i = 0; i < responseData.length; i++){
						var repository = responseData[i]
						addRepository(repository)						
					}
					
				}
			}		
		
			xhr.open('GET', 'https://api.github.com/users/jSeling/repos', true)
			xhr.send(null);
		}
		
		xhrOld()		

	</script>
  </body>
</html>
```
