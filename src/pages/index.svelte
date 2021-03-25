<script>
  import RoutifyIntro from "./example/_components/RoutifyIntro.svelte";
  import { metatags } from "@roxi/routify";
  metatags.title = "My Routify app";
  metatags.description = "Description coming soon...";
  import { FirebaseApp, User, Doc, Collection } from "sveltefire";

  import firebase from "firebase/app";
  import "firebase/firestore";
  import "firebase/auth";
  //   import "firebase/performance";
  //   import "firebase/analytics";

  // For Firebase JS SDK v7.20.0 and later, measurementId is optional
  const firebaseConfig = {
    apiKey: "AIzaSyD7edhlGOLeE2uKbbs4bKi1uFhMKLk4ayI",
    authDomain: "tichat.firebaseapp.com",
    projectId: "tichat",
    storageBucket: "tichat.appspot.com",
    messagingSenderId: "561811199163",
    appId: "1:561811199163:web:49c9359ea12e0d6f67059e",
    measurementId: "G-G5XEKYZZK8",
  };

  firebase.initializeApp(firebaseConfig);
</script>

<main>
  {#if !firebaseConfig.projectId}
    <strong>Step 0</strong>
    Create a
    <a href="https://firebase.google.com/">Firebase Project</a>
    and paste your web config into
    <code>App.svelte</code>
    .
  {/if}

  <!-- 1. 🔥 Firebase App -->
  <FirebaseApp {firebase}>
    <h1>💪🔥 Mode Activated</h1>

    <p>
      <strong>Tip:</strong>
      Open the browser console for development logging.
    </p>

    <!-- 2. 😀 Get the current user -->
    <User let:user let:auth>
      Howdy 😀! User
      <em>{user.uid}</em>

      <button on:click={() => auth.signOut()}>Sign Out</button>

      <div slot="signed-out">
        <button on:click={() => auth.signInAnonymously()}>
          Sign In Anonymously
        </button>
      </div>

      <hr />

      <!-- 3. 📜 Get a Firestore document owned by a user -->
      <Doc path={`posts/${user.uid}`} let:data={post} let:ref={postRef} log>
        <h2>{post.title}</h2>

        <p>
          Document created at <em
            >{new Date(post.createdAt).toLocaleString()}</em
          >
        </p>

        <span slot="loading">Loading post...</span>
        <span slot="fallback">
          <button
            on:click={() =>
              postRef.set({
                title: "📜 I like Svelte",
                createdAt: Date.now(),
              })}
          >
            Create Document
          </button>
        </span>

        <!-- 4. 💬 Get all the comments in its subcollection -->

        <h3>Comments</h3>
        <Collection
          path={postRef.collection("comments")}
          query={(ref) => ref.orderBy("createdAt")}
          let:data={comments}
          let:ref={commentsRef}
          log
        >
          {#if !comments.length}
            No comments yet...
          {/if}

          {#each comments as comment}
            <p>
              <!-- ID: <em>{comment.ref.id}</em> -->
            </p>
            <p>
              {comment.text}
              <button on:click={() => comment.ref.delete()}>Delete</button>
            </p>
          {/each}

          <button
            on:click={() =>
              commentsRef.add({
                text: "💬 Me too!",
                createdAt: Date.now(),
              })}
          >
            Add Comment
          </button>

          <span slot="loading">Loading comments...</span>
        </Collection>
      </Doc>
    </User>
  </FirebaseApp>
</main>

<!-- Styles -->
<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1,
  em {
    color: #ff3e00;
  }

  hr {
    height: 1px;
    border: none;
    background: rgb(195, 195, 195);
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
