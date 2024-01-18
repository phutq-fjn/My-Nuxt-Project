<script setup>
const { data, pending, error, refresh } = await useFetch('/api/modules', {
  pick: ['title']
})
</script>
