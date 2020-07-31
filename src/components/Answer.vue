<template>
    <div class="alert alert-success">
        <div>
            <h3 class="display-3"> That was CORRECT!</h3>
        </div>
        <hr>
        <div>
            <button class="btn btn-lg btn-block btn-success" @click="nextQuestion"> NEXT QUESTION</button>
        </div>
    </div>
</template>
<script>
    export default {
        methods: {
            nextQuestion() {
                this.$emit('next')
            }
        }
    }
</script>