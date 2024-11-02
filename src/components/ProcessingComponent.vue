<template>
  <div class="page">
    <div id="processing_page">
        <h3>Заявки в работе</h3>
        <ol class="list-group">
            <li class="list-group-item d-flex justify-content-between align-items-start" v-for="(item, index) in items" v-bind:key="index" v-on:click="show_chat(item)">
                <div class="ms-2 me-auto">
                    <div class="fw-bold"> #{{ item.id }} {{ item.userName }} ({{ item.userPronouns }})</div>
                    {{ item.requestText.substring(0,24) + '...' }}
                </div>
                <span class="badge text-bg-primary rounded-pill">{{ item.requestDate }}</span>
            </li>
        </ol>
    </div>
    <ChatComponent v-if="chat_show" v-bind:item="current_item"></ChatComponent>
  </div>
</template>
<script>
import ChatComponent from './ChatComponent.vue';

export default {
  name: 'ProcessingComponent',
  components: {
    ChatComponent
  },
  props: {
    items: Array
  },
  data() {
    return {
      chat_show: false,
      current_item: {}
    }
  },
  methods: {
    show_chat(item) {
      this.chat_show = false;
      this.current_item = item;
      this.chat_show = true;
    }
  }
}
</script>
<style scoped>
#processing_page {
    width: 360px;
    padding: 20px;
    background-color: #3e0057;
    color: white;
}
</style>