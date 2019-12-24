<script>
	import ApolloClient from 'apollo-boost';  
	import { setClient } from 'svelte-apollo';
	
	import LoginCard from './components/LoginCard.svelte';
	
	const client = new ApolloClient({ uri: 'http://localhost:8888/graphql' });
  setClient(client);
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <LoginCard />
</main>
