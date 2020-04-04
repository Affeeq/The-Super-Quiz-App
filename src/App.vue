<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-8 col-md-6 col-md-offset-3">
        <h1 class="text-center">The Super Quiz</h1>
        <hr>
        <div class="col-4"></div>
        <div class="col-4 text-center">
          <transition
            name="flip"
            mode="out-in">
              <component :is="selectedComponent" :selectedComponent="selectedComponent" @answerChecked="selectedComponent = $event"></component>
          </transition>
        </div>
        <div class="col-4"></div>
    </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Question from './Question.vue';
  import Success from './Success.vue';
  export default {
    data() {
      return {
        selectedComponent: 'app-question',
        animateComponent: 'flipOutY'
      }
    },
    components: {
      appQuestion: Question,
      appSuccess: Success
    }
  }
</script>

<style>
  .flip-enter {
    opacity: 0;
  }

  .flip-enter-active {
    animation: flip-left .7s ease-in;
  }

  .flip-leave {
    opacity: 1;
  }

  .flip-leave-active {
    animation: flip-right .7s ease-out;
  }

  @keyframes flip-right {
    from {
      transform: rotateY(0);
    }
    to {
      transform-style: preserve-3d;
      transform: rotateY(90deg);
    }
  }

  @keyframes flip-left {
    from {
      transform-style: preserve-3d;
      transform: rotateY(-90deg);
    }
    to {
      transform: rotateY(0);
    }
  }
</style>
