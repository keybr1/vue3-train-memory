<template>
  <div
    @click="cardSelected"
    class="flip-card w-30 h-30 md:w-40 md:h-40 relative text-center group perspective-1000"
  >
    <div
      class="flip-card-inner preserve-3d w-full h-full transition-transform"
      :class="[visible?'rotate-y-180':'', `duration-${durationFlipCard}`]"
    >
      <div
        class="flip-card-front shadow-md border-4 rounded p-2 bg-white text-black w-full h-full absolute rotate-y-180 backface-hidden"
        :class="matched?'opacity-10 bg-orange-200':''"
      >
        <img class="h-full w-auto m-auto" :src="`src/assets/img/${value}`" alt="">
      </div>
      <div
        class="flip-card-back p-4 bg-orange-200 shadow-md cursor-pointer rounded text-white w-full h-full absolute backface-hidden"
      >
        <img class="rounded" src="../assets/img/card_logo.png" alt="">
      </div>
    </div>
  </div>
</template>

<script>
import constants from '../assets/constants'

export default {
  props: {
    indexCard: {
      type: Number,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },
    visible: {
      type: Boolean,
      default: false,
    },
    matched: {
      type: Boolean,
      default: false,
    },
  },

  setup(props, context) {
    const durationFlipCard = constants.TIME_FLIPPING_CARD

    const cardSelected = (el) => {
      context.emit("card-selected", {
        indexCard: props.indexCard,
        cardValue: props.value,
        element: el
      });
    };

    return {
      cardSelected,
      durationFlipCard
    };
  },
};
</script>

