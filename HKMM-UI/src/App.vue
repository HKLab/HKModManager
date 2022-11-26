<template>
  <div class="d-flex">
    <!--Nav-->
    <div class="
      d-inline-flex
      flex-column
      p-3
      text-white
      bg-dark
      fill-height
    ">
      <hr />
      <ul class="nav nav-pnavills flex-column mb-auto">
        <navitem viewpath="/localmods"><i class="bi bi-hdd"></i> {{ $t("tabs.localmods") }}</navitem>
        <navitem viewpath="/allmods"><i class="bi bi-globe"></i> {{ $t("tabs.allmods") }}</navitem>
        <RequireExpmode>
          <li class="nav-item">
            <a class="nav-link text-white" @click="toggleNavTasks()" href="javascript:;">
              <i class="bi bi-list-task"></i> {{ $t("tabs.tasks.title") }}
            </a>
            <div class="list-group nav-list collapse" ref="tasksNavGroup">
              <navitem viewpath="/tasks/all" class="list-group-item" compare-path>{{ $t("tabs.tasks.all") }}
              </navitem>
              <navitem viewpath="/tasks/running" class="list-group-item" compare-path>{{ $t("tabs.tasks.running") }}
              </navitem>
              <navitem viewpath="/tasks/done" class="list-group-item" compare-path>{{ $t("tabs.tasks.done") }}
              </navitem>
              <navitem viewpath="/tasks/failed" class="list-group-item" compare-path>{{ $t("tabs.tasks.failed") }}
              </navitem>

            </div>
          </li>
        </RequireExpmode>

      </ul>
      <hr />
      <ul class="nav nav-pnavills">
        <navitem viewpath="/settings"><i class="bi bi-gear"></i> {{ $t("tabs.settings") }}</navitem>
      </ul>
    </div>
    <!--Body-->
    <div class="bg-secondary text-white flex-grow-1 app-body">
      <router-view></router-view>
    </div>
  </div>
</template>

<style>
body,
.fill-height,
#app {
  min-height: 100vh;
  max-height: 100vh;
}

.nav-list {
  --bs-list-group-bg: var(--bs-dark);
  --bs-list-group-item-padding-y: 0em;
}

.h-100 {
  height: 100%;
}

.app-body {
  max-height: 100vh;
  overflow: auto;
}

html {
  height: -webkit-fill-available;
}
</style>

<script lang="ts">
import { defineComponent } from "vue";
import { Collapse } from 'bootstrap';
import navitem from "./components/nav-item.vue";
import RequireExpmode from "./components/require-expmode.vue";

export default defineComponent({
  data: function () {
    return {};
  },
  components: {
    navitem,
    RequireExpmode,
},
  methods: {
    toggleNavTasks() {
      const group = this.$refs.tasksNavGroup as Element;
      const col = new Collapse(group);
      col.toggle();
    }
  },
});
</script>