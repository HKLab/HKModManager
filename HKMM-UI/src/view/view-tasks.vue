<template>
    <div class="accordion">
        <CTasksItem v-for="(task) in getTasks()" :key="task.taskGuid" :taskguid="task.taskGuid"></CTasksItem>
    </div>
</template>

<script lang="ts">
import { allTasks, TaskInfo } from '@/renderer/taskManager';
import { defineComponent } from 'vue';
import CTasksItem from './tasks/c-tasks-item.vue';

export default defineComponent({
    components: { CTasksItem },
    props: {
        filter: String
    },
    methods: {
        getTasks() {
            const arr: TaskInfo[] = [];
            for (let i = 0; i < allTasks.length; i++) {
                const e = allTasks[i];
                if(e.isHidden) continue;
                if(e.isFailed && this.filter === 'failed') arr.push(e);
                if(e.isSuccess && this.filter === 'done') arr.push(e);
                if(!e.isSuccess && !e.isFailed && this.filter === 'running') arr.push(e);
                if(!this.filter || this.filter === 'all') arr.push(e);
            }
            return arr.reverse();
        }
    },
    data() {
        return {
            checkTimer: setInterval(() => this.$forceUpdate(), 1000)
        }
    },
    created() {
        this.$watch(() => this.$route.params, () => {
            this.$forceUpdate();
        });
        this.$watch(() => allTasks, () => {
            this.$forceUpdate();
        });
    },
    unmounted() {
        clearInterval(this.checkTimer);
    }
});
</script>
