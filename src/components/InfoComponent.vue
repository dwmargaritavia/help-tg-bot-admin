<template>
    <div id="info_page">
        <h3>Информация о заявке</h3>
        <div class="info_body">
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
        <div class="info_actions">
            <button type="button" class="btn btn-success">Принять</button>
            <button type="button" class="btn btn-danger">Отклонить</button>
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
    return {}
  },
  methods: {}
}
</script>
<style scoped>
#info_page {
    padding: 20px;
    color: white;
}

.info_actions {
    display: flex;
    justify-content: space-evenly;
}

.table_info {
    margin-bottom: 20px;
    min-width: 320px;
}

.table_info td {
    border-width: 1px;
    padding: 5px;
}
</style>