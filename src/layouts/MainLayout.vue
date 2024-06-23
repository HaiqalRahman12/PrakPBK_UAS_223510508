<template>
  <q-layout view="hHh lpR fff">

<q-header bordered class="bg-rgba(0, 0, 0, 0.5) text-white" height-hint="98">
  <q-toolbar>
    <q-toolbar-title>
      Haiqal Rahman
    </q-toolbar-title>
    <div class="q-pa-md">
    <q-btn-dropdown color="bg-rgba(0, 0, 0, 0.5)" label="Tugas">
      <q-list>
        <q-item
          v-for="(task, index) in tasks"
          :key="index"
          clickable
          v-close-popup
          @click="navigateToTask(task.value)"
        >
          <q-item-section>
            <q-item-label>{{ task.label }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-btn-dropdown>
  </div>

    <q-tabs align="right">
    <q-route-tab to="/Weather" label="Weather" />
  </q-tabs>
  </q-toolbar>
</q-header>

<q-page-container>
  <router-view />
</q-page-container>

<q-footer elevated class="bg-#87ceeb text-white">
  <q-toolbar>
    <q-toolbar-title>
      <div class="foter">Copyright © 2024 Haiqal Rahman. All Rights Reserved.</div>
    </q-toolbar-title>
  </q-toolbar>
</q-footer>

</q-layout>
</template>

<script setup>
import { ref } from 'vue';

const tasks = ref([
  { label: "Tugas 1", value: "https://haiqal-projectcv.netlify.app/" },
  {
    label: "Tugas 2",
    value: "https://haiqal-prakpbk2.netlify.app/",
  },
  { label: "Tugas 3", value: "https://223510508-haiqal.netlify.app/" },
  {
    label: "Tugas 4",
    value: "https://haiqal-prakpbk4.netlify.app/",
  },
  { label: "Tugas 5", value: "https://haikal-landingpage.netlify.app/" },
  { label: "Tugas 6", value: "https://prakpbktugas6-haiqal-223510508.netlify.app/" },
]);

const navigateToTask = (url) => {
  window.location.href = url;
};
</script>

<style scoped>
.q-toolbar{
  background-color: rgba(0, 0, 0, 0.5);
  padding: 0 70px ;
}
.q-layout {

  font-size: 10px;
  
}

.foter{
  display: flex;
  justify-content: center;
  font-size: 10px;
}

</style>