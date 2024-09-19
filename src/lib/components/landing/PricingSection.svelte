<script lang="ts">
	import { LoaderIcon, CheckIcon } from 'lucide-svelte';
	import Switch from '$lib/components/ui/switch/switch.svelte';
	import Button from '$lib/components/ui/button/button.svelte';
	import { cn } from '$lib/utils';
	import { fly } from 'svelte/transition';

	type Interval = 'month' | 'year';

	export function toHumanPrice(price: number, decimals: number = 2) {
		return Number(price / 100).toFixed(decimals);
	}
	let productPrices = [
		{
			id: 'price_0',
			name: 'Public',
			description: 'Perfect for testing and small projects.',
			features: ['Up to 4k rows', 'Up to 4 projects', 'Only 1 editor seat'],
			monthlyPrice: 0,
			yearlyPrice: 0,
			isMostPopular: false
		},
		{
			id: 'price_1',
			name: 'Pro',
			description: 'For professionals working as a team.',
			features: [
				'Unlimited rows',
				'Unlimited teams',
				'Unlimited projects',
				'Includes 2 editor seats',
				'Collaboration between team members',
				'Free viewers',
				'Projects recurrence',
				'Export back to integrations'
			],
			monthlyPrice: 15000,
			yearlyPrice: 144000, // 20% annual discount applied
			extraInfo: '$50 extra per seat | VAT not included.',
			isMostPopular: true
		},
		{
			id: 'price_2',
			name: 'Enterprise',
			description: 'Pay as you scale.',
			features: [
				'Everything in Pro, plus...',
				'Multiple automatic updates per project/day',
				'Premium integrations',
				'Private Cloud and Single Sign-On',
				'Hands-on training',
				'Dedicated account manager',
				'Data Engineering Services'
			],
			monthlyPrice: null,
			yearlyPrice: null,
			contactSales: true,
			isMostPopular: false
		}
	];
	let interval: Interval = 'month';
	let isLoading = false;
	let index = '';
	let onSubscribeClick = async (priceId: string) => {
		index = priceId;
		isLoading = true;
		// Simulate API call
		await new Promise((resolve) => setTimeout(resolve, 1000));
		isLoading = false;
	};
	/*
    onCheckedChange={(checked) => {
                setInterval(checked ? 'year' : 'month')
             }}
     */
</script>

<section id="pricing">
	<div class="mx-auto flex max-w-screen-xl flex-col gap-8 px-4 py-14 md:px-8">
		<div class="mx-auto max-w-5xl text-center">
			<h4 class="text-xl font-bold tracking-tight text-black dark:text-white">Pricing</h4>

			<h2
				class="mega-hero text-5xl font-bold tracking-tight text-black dark:text-white sm:text-6xl"
			>
				Simple pricing for everyone.
			</h2>
		</div>

		<div class="flex w-full items-center justify-center space-x-2">
			<Switch
				on:click={() => {
					interval = interval === 'month' ? 'year' : 'month';
				}}
				id="interval"
			/>
			<span>Annual</span>
			<span
				class="inline-block whitespace-nowrap rounded-full bg-black px-2.5 py-1 text-[11px] font-semibold uppercase leading-5 tracking-wide text-white dark:bg-white dark:text-black"
			>
				2 MONTHS FREE ✨
			</span>
		</div>

		<div class="mx-auto flex w-full flex-col justify-center gap-2 md:flex-row">
			{#each productPrices as price, id}
				<div
					class={cn(
						'relative flex w-full flex-col gap-8 overflow-hidden rounded-2xl border p-4 text-black dark:text-white md:w-1/3',
						{
							'border-2 border-[var(--color-one)] dark:border-[var(--color-one)]':
								price.isMostPopular
						}
					)}
				>
					<div class="flex items-center">
						<div class="ml-4">
							<h2 class="text-base font-semibold leading-7">
								{price.name}
							</h2>
							<p class="h-12 text-sm leading-5 text-black/70 dark:text-white">
								{price.description}
							</p>
						</div>
					</div>

					<div>
						{#if price.contactSales}
							<div class="flex flex-row gap-1">
								<span class="text-4xl font-bold text-black dark:text-white"> Contact Sales </span>
							</div>
						{:else}
							{#key interval}
								<div in:fly={{ y: 20, duration: 300, delay: id * 40 }} class="flex flex-row gap-1">
									<span class="text-4xl font-bold text-black dark:text-white">
										{#if interval === 'month'}
											${toHumanPrice(price.monthlyPrice, 0)}
										{:else}
											${toHumanPrice(price.yearlyPrice, 0)}
										{/if}
										<span class="text-xs">
											/ {interval}
										</span>
									</span>
								</div>
							{/key}
						{/if}

						{#if price.extraInfo}
							<p class="text-sm">{price.extraInfo}</p>
						{:else}
							<p class="text-sm opacity-0">$50</p>
						{/if}
					</div>

					<Button
						class={cn(
							'group relative w-full gap-2 overflow-hidden text-lg font-semibold tracking-tighter',
							'transform-gpu ring-offset-current transition-all duration-300 ease-out hover:ring-2 hover:ring-primary hover:ring-offset-2'
						)}
						disabled={isLoading}
						on:click={() => onSubscribeClick(price.id)}
					>
						<span
							class="absolute right-0 -mt-12 h-32 w-8 translate-x-12 rotate-12 transform-gpu bg-white opacity-10 transition-all duration-1000 ease-out group-hover:-translate-x-96 dark:bg-black"
						/>
						{#if isLoading && index === price.id}
							<LoaderIcon class="mr-2 size-4 animate-spin" />
							{price.contactSales ? 'Contacting' : 'Subscribing'}
						{:else if !isLoading || (isLoading && index !== price.id)}
							{price.contactSales ? 'Contact Sales' : 'Subscribe'}
						{/if}
					</Button>

					<hr
						class="m-0 h-px w-full border-none bg-gradient-to-r from-neutral-200/0 via-neutral-500/30 to-neutral-200/0"
					/>
					{#if price.features && price.features.length > 0}
						<ul class="flex flex-col gap-2 font-normal">
							{#each price.features as feature, idx}
								<li class="flex items-center gap-3 text-sm font-medium text-black dark:text-white">
									<CheckIcon
										class="size-5 shrink-0 rounded-full bg-[var(--color-one)] p-[2px] text-white"
									/>
									<span class="flex">{feature}</span>
								</li>
							{/each}
						</ul>
					{/if}
				</div>
			{/each}
		</div>
	</div>
</section>

<style>
	.mega-hero {
		font-variation-settings: 'wdth' 110;
		font-feature-settings: 'ss02';
	}
</style>
