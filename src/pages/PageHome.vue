<template>
  <q-page>
    <div class="q-py-lg q-px-md">
      <q-input
        bottom-slots
        v-model="newJweetContent"
        placeholder="What's happening"
        counter
        autogrow
        class="new-jweet"
        maxlength="280"
        :dense="dense"
      >
        <template v-slot:before>
          <q-avatar size="xl">
            <img src="src/assets/onepunch.jpg" style="object-fit: cover" />
          </q-avatar>
        </template>

        <template v-slot:after>
          <q-btn
            :disable="!newJweetContent"
            unelevated
            no-caps
            rounded
            color="primary"
            label="jweet"
          />
        </template>
      </q-input>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "PageHome",
  data() {
    return {
      newJweetContent: "",
    };
  },
});
</script>

<style lang="sass">
.new-jweet
  textarea
    font-size: 19px
    linehight: 1.4 !important
</style>
