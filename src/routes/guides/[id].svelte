<script lang="ts" context="module">
	import type { LoadInput } from '@sveltejs/kit';

	export async function load({ fetch, params }: LoadInput) {
		const id = params.id;
		const res = await fetch(`/guides/${id}.json`);
		const { guide } = await res.json();

		if (res.ok) {
			return {
				props: {
					guide
				}
			};
		}

		return {
			status: 301,
			// error: new Error('Could not fetch the guides')
			redirect: '/guides'
		};
	}
</script>

<script lang="ts">
	import type { Guide } from './guideType';

	export let guide: Guide;
</script>

<div class="guide">
	<h2>{guide.title}</h2>
	<p>{guide.body}</p>
</div>

<style>
	.guide {
		margin-top: 40px;
		padding: 10px;
		border: 1px dotted rgba(255, 255, 255, 0.2);
	}
</style>
