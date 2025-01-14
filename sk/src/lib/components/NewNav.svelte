<script>
	import NavLinks from "./NavLinks.svelte";
	import { MenuIcon as MobileMenuIcon } from "lucide-svelte";

	let atTop = false;
	let showDrawer = false;

	function handleScroll() {
		atTop = window.pageYOffset >= 30;
	}
</script>

<svelte:window on:scroll={handleScroll} />

<div
	class="navbar-wrapper sticky top-0 z-10 bg-opacity-95 lg:backdrop-blur {atTop
		? 'border-base-content/10 border-b'
		: 'border-transparent'}"
>
	<div class="container">
		<nav class="navbar font-medium">
			<div class="navbar-start gap-2">
				<div class="flex-none lg:hidden">
					<label
						for="my-drawer"
						class="btn btn-square btn-ghost h-12 w-12 p-0 text-xl text-current shadow-none"
						aria-label="open sidebar"
					>
						<MobileMenuIcon />
					</label>
				</div>

				<!-- Brand -->
				<a href="#" class="text-lg font-bold tracking-tighter">SaaS Landing</a>
			</div>

			<div class="navbar-center hidden lg:flex">
				<ul class="menu menu-horizontal gap-2">
					<NavLinks />
				</ul>
			</div>

			<div class="navbar-end">
				<ul class="menu menu-horizontal gap-3">
					<li>
						<button
							class="btn btn-primary btn-soft"
							on:click={() => window.register_modal.showModal()}
						>
							Register
						</button>
					</li>
					<li>
						<button
							class="btn btn-primary"
							on:click={() => window.login_modal.showModal()}
						>
							Login
						</button>
					</li>
				</ul>
			</div>
		</nav>

		<!-- Mobile drawer -->
		<div class="drawer lg:hidden">
			<input id="my-drawer" type="checkbox" class="drawer-toggle" bind:checked={showDrawer} />
			<div class="drawer-side">
				<label for="my-drawer" class="drawer-overlay"></label>
				<ul class="menu menu-lg bg-base-100 min-h-full w-80 gap-2 p-4">
					<li>
						<a href="/" class="text-2xl font-bold">SaaS Landing</a>
					</li>
					<NavLinks />
				</ul>
			</div>
		</div>
	</div>
</div>

<!-- Login Modal -->
<dialog id="login_modal" class="modal">
	<div class="modal-box max-w-sm">
		<div class="text-center">
			<h3 class="text-2xl font-semibold">Login</h3>
		</div>

		<div>
			<div class="form-control mt-4">
				<label class="label" for="login_email">
					<span class="label-text font-medium">Email</span>
				</label>
				<input
					type="email"
					id="login_email"
					class="input input-bordered h-8"
					placeholder="name@daisyui.com"
					required
				/>
			</div>

			<div class="form-control mt-2">
				<label class="label" for="login_password">
					<span class="label-text font-medium">Password</span>
				</label>
				<input
					type="password"
					id="login_password"
					class="input input-bordered h-8"
					placeholder="It's top secret"
					required
				/>
				<div class="label">
					<span></span>
					<span><a href="#" class="text-base-content/80">Forgot password?</a></span>
				</div>
			</div>

			<div class="mt-3 flex items-center justify-end gap-3">
				<button class="btn">Register</button>
				<button class="btn btn-primary">Login</button>
			</div>

			<div class="divider mt-4">Continue with</div>

			<div class="mt-4 flex gap-4">
				<button class="btn btn-ghost flex-1">Google</button>
				<button class="btn btn-ghost btn-neutral flex-1">Github</button>
			</div>
		</div>
	</div>
	<form method="dialog" class="modal-backdrop">
		<button>close</button>
	</form>
</dialog>

<!-- Register Modal -->
<dialog id="register_modal" class="modal">
	<div class="modal-box max-w-sm">
		<div class="text-center">
			<h3 class="text-2xl font-semibold">Register</h3>
		</div>

		<div>
			<div class="form-control mt-4">
				<label class="label" for="register_username">
					<span class="label-text font-medium">Username</span>
				</label>
				<input
					type="text"
					id="register_username"
					class="input input-bordered h-8"
					placeholder="saadeghi"
					required
				/>
			</div>

			<div class="form-control mt-2">
				<label class="label" for="register_email">
					<span class="label-text font-medium">Email</span>
				</label>
				<input
					type="email"
					id="register_email"
					class="input input-bordered h-8"
					placeholder="name@daisyui.com"
					required
				/>
			</div>

			<div class="form-control mt-2">
				<label class="label" for="register_password">
					<span class="label-text font-medium">Password</span>
				</label>
				<input
					type="password"
					id="register_password"
					class="input input-bordered h-8"
					placeholder="It's secret"
					required
				/>
				<div class="label">
					<span class="label-text text-base-content/70 text-sm"
						>Min 8 letters required</span
					>
				</div>
			</div>

			<div class="mt-3 flex items-center justify-end gap-3">
				<button class="btn btn-primary">Register</button>
			</div>

			<div class="divider mt-4">Continue with</div>

			<div class="mt-4 flex gap-4">
				<button class="btn btn-ghost flex-1">Google</button>
				<button class="btn btn-ghost btn-neutral flex-1">Github</button>
			</div>
		</div>
	</div>
	<form method="dialog" class="modal-backdrop">
		<button>close</button>
	</form>
</dialog>
