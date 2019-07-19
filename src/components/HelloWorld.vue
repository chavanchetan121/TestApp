<template>
  <div class="image-viewer" @contextmenu.prevent>
    <div class="title-viewer">{{ title }}</div>
    <viewer
      :options="options"
      :images="images"
      @inited="inited"
      class="viewer"
      ref="viewer"
      style="display:none"
    >
      <template v-for="image in images">
        <img :src="image" :key="image" />
      </template>
    </viewer>
    <a title="next" class="button is-large toolbar-tool control" @click="next">
      <img class="nextButton" :src="require('../Next.svg')" />
    </a>
  </div>
</template>

<script>
import Viewer from "v-viewer/src/component.vue";

export default {
  name: "HelloWorld",
  components: {
    Viewer
  },
  props: ["images"],
  data() {
    return {
      currentFolderId: null,
      options: {
        navbar: false,
        scalable: false,
        title: false,
        backdrop: false,
        fullscreen: true,
        keyboard: false,
        transition: true,
        toolbar: false,
        inline: true,
        button: false
      },
      title: "Test.png"
    };
  },
  beforeDestroy() {
    this.destroyviewer(this.$viewer);
  },
  methods: {
    inited(viewer) {
      this.$viewer = viewer;
      this.$viewer.show();
    },
    destroyviewer(viewer) {
      if (viewer) viewer.destroy();
    },
    next() {
      this.$emit("next");
    }
  }
};
</script>
<style lang="scss">
@import "~bulma/sass/utilities/_all";
@import "~bulma/sass/base/helpers";
.image-viewer {
  background-color: $grey-lighter;
  height: calc(100%);
  width: 100%;
  position: absolute;
}

.viewer-container {
  z-index: 0;
}

.viewer-canvas {
  background-color: $grey-lighter;
  margin-bottom: 56px;
}

.imageViewer-close {
  right: 0em;
  height: 2.5em;
  width: 2.4em;
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  z-index: 1;
  padding-bottom: 0.1em;
  opacity: 0.8;
  background: $background;
  cursor: pointer;
}

.close-viewer-icon {
  color: $black;
}
.close-viewer-icon:hover {
  color: $black;
}

.title-viewer {
  color: $black;
  display: flex;
  width: 100%;
  background-color: $background;
  position: absolute;
  line-height: 3.2;
  max-width: 100%;
  text-align: left;
  padding-left: 1.3em;
  z-index: 1;
  margin: 0;
  left: 0;
  opacity: 0.8;
  font-size: 0.81em;
}

.title-viewer:hover {
  color: $black;
  display: flex;
  position: absolute;
  width: 100%;
  background-color: $background;
  line-height: 3.2;
  max-width: 100%;
  text-align: left;
  padding-left: 1.3em;
  z-index: 1;
  margin: 0;
  left: 0;
  opacity: 0.8;
  font-size: 0.81em;
}

.nextButton {
  z-index: 1;
  width: 40px;
}

.button.is-large {
  bottom: 0;
  position: absolute;
}

.image-toolbar .toolbar-tools .field .is-large {
  @include mobile {
    font-size: 18px;
  }
}
</style>
