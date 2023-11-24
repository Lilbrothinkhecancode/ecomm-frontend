<script>
    import "../app.css";
    import { goto } from '$app/navigation';

    function navigateToSignUp() {
    goto('/users/new');
    }

    function navMain() {
    goto('/');
    }

    function navAbout() {
    goto('/about');
    }
  </script>

<button on:click={navMain}>Main Page</button>
<button on:click={navigateToSignUp}>Sign Up</button>

  <slot />