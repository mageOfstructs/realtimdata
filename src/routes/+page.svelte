<script lang="ts">
  import { Doc } from "sveltefire";
  import { getFirestore } from "firebase/firestore";
  import { initializeApp } from "firebase/app";
  import { doc, setDoc } from "firebase/firestore";

  const app = initializeApp(/* your firebase config */);
  const firestore = getFirestore();
</script>

<Doc ref={"posts/id"} let:data>
  <p>{data?.counter}</p>
  <p slot="loading">Loading...</p>
</Doc>
