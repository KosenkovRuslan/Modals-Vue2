<template>
  <modal
    title="Modal with form + validate"
    @close="$emit('close')"
  >
    <div slot="body">
      <form @submit.prevent="">
        <label>Name:</label>
        <input type="text" required />
        <label>Email:</label>
        <input type="email" required />
        <button class="btn btnPrimary">Submit</button>
      </form>
    </div>
  </modal>
</template>

<script>
import modal from '@/components/UI/Modal.vue'
export default {
  components: {
    modal,
  },
}
</script>

<style></style>
