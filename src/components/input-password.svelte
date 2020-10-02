<!-- SPDX-License-Identifier: MIT
     Copyright (c) 2020 Kim Il Yong -->

<ListInput
    input={true}
    outline={outline}
    label="{label}"
    floatingLabel="{floatingLabel}"
    type="{passwordType}"
    clearButton="{clearButton}"
    id="{id}"
    inputId="REMOVEDINPUT"
    value="{password}"
    onInputClear="{(e) => {password = ""; clearButtonVisible = false; thisInput.focus();}}"  
    onFocus={onFocus}
    onBlur={onBlur}
    onInputNotempty={onInputNotempty}
    onInputEmpty={onInputEmpty}
  >
      <div slot="input" style="display:flex;flex-direction: row;justify-content: flex-end;align-items:stretch;min-height: inherit;">
          <div style="flex: 1 1 90%;">               
            {#if passwordVisible} 
                <input type="text" bind:value="{password}" bind:this={thisInput} id={inputId} 
                on:input="{(e) => onInput(e)}"
                on:change="{(e) => onChange(e)}"
                >
            {:else}
                <input type="password" bind:value="{password}" bind:this={thisInput} id={inputId} 
                on:input="{(e) => onInput(e)}"
                on:change="{(e) => onChange(e)}"
                >
            {/if}
          </div>           
          <div style="max-width:2em;margin-right:3px;flex: 0 0 5%;display:flex;justify-content:center;align-items:center;z-index:2;cursor:pointer;">
            <div class="f7-icons password-eye-button" on:click="{(e) => togglePasswordHidden(e)}">{eyeStyle}</div>
          </div>
          {#if clearButtonVisible}
            <div style="max-width:1.5em;flex: 0 0 5%;justify-content:center;align-items:center;">              
            </div>
          {/if}
      </div>
</ListInput>

<style>

    .password-eye-button
    {        
        z-index: 1;
        color: var(--f7-input-clear-button-color);
        font-size: 22px;
        transition-duration: 100ms;
        pointer-events: visible;
        -webkit-tap-highlight-color: rgba(0, 0, 0, 0);        
        -webkit-font-smoothing: antialiased;
    }
</style>

<script>
    import {
      List,    
      ListItem,
      ListInput, 
    } from 'framework7-svelte';
    import { tick } from 'svelte';
  
    export let passwordVisible = false;
    export let password;
    export let label;
    export let floatingLabel = true;
    export let clearButton = false;
    export let outline = true;
    export let id;
    export let inputId;
    export let clearButtonVisible = false;
    export let onFocus;
    export let onBlur;
    export let onInputNotempty;
    export let onInputEmpty;

    let thisInput;
    let passwordType = "password";    
    let eyeStyle = "eye_slash";

    function passwordChanged(e) {
      password = e.target.value;
    }
    async function togglePasswordHidden(e) {
      if (passwordVisible) {
        passwordType = "password";
        passwordVisible = false;        
        eyeStyle = "eye_slash";
      } else {
        passwordType = "text";
        passwordVisible = true;        
        eyeStyle = "eye";
      }
      await tick();
      thisInput.focus();
    }
    function onInput(e) {      
      thisInput.blur();
      thisInput.focus();
    }
    function onChange(e) {      
      if ( thisInput.className.includes("input-with-value")) {
        clearButtonVisible = true;  
      } else {
        clearButtonVisible = false;
      }
    }  
  </script>
