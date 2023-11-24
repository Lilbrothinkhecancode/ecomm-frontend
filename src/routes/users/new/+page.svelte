<script>
    import { goto } from '$app/navigation';
    let formErrors = {};

    function postSignUp() {
      const successMessage = "Sign-up successful!";
      window.alert(successMessage);
      goto('/');
    }

    async function createUser(evt) {
      evt.preventDefault()
      console.log('Password:', evt.target['password'].value);
      console.log('Password confirmation:', evt.target['password-confirmation'].value);
      if (evt.target['password'].value != evt.target['password-confirmation'].value) {
        console.log(formErrors);
        formErrors = { ...formErrors, password: { message: 'Password confirmation does not match' } };
        console.log(formErrors);
        return;
      }
  
      const userData = {
        name: evt.target['name'].value,
        email: evt.target['email'].value,
        password: evt.target['password'].value,
        passwordConfirm: evt.target['password-confirmation'].value
      };
  
      console.log(userData);

      const resp = await fetch('http://localhost:8080/users', {
        method: 'POST',
        mode: 'cors',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(userData)
      });
  
      if (resp.status == 200) {
        goto('/');
  
        if (res.success) {
          postSignUp();
        } else {
          throw 'Sign up succeeded but authentication failed';
        }
      } 
    }
  </script>

<div class="text-center">
    <a class="link-hover italic text-xs" href="/users/login">Already have an account? Click here to login instead.</a>
</div>
<div class="flex justify-center items-center mt-8">
    <form on:submit={createUser} class="w-1/3">
        <div class="form-control w-full">
            <label class="label" for="name">
                <span>Username</span>
            </label>
            <input type="text" name="name" placeholder="johndoe" class="input input-bordered w-full" />
            {#if 'name' in formErrors}
            <label class="label" for="name">
                <span class="label-text-alt text-red-500">{formErrors['name'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="email">
                <span>Email</span>
            </label>
            <input type="email" name="email" placeholder="john@example.com" class="input input-bordered w-full" required />
            {#if 'email' in formErrors}
            <label class="label" for="email">
                <span class="label-text-alt text-red-500">{formErrors['email'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="password">
                <span>Password</span>
            </label>
            <input type="password" name="password" placeholder="" class="input input-bordered w-full" required />
            {#if 'password' in formErrors}
            <label class="label" for="password">
                <span class="label-text-alt text-red-500">{formErrors['password'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full">
            <label class="label" for="password">
                <span>Confirm Password</span>
            </label>
            <input type="password" name="password-confirmation" placeholder="" class="input input-bordered w-full" required />
            {#if 'password' in formErrors}
            <label class="label" for="password">
                <span class="label-text-alt text-red-500">{formErrors['password'].message}</span>
            </label>
            {/if}
        </div>

        <div class="form-control w-full mt-4">
            <button class="btn btn-md">Create an Account</button>
        </div>
    </form>
</div>