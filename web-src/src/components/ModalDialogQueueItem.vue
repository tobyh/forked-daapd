<template>
  <div>
    <transition name="fade">
      <div class="modal is-active" v-if="show">
        <div class="modal-background" @click="$emit('close')"></div>
        <div class="modal-content fd-modal-card">
          <div class="card">
            <div class="card-content">
              <p class="title is-4">
                {{ item.title }}
              </p>
              <p class="subtitle">
                {{ item.artist }}
              </p>
              <div class="content is-small">
                <p>
                  <span class="heading">Album</span>
                  <span class="title is-6">{{ item.album }}</span>
                </p>
                <p v-if="item.album_artist">
                  <span class="heading">Album artist</span>
                  <span class="title is-6">{{ item.album_artist }}</span>
                </p>
                <p v-if="item.composer">
                  <span class="heading">Composer</span>
                  <span class="title is-6">{{ item.composer }}</span>
                </p>
                <p v-if="item.year > 0">
                  <span class="heading">Year</span>
                  <span class="title is-6">{{ item.year }}</span>
                </p>
                <p>
                  <span class="heading">Genre</span>
                  <span class="title is-6">{{ item.genre }}</span>
                </p>
                <p>
                  <span class="heading">Track / Disc</span>
                  <span class="title is-6">{{ item.track_number }} / {{ item.disc_number }}</span>
                </p>
                <p>
                  <span class="heading">Length</span>
                  <span class="title is-6">{{ item.length_ms | duration }}</span>
                </p>
                <p>
                  <span class="heading">Path</span>
                  <span class="title is-6">{{ item.path }}</span>
                </p>
              </div>
            </div>
            <footer class="card-footer">
              <a class="card-footer-item has-text-dark" @click="remove">
                <span class="icon"><i class="mdi mdi-delete"></i></span> <span class="is-size-7">Remove</span>
              </a>
              <a class="card-footer-item has-text-dark" @click="play">
                <span class="icon"><i class="mdi mdi-play"></i></span> <span class="is-size-7">Play</span>
              </a>
            </footer>
          </div>
        </div>
        <button class="modal-close is-large" aria-label="close" @click="$emit('close')"></button>
      </div>
    </transition>
  </div>
</template>

<script>
import webapi from '@/webapi'

export default {
  name: 'ModalDialogQueueItem',
  props: [ 'show', 'item' ],

  methods: {
    remove: function () {
      this.$emit('close')
      webapi.queue_remove(this.item.id)
    },

    play: function () {
      this.$emit('close')
      webapi.player_play({ 'item_id': this.item.id })
    }
  }
}
</script>

<style>
</style>
