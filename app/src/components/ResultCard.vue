<template>
    <transition appear name="fade">
        <div class="relative shadow-xl sm:rounded-2xl sm:overflow-hidden">
            <div class="absolute inset-0">
                <img class="h-full w-full object-cover hidden" src="https://images.unsplash.com/photo-1521737852567-6949f3f9f2b5?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=2830&q=80&sat=-100" alt="People working on laptops" />
                <div :class="'absolute inset-0 bg-' + getResultColor + '-700'" />
            </div>
            <div class="relative">
                 <div :class="'bg-' + getResultColor + '-900'">
                    <div class="max-w-7xl mx-auto py-3 px-3 sm:px-6 lg:px-8">
                        <div class="flex items-center justify-between flex-wrap">
                        <div class="w-0 flex-1 flex items-center">
                            <p class="ml-3 font-medium text-white truncate">
                            <span class="md:hidden">
                                {{currCategory}}
                            </span>
                            <span class="hidden md:inline">
                               {{currCategory}} 
                            </span>
                            </p>
                        </div>
                        <div class="flex-1 px-8 sm:px-6 lg:px-10">
                            <div class="relative">
                                <div :class="'overflow-hidden h-2 text-xs flex rounded bg-' + getResultColor + '-200'">
                                    <div :style="'width:' + catCompletionPercentage + '%'" :class="'shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-' + getResultColor + '-500'"></div>
                                </div>
                            </div>
                        </div>
                        </div>
                    </div>
                </div>
                <div class="px-4 py-16 sm:px-6 sm:py-24 lg:py-32 lg:px-8">
                    <h1 v-html="text" class="result-text mt-10 mx-10 text-center text-l font-medium tracking-tight sm:text-xl lg:text-2xl text-white">
                    </h1>
                    <div class="mt-10 max-w-sm mx-auto sm:max-w-none sm:flex sm:justify-center">
                        <div class="space-y-4 sm:space-y-0 sm:mx-auto sm:inline-grid sm:grid-cols-1 sm:gap-5">
                            <button @click="nextQuestion" :class="'flex items-center justify-center px-4 py-3 border border-transparent text-base font-medium rounded-md shadow-sm text-' + getResultColor + '-700 bg-white hover:bg-' + getResultColor + '-50 sm:px-8'">
                                Next question
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </transition>
</template>
<script>
import store from '../store'

export default {
    name : 'ResultCard',
    computed: {
        currCategory () {
            return store.state.quiz.currCategory
        },
        score () {
            return store.state.quiz.currResultScore
        },
        text () {
            return store.state.quiz.currResultHTML
        },
        getResultColor () {
            let color
            switch(this.score) {
                case 0:
                    color = 'red'
                    break;
                case 0.5:
                    color = 'yellow'
                    break;
                case 1:
                    color = 'green'
                    break;
                default:
                    color = 'green'
            }
            return color;
        },
        catCompletionPercentage () {
            return store.state.quiz.currCategoryCompletion * 100
        }
    },
    methods : {
        nextQuestion () {
            store.dispatch("quiz/nextTopLevelQuestion")
        }
    }
}
</script>
<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity 1s ease-in;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>