<template>
	<div class="flex overflow-y-auto flex-col">
		<div class="flex flex-col md:flex-row max-w-5xl self-center">
			<div class="connect-panel w-full px-4 py-2 mt-32">
				<connect @update:query="val => urlArgs = val" />

				<div class="card">
					<div class="card-title">
						<h2>Automatic Login</h2>
					</div>
					<div class="card-content">
						<p class="mb-2 text-sm">
							To automatically connect, bookmark this URL with connection info in URL after #!auto (default values can be skipped)
						</p>
						<label class="label">Current settings:</label>
						<a
							:href="exampleURL"
							class="block break-all mb-2"
							@click.prevent="() => {}"
						>{{ exampleURL }}</a>
						<p class="text-sm">
							To include password add &password={password}. Note that all fields can't include &amp; or =
						</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import Connect from './connect'

export default {
	components: {
		Connect
	},
	data() {
		return {
			urlArgs: ''
		}
	},
	computed: {
		exampleURL() {
			return `${location.origin + location.pathname}#!auto${this.urlArgs}`
		},
		httpURL() {
			return location.href.replace('https://', 'http://')
		},
		showHTTPSWarning() {
			return location.protocol === 'https:'
		}
	}
}
</script>

<style lang="postcss">
@screen md {
	.connect-panel {
		order: 2;
	}
}
</style>
