<script>
import { onMount } from "svelte";

	let data = []

	onMount(async () => {
		const res = await fetch('http://localhost:3333')
		data = await res.json()
	})

	const generateRandomHex = () => Math.random().toString(16).slice(2, 8)
</script>

<main id="main">
	<figure class="logo-container">
		<img src="/ghibli.png" alt="studio ghibli logo" class="logo">
	</figure>

	<div class="filmes">
		{#each data as filme}
			<article class="filme">
				<div class="filme-title" style={`background-image: linear-gradient(to left, #${generateRandomHex()}, #${generateRandomHex()})`}>
					<h2>{filme.title}</h2>
				</div>

				<div class="image-description">
					<p class="description">{filme.description}</p>
					<img src={filme.image_url} alt={filme.title}>
				</div>

				<h3>{'Director: ' + filme.director}</h3>
				<p class="release_date">{'Release Date: ' + filme.release_date}</p>
				<p class="rt_score">{'Rotten Tomatoes: ' + filme.rt_score}</p>
			</article>
		{/each}
	</div>
</main>

<style>

.logo{
  width: 50rem;
  margin: 50px auto;
}

.filmes {
    width: 100%;
    max-width: 130rem;
    margin: 4rem auto;

    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(40rem, 1fr));
    justify-items: center;
    grid-gap: 4rem;
}

.logo-container{
    display: grid;
    place-items: center;
    width: 100%;
}

.filme {
    width: 40rem;
    border-radius: 8px;
}

.filme-title {
    color: white;
    text-align: center;
    padding: 5px;
    font-size: 1.5rem;
    border-radius: 8px;
    position: relative;
    z-index: 0;
}

h2{
  z-index: 999;
  display: block;
}

.release_date,
.rt_score,
h3 {
    font-size: 1.6rem;
    padding: 8px;
    font-weight: 600;
    color: rgb(255, 255, 255);
    border-radius: 8px;
}

h3 {
    background-image: linear-gradient(to left, rgb(255, 142, 142), rgb(255, 116, 181));
}

.release_date {
    background-image: linear-gradient(to left, rgb(142, 210, 255), rgb(116, 255, 220));
}

.rt_score {
    background-image: linear-gradient(to left, rgb(255, 142, 142), rgb(255, 155, 116));
}


.image-description img{
    width: 100%;
    position: relative;
}

.description {
    border: 2px solid white;
    padding: 1rem;

    font-weight: 600;
    color: rgb(255, 249, 249);
    font-size: 1.5rem;
    text-align: center;
    line-height: 1.3;
    z-index: 100;
}
</style>