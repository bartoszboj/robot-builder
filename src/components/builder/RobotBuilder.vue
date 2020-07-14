<template>
  <div>
    <div class="top-row">
      <div class="top part">
        <img :src="availableParts.heads[headIndex].src" title="head" />
        <button @click="selectPreviousHead()" class="prev-selector">
          &#9668;
        </button>
        <button @click="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="availableParts.arms[0].src" title="left arm" />
        <button @click="selectPreviousLeftArm()" class="prev-selector">
          &#9650;
        </button>
        <button @click="selectNextLeftArm()" class="next-selector">
          &#9660;
        </button>
      </div>
      <div class="center part">
        <img :src="availableParts.torsos[0].src" title="torso" />
        <button @click="selectPreviousTorso()" class="prev-selector">
          &#9668;
        </button>
        <button @click="selectNextTorso()" class="next-selector">
          &#9658;
        </button>
      </div>
      <div class="right part">
        <img :src="availableParts.arms[0].src" title="right arm" />
        <button @click="selectPreviousRightArm()" class="prev-selector">
          &#9650;
        </button>
        <button @click="selectNextRightArm()" class="next-selector">
          &#9660;
        </button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="availableParts.bases[0].src" title="base" />

        <button @click="selectPreviousBase()" class="prev-selector">
          &#9668;
        </button>
        <button @click="selectNextBase()" class="next-selector">&#9658;</button>
      </div>
    </div>
  </div>
</template>

<script>
import availableParts from "@/components/data/parts";

const nextValidIndex = function(index, length) {
  return index === length - 1 ? 0 : index + 1;
};
const previousValidIndex = function(index, length) {
  return index === 0 ? length - 1 : index - 1;
};
export default {
  name: "RobotBuilder",
  data() {
    return {
      availableParts,
      headIndex: 0,
      leftArmIndex: 0,
      torsoIndex: 0,
      rightArmIndex: 0,
      baseIndex: 0,
    };
  },
  computed: {
    headsImg() {
      const headsImg = this.availableParts.heads.map((head) => {
        return head.src;
      });
      return headsImg;
    },
    armsImg() {
      const headsImg = this.availableParts.arms.map((arm) => {
        return arm.src;
      });
      return headsImg;
    },
    torsosImg() {
      const torsosImg = this.availableParts.torsos.map((torso) => {
        return torso.src;
      });
      return torsosImg;
    },
    basesImg() {
      const basesImg = this.availableParts.bases.map((base) => {
        return base.src;
      });
      return basesImg;
    },
  },
  methods: {
    selectNextHead: function() {
      this.headIndex = nextValidIndex(
        this.headIndex,
        this.availableParts.heads.length
      );
    },
    selectPreviousHead: function() {
      this.headIndex = previousValidIndex(
        this.headIndex,
        this.availableParts.heads.length
      );
    },
    selectNextLeftArm: function() {
      this.leftArmIndex = nextValidIndex(
        this.leftArmIndex,
        this.availableParts.arms.length
      );
    },
    selectPreviousLeftArm: function() {
      this.leftArmIndex = previousValidIndex(
        this.leftArmIndex,
        this.availableParts.arms.length
      );
    },
    selectNextTorso: function() {
      this.torsoIndex = nextValidIndex(
        this.torsoIndex,
        this.availableParts.torsos.length
      );
    },
    selectPreviousTorso: function() {
      this.torsoIndex = previousValidIndex(
        this.torsoIndex,
        this.availableParts.torsos.length
      );
    },
    selectNextRightArm: function() {
      this.rightArmIndex = nextValidIndex(
        this.rightArmIndex,
        this.availableParts.arms.length
      );
    },
    selectPreviousRightArm: function() {
      this.rightArmIndex = previousValidIndex(
        this.rightArmIndex,
        this.availableParts.arms.length
      );
    },
    selectNextBase: function() {
      this.baseIndex = nextValidIndex(
        this.baseIndex,
        this.availableParts.bases.length
      );
    },
    selectPreviousBase: function() {
      this.baseIndex = previousValidIndex(
        this.baseIndex,
        this.availableParts.bases.length
      );
    },
  },
};
</script>

<style lang="scss" scoped>
.part {
  position: relative;
  width: 165px;
  height: 165px;
  border: 3px solid #aaa;
}
.part img {
  width: 165px;
}
.top-row {
  display: flex;
  justify-content: space-around;
}
.middle-row {
  display: flex;
  justify-content: center;
}
.bottom-row {
  display: flex;
  justify-content: space-around;
  border-top: none;
}
.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
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
.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}
</style>
