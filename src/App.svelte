<script lang="ts">
  import type { User } from '@auth0/auth0-spa-js';
  import { withAuth } from './auth';

  const auth = withAuth();

  // a variable to hold the authentication details
  let user: User;
  // update the local store of auth details when they change
  auth.user.subscribe((userAuth) =>{
    user = userAuth;
  } )

  let token = "";
  auth.token.subscribe(t => {
    token = t;
  })
</script>

<main>
  <div>
    {#if !user}
    <button on:click={auth.login}>Login</button>
    {:else}
    <button on:click={auth.logout}>Logout</button>
    <h1>Hello {user.nickname}</h1>
    <div class="profile">
      <img class="profile" src={user.picture} alt="User profile">
    </div>
    <p>User:</p>
    <pre>
      {JSON.stringify(user, null, 2)}
    </pre>
    <p>Access Token:
    </p>
    <p> Don't display access tokens. </p>
    <pre>{token}</pre>

    {/if}
  </div>
</main>

<style>
  *{
    box-sizing: border-box;
  }
button{
  padding:1rem;
  background-color:  aqua;
  color:black;
  transition: background-color 500ms ease;
}
button:hover{
  background-color: aquamarine;

}
pre{
  max-width: 100%;
word-wrap: break-word;
text-align: left;
}
img.profile{
  border-radius: 50%;
  border: 0.5rem solid aqua;
  opacity: 0.8;
  transition: opacity 500ms ease, border-color 500ms ease;
}
img.profile:hover{
  opacity: 1;
  border-color: aquamarine;
}
div.profile{
  margin:1rem;
}
pre{
  opacity: 0.5;
  border: 1px solid black;
  transition: opacity 500ms ease, border-color 500ms ease;
  padding:1rem;
  white-space: pre-wrap;
}
pre:hover{
  opacity: 1;
  border-color: aquamarine;
}


</style>