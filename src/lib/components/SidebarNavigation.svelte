<script>
	import { page } from '$app/stores';
	import logo from '$lib/assets/images/logo/logo.png';
	import CloseIcon from '$lib/assets/icons/CloseIcon.svelte';
	import StatisticsIcon from '$lib/assets/icons/navbar-icon/StatisticsIcon.svelte';
	import InventoryIcon from '$lib/assets/icons/navbar-icon/InventoryIcon.svelte';
	import ExpensesIcon from '$lib/assets/icons/navbar-icon/ExpensesIcon.svelte';
	import SalesIcon from '$lib/assets/icons/navbar-icon/SalesIcon.svelte';
	import ToolsIcon from '$lib/assets/icons/navbar-icon/ToolsIcon.svelte';
	import MarketIcon from '$lib/assets/icons/navbar-icon/MarketIcon.svelte';
	import SettingsIcon from '$lib/assets/icons/navbar-icon/SettingsIcon.svelte';

	const sidebarMenues = [
		{
			path: '/',
			name: 'Statistics',
			icon: StatisticsIcon
		},
		{
			path: '/inventory',
			name: 'Inventory',
			icon: InventoryIcon
		},
		{
			path: '/expenses',
			name: 'Expenses',
			icon: ExpensesIcon
		},
		{
			path: '/sales',
			name: 'Sales',
			icon: SalesIcon
		},
		{
			path: '/tools',
			name: 'Tools',
			icon: ToolsIcon
		},
		{
			path: '/market',
			name: 'Market',
			icon: MarketIcon
		},
		{
			path: '/settings',
			name: 'Settings',
			icon: SettingsIcon
		},
	];

	let sidebar;

	const handleMenuHideOnClick = ()=>{
		sidebar.classList.remove('show')
	}
</script>

<aside class="sidebar" bind:this={sidebar}>
	<div class="sidebar__header">
		<button type="button" class="btn-close" aria-label="Close menu" on:click={handleMenuHideOnClick}>
			<svelte:component this={CloseIcon} />
		</button>
		<a href="/" class="sidebar__logo" on:click={handleMenuHideOnClick}>
			<img src={logo} alt="logo" width="42" height="37">
		</a>
	</div>
	<nav class="sidebar__nav">
		{#each sidebarMenues as menue }
			<a href={menue.path} class="nav__link" aria-current={$page.url.pathname === menue.path ? 'page' : undefined} on:click={handleMenuHideOnClick} data-sveltekit-preload-data="hover">
				<span class="nav__link__icon">
					<svelte:component this={menue.icon} />
				</span>
				<span class="nav__link__text">{menue.name}</span>
			</a>
		{/each}
	</nav>
</aside>

<style>
	:global(:root) {
		--sidebar-width: 277px;
	}

	.sidebar{
		--_padding: 50px;
		--_gap: 40px;
		position: fixed;
		z-index: 999;
		top: 0;
		left: 0;
		bottom: 0;
		display: -webkit-box;
		display: -ms-flexbox;
		display: flex;
		-webkit-box-orient: vertical;
		-webkit-box-direction: normal;
		    -ms-flex-direction: column;
		        flex-direction: column;
		-webkit-transition:
			-webkit-box-shadow 0.25s linear,
			-webkit-transform 0.25s ease-in-out;
		transition:
			-webkit-box-shadow 0.25s linear,
			-webkit-transform 0.25s ease-in-out;
		-o-transition:
			box-shadow 0.25s linear,
			transform 0.25s ease-in-out;
		transition:
			box-shadow 0.25s linear,
			transform 0.25s ease-in-out;
		transition:
			box-shadow 0.25s linear,
			transform 0.25s ease-in-out,
			-webkit-box-shadow 0.25s linear,
			-webkit-transform 0.25s ease-in-out;
	}

	.sidebar__header{
		text-align: center;
		padding: var(--_padding) var(--_padding) 0;
		margin-bottom: var(--_gap);
	}

	.sidebar__header .btn-close{
		position: absolute;
		top: 15px;
		right: 15px;
	}

	.sidebar__logo{
		display: inline-block;
		padding: 2px;
	}

	.sidebar__nav{
		-webkit-box-flex: 1;
		    -ms-flex-positive: 1;
		        flex-grow: 1;
		display: -webkit-box;
		display: -ms-flexbox;
		display: flex;
		-webkit-box-orient: vertical;
		-webkit-box-direction: normal;
		    -ms-flex-direction: column;
		        flex-direction: column;
		gap: var(--_gap);
		padding: 0 var(--_padding) var(--_padding);
		overflow: auto;
	}

	.nav__link{
		display: -webkit-inline-box;
		display: -ms-inline-flexbox;
		display: inline-flex;
		-webkit-box-align: center;
		    -ms-flex-align: center;
		        align-items: center;
		gap: 15px;
		color: #7B7B7B;
		padding: 12px 32px;
		border: 1.5px solid transparent;
		border-radius: 50rem;
		-webkit-transition: all .25s ease-in-out;
		-o-transition: all .25s ease-in-out;
		transition: all .25s ease-in-out;
	}

	.nav__link[aria-current="page"],
	.nav__link:hover,
	.nav__link:focus-visible
	{
		color: #ffffff;
		background-color: rgba(7, 6, 6, 0.8);
	}
	
	.nav__link[aria-current="page"]{
		border-color: #EFEEEB;
	}
	
	.nav__link__icon{
		font-size: 22px;
		-ms-flex-negative: 0;
		    flex-shrink: 0;
	}

	.nav__link__text{
		font-size: 15px;
		font-weight: 600;
	}

	@media (max-width: 991.98px){
		:global(:root) {
			--sidebar-width: 0;
		}

		.sidebar{
			--_gap: 20px;
			background-color: #000000;
		}

		.sidebar:not(.show){
			-webkit-transform: translateX(-100%);
			    -ms-transform: translateX(-100%);
			        transform: translateX(-100%);
		}
	}

	@media (min-width: 992px){
		.sidebar__header .btn-close{
			display: none;
		}
	}
</style>