<script lang="ts">
	import { i18n } from '$lib/i18n';
	import { ParaglideJS } from '@inlang/paraglide-sveltekit';
	import '../app.css';
	
	import { browser } from '$app/environment';
	import { QueryClient, QueryClientProvider } from '@tanstack/svelte-query';

	let { children } = $props();
	const queryClient = new QueryClient({
		defaultOptions: {
			queries: {
				enabled: browser
			}
		}
	});
</script>

<ParaglideJS {i18n}>
	<QueryClientProvider client={queryClient}>
		{@render children()}
	</QueryClientProvider>
</ParaglideJS>
