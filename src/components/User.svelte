<script>
  import { fade } from 'svelte/transition';

  const getUserData = async () => {
    await new Promise((r) => setTimeout(r, 3000));

    return {
      name: 'Edgar',
      likes: 123456,
      followers: 6,
      likedThings: ['Biscoito treloso', 'JS', 'Gato'],
    }
  };
</script>

{#await getUserData()}
  <p>Loading...</p>
{:then { name, likes, followers, likedThings }}
  <div transition:fade="{{ duration: 2000 }}">
    <p>Nome: {name}</p>
    <p>Likes: {likes}</p>
    <p>Seguidores: {followers}</p>

    {#if followers >= 10}
      <p>Blogueira famosa</p>
    {:else if likes >= 5}
      <p>Pelo menos tu tem like</p>
    {:else}
      <p>Sad times</p>
    {/if}

    <ul>
      {#each likedThings as thing}
        <li>{thing}</li>
      {:else}
        <li>Não tem itens na lista</li>
      {/each}
    </ul>
  </div>
{:catch err}
  <p>Lascou: {err}</p>
{/await}
