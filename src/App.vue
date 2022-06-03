<template>
  <div class="wrapper">
    <!-- Header -->

    <div class="wrapper-content">
      <section>
        <div class="container">
          <!-- First Modal -->
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">
            Show first modal
          </button>
          <modal
            title="First Modal"
            v-show="modalFirst"
            @close="modalFirst = !modalFirst"
          >
            <div slot="body">
              <p>
                Lorem ipsum dolor sit amet consectetur, adipisicing elit. Ad,
                fuga excepturi reiciendis tenetur aperiam repudiandae?
              </p>
              <button class="btn btnPrimary" @click="modalFirst = false">
                Well done!
              </button>
            </div>
          </modal>

          <!-- Second modal -->
          <button
            class="btn btnPrimary"
            @click="modalSecond.show = !modalSecond.show"
          >
            Show modal with form
          </button>
          <modal
            title="Modal with form"
            v-show="modalSecond.show"
            @close="modalSecond.show = false"
          >
            <div slot="body">
              <form @submit.prevent="submitSecondForm">
                <label>Name:</label>
                <input type="text" required v-model="modalSecond.name" />
                <label>Email:</label>
                <input type="email" required v-model="modalSecond.email" />
                <button class="btn btnPrimary">Submit</button>
              </form>
            </div>
          </modal>

          <!-- Modal with validate -->
          <button
            class="btn btnPrimary"
            @click="modalValidate = !modalValidate"
          >
            Show modal with form + validate
          </button>
          <modalValidate
            v-show="modalValidate"
            @close="modalValidate = false"
          >
          </modalValidate>
        </div>
      </section>
    </div>

    <!-- Footer -->
  </div>
</template>

<script>
import modal from '@/components/UI/Modal.vue'
import modalValidate from '@/components/ModalValidate.vue'
export default {
  name: 'App',
  components: {
    modal,
    modalValidate,
  },

  data() {
    return {
      modalFirst: false,
      modalSecond: {
        show: false,
        name: '',
        email: '',
      },
      modalValidate: false,
    }
  },

  methods: {
    submitSecondForm() {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email,
      })

      this.modalSecond.name = ''
      this.modalSecond.email = ''
      this.modalSecond.show = false
    },
  },
}
</script>

<style></style>
