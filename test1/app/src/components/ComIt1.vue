<template>
    <div>
    <com-it2
    :questions='questions'
    />
    </div>
</template>

<script>
import ComIt2 from './ComIt2'
import questions from '../mock/questions'
export default {
    components:{
        ComIt2
    },
    data () {
        return {
            questions
        }
    },
}
</script>

<style lang="scss" scoped>
*{
    background:rgba(0, 11, 11, .8);
    border-radius:7px;
}
</style>