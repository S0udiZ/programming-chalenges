<script lang="ts">
  import { AppShell, Divider, LightSwitch } from '@skeletonlabs/skeleton';

  import { writable } from 'svelte/store';

  import maleNames from "./assets/maleNames.json";
  import femaleNames from "./assets/femaleNames.json";
  import surnames from "./assets/surnames.json";
  import titles from "./assets/titles.json";

  const gender = writable(1);
  const credentials = writable(false);

  const firstName = writable('');
  const lastName = writable('');
  const title = writable('');

  function GenerateName() {

    if ($gender == 1) {
      $firstName = maleNames[Math.floor(Math.random() * maleNames.length)];
    }
    else if ($gender == 2) {
      $firstName = femaleNames[Math.floor(Math.random() * femaleNames.length)];
    }
    else {
      if (Math.floor(Math.random()*2)) {
        $firstName = maleNames[Math.floor(Math.random() * maleNames.length)];
      }
      else {
        $firstName = femaleNames[Math.floor(Math.random() * femaleNames.length)];
      }
    }

    $lastName = surnames[Math.floor(Math.random() * surnames.length)];

    $title = titles[Math.floor(Math.random() * titles.length)];
  }

</script>

<AppShell>
	<div id="page" class="container mx-auto p-8 space-y-8">
    <LightSwitch class="absolute top-5 right-16" />
    <h1 class="text-5xl text-center">Name Generator</h1>
    <Divider />
    <div class="space-y-3">
      <label for="gender">
        <span>Choose your gender</span>
        <select name="gender" id="gender" bind:value={$gender}>
          <option value={1}>Male</option>
          <option value={2}>Female</option>
          <option value={3}>Other</option>
        </select>
      </label>
      <label for="credentials">
        <span>Job title</span>
        <select name="credentials" id="credentials" bind:value={$credentials}>
          <option value={false}>No</option>
          <option value={true}>Yes</option>
        </select>
      </label>
      <div class="text-center">
        <button class="border-8 border-accent-500 p-2 px-8 rounded-full text-lg mt-3" on:click={GenerateName}>
          Generate
        </button>
      </div>
    </div>
    <Divider />
    <div class="text-center space-y-2">
      <h2 class="text-3xl">Your name is</h2>
      <div class="">
        <h1 class="text-5xl">{$firstName} {$lastName}</h1>
        {#if $credentials}
          <p>{$title}</p>
        {/if}
      </div>
  </div>
</AppShell>

<style>
  select {
    @apply p-2 px-4
  }
</style>