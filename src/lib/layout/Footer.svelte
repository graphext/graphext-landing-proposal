<script>
	import DiscordSvg from '$lib/imgs/discord.svg';
	import TwitterSvg from '$lib/imgs/x.svg';

	const footerNavs = [
		{
			label: 'Product',
			items: [
				{
					href: '/',
					name: 'Email Collection'
				},
				{
					href: '/pricing',
					name: 'Pricing'
				},
				{
					href: '/faq',
					name: 'FAQ'
				}
			]
		},

		{
			label: 'Community',
			items: [
				{
					href: '/',
					name: 'Discord'
				},
				{
					href: '/',
					name: 'Twitter'
				},
				{
					href: 'mailto:hello@chatcollect.com',
					name: 'Email'
				}
			]
		},
		{
			label: 'Legal',
			items: [
				{
					href: '/terms',
					name: 'Terms'
				},

				{
					href: '/privacy',
					name: 'Privacy'
				}
			]
		}
	];

	const footerSocials = [
		{
			href: '',
			name: 'Discord',
			icon: DiscordSvg
		},
		{
			href: '',
			name: 'Twitter',
			icon: TwitterSvg
		}
	];
</script>

<footer>
	<div class="mx-auto w-full max-w-screen-xl xl:pb-2">
		<div class="gap-4 p-4 px-8 py-16 sm:pb-16 md:flex md:justify-between">
			<div class="mb-12 flex flex-col gap-4">
				<a href="https://graphext.com" class="flex items-center gap-2">
					<svg
						width="32px"
						height="24px"
						version="1.1"
						xmlns="http://www.w3.org/2000/svg"
						xmlns:xlink="http://www.w3.org/1999/xlink"
						xml:space="preserve"
						class="fill-black dark:fill-white"
						style="fill-rule:evenodd;clip-rule:evenodd;stroke-linejoin:round;stroke-miterlimit:2;"
					>
						<g transform="matrix(1,0,0,1,-8165.71,-909.01)">
							<g transform="matrix(1.08571,0,3.06782e-17,1.08571,8165.71,909.01)">
								<path
									d="M29.342,10.892C29.342,16.908 25.434,21.785 19.667,21.785C16.748,21.785 8.951,20.346 6.661,19.265C2.402,17.493 0,14.915 0,10.892C0,6.87 2.402,4.291 6.661,2.519C8.951,1.439 16.748,0 19.667,0C25.434,0 29.342,4.877 29.342,10.892ZM9.04,10.892C9.04,12.598 7.691,13.981 6.027,13.981C4.363,13.981 3.013,12.598 3.013,10.892C3.013,9.186 4.363,7.803 6.027,7.803C7.691,7.803 9.04,9.186 9.04,10.892ZM25.756,10.892C25.756,14.214 23.019,16.908 19.643,16.908C16.267,16.908 13.53,14.214 13.53,10.892C13.53,7.57 16.267,4.877 19.643,4.877C23.019,4.877 25.756,7.57 25.756,10.892Z"
								/>
							</g>
						</g>
					</svg>

					<span
						class="graphext-logo self-center whitespace-nowrap text-2xl font-semibold dark:text-white"
					>
						Graphext
					</span>
				</a>
			</div>
			<div class="grid grid-cols-1 gap-8 sm:grid-cols-3 sm:gap-10">
				{#each footerNavs as nav}
					<div>
						<h2
							class="mb-6 text-sm font-medium uppercase tracking-tighter text-gray-900 dark:text-white"
						>
							{nav.label}
						</h2>
						<ul class="grid gap-2">
							{#each nav.items as item}
								<li>
									<a
										href={item.href}
										class="cursor-pointer text-sm font-[450] text-gray-400 duration-200 hover:text-gray-200"
									>
										{item.name}
									</a>
								</li>
							{/each}
						</ul>
					</div>
				{/each}
			</div>
		</div>

		<div
			class="flex flex-col gap-2 rounded-md border-neutral-700/20 px-8 py-4 sm:flex sm:flex-row sm:items-center sm:justify-between"
		>
			<div class="flex items-center space-x-5 sm:mt-0 sm:justify-center">
				{#each footerSocials as social}
					<a
						href={social.href}
						class="fill-gray-500 text-gray-500 hover:fill-gray-900 hover:text-gray-900 dark:hover:fill-gray-600 dark:hover:text-gray-600"
					>
						<img src={social.icon} class="size-4" alt={social.name} />
						<span class="sr-only">{social.name}</span>
					</a>
				{/each}
			</div>
			<span class="text-sm text-gray-500 dark:text-gray-400 sm:text-center">
				Copyright ©
				{' '}
				{new Date().getFullYear()}
				{' '}
				<a href="/" class="cursor-pointer">Graphext</a>
			</span>
		</div>
	</div>
	<!-- Site Banner -->
</footer>

<style>
	.graphext-logo {
		font-variation-settings: 'wdth' 110;
	}
</style>
