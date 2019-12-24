<script>
  import { getClient } from "svelte-apollo";
  import gql from "graphql-tag";

  let username = "";
  let password = "";

  const LOGIN_MUTATION = gql`
    mutation Login($username: String!, $password: String!) {
      login(username: $username, password: $password)
    }
  `;

  const client = getClient();

  async function signIn() {
    const { data } = await client.mutate({
      mutation: LOGIN_MUTATION,
      variables: {
        username,
        password
      }
    });
    const { login: token } = data;
  }
</script>

<style>
  .input {
    margin: 1em 0;
  }
</style>

<div class="ui container">
  <div class="ui card fluid">
    <div class="content">
      <a class="header" href="/">Game Geek</a>
      <div class="description">Please login.</div>
      <form on:submit|preventDefault={signIn}>
        <div class="ui input fluid">
          <input
            type="text"
            class="ui input"
            placeholder="Username"
            bind:value={username} />
        </div>
        <div class="ui input fluid">
          <input
            type="password"
            class="ui input"
            placeholder="Password"
            bind:value={password} />
        </div>
        <button type="submit" class="ui primary button">Login</button>
      </form>
    </div>
  </div>
</div>
