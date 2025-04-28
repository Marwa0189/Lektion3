<script>
	import { goto } from '$app/navigation';
	let userName = '';
	let password = '';
	let errorMessage = '';
	let isLoading = false;

	const handleLogin = async () => {
		errorMessage = '';
		isLoading = true;

		// Simulerer lidt ventetid (du kan fjerne hvis du vil)
		await new Promise((resolve) => setTimeout(resolve, 1000));

		if (userName.trim() === 'admin' && password.trim() === 'admin') {
			goto('/home');
		} else {
			errorMessage = 'Forkert brugernavn eller kodeord.';
			isLoading = false;
		}
	};
</script>
<div class="grid place-content-center h-80">
	<div class="card p-4 shadow" style="max-width: 400px; width: 100%;">
		<h2 class="text-center mb-4">Login</h2>

		<form on:submit|preventDefault={handleLogin}>
			<div class="mb-3">
				<label for="username" class="form-label">Brugernavn</label>
				<input
					id="username"
					type="text"
					class="form-control"
					bind:value={userName}
					placeholder="Indtast brugernavn"
					required
				/>
			</div>

			<div class="mb-3">
				<label for="password" class="form-label">Kodeord</label>
				<input
					id="password"
					type="password"
					class="form-control"
					bind:value={password}
					placeholder="Indtast kodeord"
					required
				/>
			</div>

			{#if errorMessage}
				<div class="alert alert-danger" role="alert">
					{errorMessage}
				</div>
			{/if}

			<div class="d-grid">
				<button type="submit" class="btn btn-primary" disabled={isLoading}>
					{#if isLoading}
						<span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
						<span class="ms-2">Logger ind...</span>
					{:else}
						Login
					{/if}
				</button>
			</div>
		</form>
	</div>
</div>
