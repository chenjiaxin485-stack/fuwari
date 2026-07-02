<script>
  import { onMount } from 'svelte';

  let username = $state('');
  let password = $state('');
  let error = $state('');
  let showLogin = $state(true);

  onMount(() => {
    if (sessionStorage.getItem('authenticated') === 'true') {
      showLogin = false;
    } else {
      document.body.style.overflow = 'hidden';
    }
  });

  function login() {
    if (username === 'admin' && password === 'laochen666') {
      sessionStorage.setItem('authenticated', 'true');
      showLogin = false;
      document.body.style.overflow = '';
      error = '';
    } else {
      error = '账号或密码错误';
    }
  }

  function handleKeydown(e) {
    if (e.key === 'Enter') {
      login();
    }
  }
</script>

{#if showLogin}
  <div class="login-overlay">
    <div class="login-card">
      <div class="login-avatar">🐱</div>
      <h1 class="login-title">老陈の小站</h1>
      <p class="login-subtitle">请输入密码以继续访问</p>
      <div class="login-form">
        <input
          type="text"
          class="login-input"
          placeholder="账号"
          bind:value={username}
          onkeydown={handleKeydown}
        />
        <input
          type="password"
          class="login-input"
          placeholder="密码"
          bind:value={password}
          onkeydown={handleKeydown}
        />
        <button class="login-btn" onclick={login}>登 录</button>
        {#if error}
          <p class="login-error">{error}</p>
        {/if}
      </div>
    </div>
  </div>
{/if}

<style>
  .login-overlay {
    position: fixed;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    background: oklch(0.95 0.01 var(--hue, 345));
    z-index: 99999;
  }

  :global(.dark) .login-overlay {
    background: oklch(0.16 0.014 var(--hue, 345));
  }

  .login-card {
    text-align: center;
    padding: 2.5rem 2rem;
    border-radius: 1rem;
    background: white;
    box-shadow: 0 4px 24px oklch(0.70 0.14 var(--hue, 345) / 0.15);
    width: 100%;
    max-width: 360px;
  }

  :global(.dark) .login-card {
    background: oklch(0.23 0.015 var(--hue, 345));
    box-shadow: 0 4px 24px oklch(0.50 0.14 var(--hue, 345) / 0.15);
  }

  .login-avatar {
    font-size: 3rem;
    margin-bottom: 0.5rem;
  }

  .login-title {
    font-size: 1.5rem;
    font-weight: 700;
    margin: 0 0 0.25rem;
    color: oklch(0.55 0.12 var(--hue, 345));
  }

  .login-subtitle {
    font-size: 0.875rem;
    color: oklch(0.50 0.02 var(--hue, 345));
    margin: 0 0 1.5rem;
  }

  .login-form {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }

  .login-input {
    padding: 0.65rem 1rem;
    border: 1px solid oklch(0.85 0.02 var(--hue, 345));
    border-radius: 0.5rem;
    font-size: 0.95rem;
    outline: none;
    transition: border-color 0.2s;
    background: oklch(0.98 0.005 var(--hue, 345));
    color: oklch(0.25 0.02 var(--hue, 345));
  }

  :global(.dark) .login-input {
    background: oklch(0.28 0.015 var(--hue, 345));
    border-color: oklch(0.35 0.02 var(--hue, 345));
    color: oklch(0.90 0.01 var(--hue, 345));
  }

  .login-input:focus {
    border-color: oklch(0.70 0.14 var(--hue, 345));
  }

  .login-btn {
    padding: 0.65rem;
    border: none;
    border-radius: 0.5rem;
    background: oklch(0.70 0.14 var(--hue, 345));
    color: white;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.2s;
    letter-spacing: 0.25em;
  }

  .login-btn:hover {
    background: oklch(0.60 0.16 var(--hue, 345));
  }

  .login-error {
    color: #e53e3e;
    font-size: 0.875rem;
    margin: 0;
  }
</style>
