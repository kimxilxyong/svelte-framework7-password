<Page name="home">
 
  <!-- Page content -->
  <Block strong>
    <p>Here is your blank Framework7 app. Let's see what we have here.</p>
  </Block>

  <BlockTitle>Password ListInputPassword {password} </BlockTitle>
  <List>
    <ListInputPassword label="Test Passwort label" clearButton={true} bind:password={password}>
    </ListInputPassword>
  </List>

  <BlockTitle>Navigation {password} </BlockTitle>
  <List>
    <ListItem link="/about/" title="About"/>
    <ListItem link="/form/" title="Form"/>
  </List>

  
</Page>
<script>
  import {
    Page,
    Block,
    BlockTitle,
    List,    
    ListItem,
    ListInput,
  } from 'framework7-svelte';

  import ListInputPassword from '../components/input-password.svelte';

  let password;



</script>