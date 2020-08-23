<script>
	export let segment;
</script>

<slot></slot>

<style>
	:global(*) {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        user-select: none;
    }

    :global(body) {
        height: 100vh;
        overflow: hidden;
    }
</style>