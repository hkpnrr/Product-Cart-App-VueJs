<template>
<div class="progress">
    <div class="progress-bar bg-info" role="progressbar" :style="{width : progress+'%'}" aria-valuenow="50" aria-valuemin="0" aria-valuemax="100">
        {{currentItemCount}}/5
    </div>
</div>
</template>

<script>
import {
    eventBus
} from '../main';
export default {

    data() {
        return {
            progress: 0,
            currentItemCount:0
        }
    },
    created() {
        eventBus.$on('updateProgressBar', (data) => {
            this.currentItemCount = data;
            this.progress=data*20;
        })
    }

}
</script>
