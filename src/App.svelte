<script>
	import Icon from '@iconify/svelte';

	let items = [
		{
			label: 'Home',
			path: '#',
			icon: 'bx:home',
			active: true,
		},
		{
			label: 'Account',
			path: '#',
			icon: 'ic:baseline-account-circle',
			active: false,
		},
		{
			label: 'Inbox',
			path: '#',
			icon: 'bx:message',
			active: false,
		},
		{
			label: 'Photos',
			path: '#',
			icon: 'ant-design:camera-outlined',
			active: false,
		},
		{
			label: 'Settings',
			path: '#',
			icon: 'charm:cog',
			active: false,
		},
	];

	const handleClick = (label, i) => {
		const mapped = items.map(item => ({ ...item, active: false }));
		mapped.find(item => item.label === label).active = true;
		items = mapped;

		indicatorLeft = i * 95 + 78;
	};

	let indicatorLeft = 78;
</script>

<main class="h-[100vh] flex items-center justify-center bg-gray-700">
	<nav class="bg-white w-[600px] py-6 rounded-lg relative flex justify-center items-center">
		<ul class="grid grid-cols-5 gap-x-10 justify-center items-center">
			<div class="absolute bg-green-500 w-16 h-16 rounded-full duration-500 transition-all border-[6px] border-gray-700 -top-8 indicator" style={`left: ${indicatorLeft}px`} />
			{#each items as { label, path, icon, active }, i}
				<li class="text-gray-800" on:click={() => handleClick(label, i)}>
					<a href={path} class="flex flex-col items-center">
						<div class="text-2xl icon transition-all" class:active>
							<Icon {icon} />
						</div>
						<div class="text-sm font-medium label opacity-0 translate-y-2 transition-all duration-500" class:active class:opacity-100={active}>{label}</div>
					</a>
				</li>
			{/each}
		</ul>
	</nav>
</main>

<style>
	li .icon.active {
		@apply -translate-y-9;
	}
	li .label.active {
		@apply -translate-y-3;
	}
</style>
