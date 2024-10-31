<template>
  <div class="page">
    <div id="regulars_page">
        <h3>Обычные заявки</h3>
        <ol class="list-group">
            <li class="list-group-item d-flex justify-content-between align-items-start" v-for="(item, index) in items" v-bind:key="index" v-on:click="show_info(item)">
                <div class="ms-2 me-auto">
                    <div class="fw-bold"> #{{ item.id }} {{ item.userName }} ({{ item.userPronouns }})</div>
                    {{ item.requestText.substring(0,24) + '...' }}
                </div>
                <span class="badge text-bg-primary rounded-pill">{{ item.requestDate }}</span>
            </li>
        </ol>
    </div>
    <InfoComponent v-if="info_show" v-bind:item="current_item"></InfoComponent>
  </div>
</template>
<script>
import InfoComponent from './InfoComponent.vue';

export default {
  name: 'RegularComponent',
  components: {
    InfoComponent
  },
  props: {
    items: Array
  },
  data() {
    return {
      info_show: false,
      current_item: {}
    }
  },
  methods: {
    show_info(item) {
      this.current_item = item;
      this.info_show = true;
    }
  }
}
</script>
<style scoped>
#regulars_page {
    width: 360px;
    padding: 20px;
    background-color: #001245;
    color: white;
}
</style>