<script>
  export let platform;

  let sudah_login = true;
  let email = "";

  if (!localStorage.email) {
    sudah_login = false;
  }

  function login() {
    fetch("https://zen.mabaiz.web.id/add-email", {
      method: "post",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        email,
        platform,
      }),
    });
    sudah_login = true;
    localStorage.email = email;
  }
</script>

{#if !sudah_login}
  <div class="w-full h-full fixed top-0 p-5 left-0 bg-gray-200 z-[9999]">
    <div class="card bg-base-100 shadow-xl w-full">
      <div class="card-body">
        <form on:submit|preventDefault={login} action="">
          <label class="form-control w-full mb-3">
            <div class="label">
              <span class="label-text">Login with email</span>
            </div>
            <input
              type="email"
              required
              bind:value={email}
              placeholder="Type here"
              class="input input-bordered w-full"
            />
          </label>
          <button class="btn btn-secondary">Login</button>
        </form>
      </div>
    </div>
  </div>
{/if}
