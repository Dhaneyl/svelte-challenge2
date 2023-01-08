<script>
  let password = '';
  let passwordState = 'short';
  let lists =[]
$: if(password.trim().length < 5){
  passwordState = 'short';
}else if(password.trim().length > 10){
  passwordState = 'long'
} else{
  passwordState = 'valid'
}

const passwordList = () =>{
  if(passwordState === 'valid'){
    lists = [ ...lists, password];
  }
 
}
const removedPassword = (index) =>{
  lists = lists.filter((pw, idx)=>{
    return idx !== index;
  });
}

  
</script>

<main>
  <input type="password" bind:value="{password}"/>
  <button on:click={passwordList}>add password</button>
 
</main>

{#if passwordState === 'short'}
<p>Password too short</p>
{:else if passwordState === 'long'}
<p>password too long</p>
{:else if passwordState === 'valid'}
<p> password: {password}</p>

{/if}

 <ul>
{#each lists as list, i}
  <li on:click={removedPassword.bind(this, i)}>{list}</li>
{/each}
</ul>