<template>
    <div id="chat_page">
        <h3>Заявка {{ item.id }} от {{ item.userName }} ({{ item.userPronouns }})</h3>
        <button type="button" class="btn btn-outline-success btn-hs" v-if="!info_show" v-on:click="show_info">Показать информацию</button>
        <button type="button" class="btn btn-outline-warning btn-hs" v-if="info_show" v-on:click="hide_info">Скрыть информацию</button>
        <div class="info_body" v-if="info_show">
          <table class="table_info">
            <tr><td><b>ID заявки</b></td><td>{{ item.id }}</td></tr>
            <tr><td><b>ID чата в ТГ</b></td><td>{{ item.tgChatId }}</td></tr>
            <tr><td><b>Имя</b></td><td>{{ item.userName }}</td></tr>
            <tr><td><b>Местоимения</b></td><td>{{ item.userPronouns }}</td></tr>
            <tr><td><b>Дата заявки</b></td><td>{{ item.requestDate }}</td></tr>
            <tr><td><b>Текст</b></td><td>{{ item.requestText }}</td></tr>
            <tr><td><b>В работе</b></td><td>{{ item.inWork }}</td></tr>
            <tr><td><b>В архиве</b></td><td>{{ item.inTheArchive }}</td></tr>
            <tr><td><b>ID админа в ТГ</b></td><td>{{ item.relatedAdminId }}</td></tr>
            <tr><td><b>Срочно</b></td><td>{{ item.urgent }}</td></tr>
          </table>
        </div>
        <button type="button" class="btn btn-outline-primary btn-hs" v-on:click="load_chat">Перезагрузить чат</button>
        <div class="chat_body">
          <div class="card msg" v-for="(msg, index) in messages" v-bind:key="index">
            <div class="card-body">
              <h5 class="card-title" v-if="msg.fromAdmin">Admin</h5>
              <h5 class="card-title" v-if="!msg.fromAdmin">{{ msg.request.userName }}</h5>
              <h6 class="card-subtitle mb-2 text-body-secondary">{{  msg.timestamp }}</h6>
              <p class="card-text">{{ msg.messageText }}</p>
            </div>
          </div>
        </div>
    </div>
</template>
<script>
export default {
  name: 'InfoComponent',
  props: {
    item: Object
  },
  data() {
    return {
      info_show: false,
      messages: []
    }
  },
  methods: {
    show_info() {
      this.info_show = true;
    },
    hide_info() {
      this.info_show = false;
    },
    load_chat() {
      this.messages = [];
      fetch(this.$parent.$parent.server + '/message/get/' + this.item.id)
      .then(response => response.json()).then(result => {
        this.messages = result;
      });
    },
  },
  watch: {
    item() {
      this.load_chat();
    }
  }
}
</script>
<style scoped>
#chat_page {
    padding: 20px;
}

.table_info {
    margin-bottom: 20px;
    min-width: 320px;
}

.table_info td {
    border-width: 1px;
    padding: 5px;
}

.btn-hs {
  margin-bottom: 10px;
  margin-right: 10px;
}

.chat_body {
    font-size: 14px;
    background-color: #5b5b5b;
    overflow-y: scroll;
    height: 70vh;
}

.msg {
    margin: 10px;
    max-width: 720px;
}
</style>