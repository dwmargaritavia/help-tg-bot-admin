<template>
  <nav id="main-menu" class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">HelpBot Admin</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link" href="#" id="imm-urgent" v-on:click="load_urgents">Срочные заявки</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#" id="imm-regular" v-on:click="load_regulars">Обычные заявки</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#" id="imm-processing">Заявки в обработке</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <UrgentComponent v-if="urgent_list_show" v-bind:items="urgents"></UrgentComponent>
  <RegularComponent v-if="regular_list_show" v-bind:items="regulars"></RegularComponent>
</template>
<script>
import UrgentComponent from './components/UrgentComponent.vue';
import RegularComponent from './components/RegularComponent.vue';

export default {
  name: 'App',
  components: {
    UrgentComponent,
    RegularComponent
  },
  data() {
    return {
      server_host: 'eve.test:8080',
      server_protocol: 'http://',
      server_api: '/api',
      urgent_list_show: false,
      regular_list_show: false,
      urgents: [],
      regulars: []
    };
  },
  computed: {
    server() {
      return this.server_protocol + this.server_host + this.server_api;
    }
  },
  methods: {
    hide_all() {
      this.urgent_list_show = false;
      this.regular_list_show = false;
    },
    load_urgents() {
      this.hide_all();
      this.urgents = [];
      fetch(this.server + '/request/urgent')
      .then(response => response.json()).then(result => {
        this.urgents = result;
        this.urgent_list_show = true;
      });
    },
    load_regulars() {
      this.hide_all();
      this.regulars = [];
      fetch(this.server + '/request/regular')
      .then(response => response.json()).then(result => {
        this.regulars = result;
        this.regular_list_show = true;
      });
    }
  }
}
</script>
<style>
.page {
    display: flex;
}
</style>