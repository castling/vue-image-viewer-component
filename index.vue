<template>
  <div class="image-viewer" @contextmenu.prevent
    :class="{ 'no-image': noImage || images==null || images.length==0 }"
    >
    <viewer class="image-viewer__view"
      :images="images"
      @inited="inited"
      ref="viewer"
      rebuild
      >
      <img class="image-viewer__view__image" v-for="(src,i) in images" :key="src"
        @error="noImage = true"
        @success="noImage = false"
        :class="{active:i+1==page}"
        :src="src"
      >
    </viewer>
  </div>
</template>

<script>
import Viewer from 'v-viewer/src/component.vue'
import 'viewerjs/dist/viewer.css'

export default {
  components: {
    Viewer,
  },
  props: {
    images: {
      type: Array,
      default: () => [],
    },
    page: {
      type: Number,
      default: 1,
    },
  },
  data() {
    return {
      noImage: false,
    }
  },
  watch: {
  },
  mounted() {
    this.$el.querySelector('.image-viewer__view').addEventListener('show',() => {
      this.$emit('show')
    })
    this.$el.querySelector('.image-viewer__view').addEventListener('hide',() => {
      this.$emit('hide')
    })
  },
  methods: {
    inited(viewer) {
      this.viewer = viewer
    },
    setNoImage() {
      this.noImage = true
    },
  },
}
</script>

<style scoped lang="scss">
.image-viewer {
  width: 100%;
  height: 100%;
  min-width: 100%;
  min-height: 200px;

  &.no-image {
    &::after {
      content: "NO PAGE";
      position: absolute;
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;
      background-color: rgba(0,0,0,0.15);
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: Verdana;
      font-size: 2.5rem;
      font-weight: 800;
    }

    .image-viewer__view__image {
      display: none;
    }
  }

  &__view {
    width: 100%;
    height: 100%;
    cursor: pointer;
    &__image {
      width: 100%;
      height: 100%;
      max-height: 90vh;
      object-fit: contain;
      padding: 1rem;
      background-color: rgb(230,230,230);
      z-index: -1;
      &.active {
        z-index: 0;
      }
      &:not(:first-child) {
        position: absolute;
        left: 0;
        top: 0;
      }
    }
  }
}
</style>
