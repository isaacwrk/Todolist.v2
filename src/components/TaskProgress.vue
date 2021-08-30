<template>
    <div class="tasks-progress">
        <span class="progress-value">{{ progress }}%</span>
        <div class="progress-bar" :style="{width: progress + '%'}"></div>
    </div>
</template>

<script>
export default {
    props:{
        progress:{type:Number, default:0}
    }
}
</script>

<style>
    .tasks-progress{
        position: relative;
        width: 80%;
        border: 1px solid #FFF;
        border-radius: 8px;
        margin-bottom: 15px;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .progress-bar{
        position: absolute;
        height: 100%;
        border-radius: 8px;
        background: linear-gradient(270deg, rgba(204,236,10,1) 0%, rgba(0,236,255,1) 100%);;
        align-self: flex-start;
    }

    .progress-value{
        z-index: 1;
        font-size:1.5rem;
    }
</style>