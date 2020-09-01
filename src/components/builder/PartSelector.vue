<template>
  <div class="part" :class="position">
    <img :src="selectedPart.src">
    <button @click="selectPreviousPart()" class="prev-selector"></button>
    <button @click="selectNextPart()" class="next-selector"></button>
  </div>
</template>

<script>
const nextValidIndex = function(index, length) {
  return index === length - 1 ? 0 : index + 1;
};
const previousValidIndex = function(index, length) {
  return index === 0 ? length - 1 : index - 1;
};

export default {
    name: "PartSelector",
    props: ['parts', 'position'],
    data() {
        return {
            selectedPartIndex: 0
        }
    },
    computed: {
        selectedPart () {
            return this.parts[this.selectedPartIndex];
        }
    },
    methods: {
        selectPreviousPart() {
            this.selectedPartIndex = previousValidIndex(this.selectedPartIndex, this.parts.length)
        },
        selectNextPart() {
            this.selectedPartIndex = nextValidIndex(this.selectedPartIndex, this.parts.length)
        }
    }
}
</script>

<style lang="scss" scoped>
    .part{
        position: relative;
        width: 165px;
        height: 165px;
        border: 3px solid #aaa;
        & img {
            width: 100%;
        }
    }

    .top {
        border-bottom: none;
    }
    .left {
        border-right: none;
        img {
            transform: rotate(-90deg);
        }
        .prev-selector {
            top: -28px;
            left: -3px;
            width: 144px;
            height: 25px;
        }
        .next-selector {
            top: auto;
            bottom: -28px;
            left: -3px;
            width: 144px;
            height: 25px;
        }
    }
    .center {
        .prev-selector, .next-selector {
            opacity: 0.7
        }
    }
    .right {
        border-left: none;
        img {
            transform: rotate(90deg) scale(-1, 1);    
        }
        .prev-selector {
            top: -28px;
            left: 24px;
            width: 144px;
            height: 25px;
        }
        .next-selector {
            top: auto;
            bottom: -28px;
            left: 24px;
            width: 144px;
            height: 25px;
        }
    }
    .bottom {
        border-top: none;
    }
    .prev-selector {
    position: absolute;
    z-index: 1;
    top: -3px;
    left: -28px;
    width: 25px;
    height: 171px;
    }
   .next-selector {
    position: absolute;
    z-index: 1;
    top: -3px;
    right: -28px;
    width: 25px;
    height: 171px;
    }
</style>