<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1 class="text-center">The Super Quiz</h1>
            </div>
        </div>
        <hr>
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
            <!--ToDo: Load component in a transition element/tag-->
                <!--set the name attribute to flip, which you will create in the styles below-->
                <!--use an attribute called mode and set it to out-in, this allows the component to finish what it is doing before loading the new question-->
                <transition name="flip" mode="out-in">
                    <component :is="mode" @answered="answered($event)" @confirmed="mode = 'app-question'"></component>
                </transition>

            </div>
        </div>
    </div>
</template>

<script>
    import Question from './components/Question.vue';
    import Answer from './components/Answer.vue';

    export default {
        data() {
            return {
                mode: 'app-question'
            }
        },
        methods: {
          answered(isCorrect) {
              if (isCorrect) {
                  this.mode = 'app-answer';
              } else {
                  this.mode = 'app-question';
                  alert('Wrong, try again!');
              }
          }
        },
        components: {
            appQuestion: Question,
            appAnswer: Answer
        }
    }
</script>

<style>
     /*ToDo: Create flip-enter-active class */
        /*use CSS animation, which will take 4 arguments*/
            /*the type of animation: for this exercise we will be using flip-in*/
            /*the time it should take to animate, use a time you prefer*/
            /*an easing function, for this exercise use ease-out*/
            /*lastly: use forwards so that it will stay in the final place and not snap back to where it started*/
    .flip-enter-active {
        animation: flip-in 1s ease-out forwards;
    }

     /*ToDo: Create flip-leave-active class */
         /*use CSS animation, which will take 4 arguments*/
            /*the type of animation: for this exercise we will be using flip-out*/
            /*the time it should take to animate, use a time you prefer*/
            /*an easing function, for this exercise use ease-out*/
             /*lastly: use forwards so that it will stay in the final place and not snap back to where it started*/
    .flip-leave-active {
        animation: flip-out 1s ease-out forwards;
    }

     /*ToDo: Create the flip-out using keyframes */
        /*from: you will use transform and rotate it along Y axis by 0 deg*/
     /*to: you will use transform and rotate it along Y axis by 90 deg*/
     @keyframes flip-out {
         from {
             transform: rotateY(0deg);
         }
         to {
             transform: rotateY(90deg);
         }
     }

     /*ToDo: Create the flip-in using keyframes */
         /*from: you will use transform and rotate it along Y axis by 90 deg*/
         /*to: you will use transform and rotate it along Y axis by 0 deg*/
     @keyframes flip-in {
         from {
             transform: rotateY(90deg);
         }
         to {
             transform: rotateY(0deg);
         }
     }

</style>

