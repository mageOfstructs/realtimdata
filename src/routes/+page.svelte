<script lang="ts">
  import { Doc } from "sveltefire";
  import { getFirestore } from "firebase/firestore";
  import { initializeApp } from "firebase/app";
  import { doc, setDoc } from "firebase/firestore";

  const app = initializeApp(/* your firebase config */);
  const firestore = getFirestore(app);

  const DATA_PATH = "testing/123";

  function updateDb(path: string, data: Object) {
    setDoc(doc(firestore, path), data);
  }

  let inputObj = { name: "", password: "" };
</script>

<Doc ref={DATA_PATH} let:data>
  <form action="" class="grid grid-rows-3 gap-3 place-content-center m-4">
    <label class="label">Username: </label>
    <input class="input" type="text" bind:value={inputObj.name} required />
    <label class="label">Password: </label>
    <input
      class="input"
      type="password"
      bind:value={inputObj.password}
      required
    />
    <button
      class="btn variant-filled"
      on:click={() => {
        let obj = { ...data };
        obj[inputObj.name] = inputObj.password;
        updateDb(DATA_PATH, obj);
        inputObj = { name: "", password: "" };
      }}>Test</button
    >
  </form>
  <p class="center" slot="loading">Loading...</p>
</Doc>
