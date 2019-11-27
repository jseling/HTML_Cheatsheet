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
		<h1>GitHub<h1>
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
			//const myPromise = axios.get('https://api.github.com/users/jersonSeling/repos')
			//myPromise.then(...).catch(...)
		
			axios.get('https://api.github.com/users/jersonSeling/repos')
			.then((response) => {
				console.log(response)				
				response.data.forEach(repository => {addRepository(repository)})						
			})
			.catch((error) => {
				console.log(error)
			})
		}
		
		const axiosAsAsyncAwait = async () => {
			const response = await axios.get('https://api.github.com/users/jersonSeling/repos')
			
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
			fetch('https://api.github.com/users/jersonSeling/repos')
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
			const response = await fetch('https://api.github.com/users/jersonSeling/repos')
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
		
		//axiosAsPromise()
		//axiosAsAsyncAwait()
		//fetchAsPromise()
		fetchAsAsyncAwait()
		
	</script>
  </body>
</html>
```
