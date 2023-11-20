<template>
  <q-page>
    <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
      <div class="col">
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
        </q-input>
      </div>
      <div class="col col-shrink">
        <q-btn
          @click="addNewJweet"
          :disable="!newJweetContent"
          class="q-mb-lg"
          unelevated
          no-caps
          rounded
          color="primary"
          label="jweet"
        />
      </div>
    </div>
    <q-separator size="10px" color="grey-2" class="divider" />

    <q-list seperator>
      <transition-group
        appear
        enter-active-class="animated fadeIn slower"
        leave-active-class="animated fadeOut slower"
      >
        <q-item class="jweet q-py-md" v-for="jweet in jweets" :key="jweet.date">
          <q-item-section avatar top>
            <q-avatar size="xl">
              <img src="src/assets/onepunch.jpg" style="object-fit: cover" />
            </q-avatar>
          </q-item-section>

          <q-item-section>
            <q-item-label class="text-subtitle1">
              <strong>Jonas Neufeld</strong>
              <span class="text-grey-7 q-ml-sm">@jonasneuf</span>
            </q-item-label>
            <q-item-label class="jweet-content text-body1">
              {{ jweet.content }}
            </q-item-label>
            <div class="jweet-icons row justify-between q-mt-sm">
              <q-btn flat round size="sm" color="grey" icon="far fa-comment" />
              <q-btn flat round size="sm" color="grey" icon="fas fa-retweet" />
              <q-btn flat round size="sm" color="grey" icon="far fa-heart" />
              <q-btn
                @click="deletejweet(jweet)"
                flat
                round
                size="sm"
                color="grey"
                icon="fa-solid fa-trash"
              />
            </div>
          </q-item-section>

          <q-item-section side top>
            {{ relativeDate(jweet.date) }}
          </q-item-section>
        </q-item>
      </transition-group>
    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import { formatDistance } from "date-fns";

export default defineComponent({
  name: "PageHome",
  data() {
    return {
      newJweetContent: "",
      jweets: [
        {
          content:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Consequuntur sed nobis quaerat atque tempore fugit sit quasi ex. Ipsa vel magni unde ipsam. Quo, eum voluptate! Iusto voluptates nam sapiente.",
          date: 1699388919747,
        },
        // ... more jweets
      ],
    };
  },
  methods: {
    relativeDate(value) {
      return formatDistance(new Date(value), new Date());
    },
    addNewJweet() {
      if (this.newJweetContent.trim()) {
        this.jweets.unshift({
          content: this.newJweetContent,
          date: Date.now(),
        });
        this.newJweetContent = "";
      }
    },
    deletejweet(jweet) {
      let dateToDelete = jweet.date;
      let index = this.jweets.findIndex((jweet) => jweet.date === dateToDelete);
      this.jweets.splice(index, 1);
    },
  },
});
</script>

<style lang="sass">
.new-jweet
  textarea
    font-size: 19px
    line-height: 1.4 !important

.divider
  border-top: 1px solid
  border-bottom: 1px solid
  border-color: $grey-4

.jweet:not(:first-child)
  border-top: 1px solid rbga(0, 0, 0, 0, 12)

.jweet-content
  white-space: pre-line

.jweet-icons
  margin-left: -5px
</style>
