<script>
    import "../app.css";
    import { goto } from '$app/navigation';

    function navigateToSignUp() {
    goto('/users/new');
    }

    function navMain() {
    goto('/');
    }

    function navLogin() {
    goto('/users/sign-in');
    }
  </script>

<button on:click={navMain}>Main Page</button>
<button on:click={navigateToSignUp}>Sign Up</button>
<button on:click={navLogin}>Sign In</button>

  <slot />