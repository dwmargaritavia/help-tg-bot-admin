<template>
  <nav id="main-menu" class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container-fluid">
      <a class="navbar-brand" href="#" v-on:click="hide_all"><img id="tg_flag" src="./assets/transgender_pride_flag.svg" /> HelpBot Admin</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item li-imm" id="imm-1">
            <a class="nav-link" v-bind:class="{ active: urgent_list_show }" href="#" id="imm-urgent" v-on:click="load_urgents">Срочные заявки</a>
          </li>
          <li class="nav-item li-imm" id="imm-2">
            <a class="nav-link" v-bind:class="{ active: regular_list_show }" href="#" id="imm-regular" v-on:click="load_regulars">Обычные заявки</a>
          </li>
          <li class="nav-item li-imm" id="imm-3">
            <a class="nav-link" v-bind:class="{ active: processing_list_show }" href="#" id="imm-processing" v-on:click="load_processings">Заявки в работе</a>
          </li>
          <li class="nav-item li-imm" id="imm-4">
            <a class="nav-link" v-bind:class="{ active: login_show }" href="#" id="imm-login" v-on:click="load_login">Авторизация</a>
          </li>
          <li class="nav-item li-imm" id="imm-5">
            <a class="nav-link" v-bind:class="{ active: about_show }" href="#" id="imm-about" v-on:click="load_about">Справка</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <UrgentComponent v-if="urgent_list_show" v-bind:items="urgents"></UrgentComponent>
  <RegularComponent v-if="regular_list_show" v-bind:items="regulars"></RegularComponent>
  <ProcessingComponent v-if="processing_list_show" v-bind:items="processings"></ProcessingComponent>
  <AboutComponent v-if="about_show"></AboutComponent>
</template>
<script>
import UrgentComponent from './components/UrgentComponent.vue';
import RegularComponent from './components/RegularComponent.vue';
import ProcessingComponent from './components/ProcessingComponent.vue';
import AboutComponent from './components/AboutComponent.vue';

export default {
  name: 'App',
  components: {
    UrgentComponent,
    RegularComponent,
    ProcessingComponent,
    AboutComponent
  },
  data() {
    return {
      server_host: 'eve.test:8080',
      server_protocol: 'http://',
      server_api: '/api',
      urgent_list_show: false,
      regular_list_show: false,
      processing_list_show: false,
      login_show: false,
      about_show: false,
      urgents: [],
      regulars: [],
      processings: []
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
      this.processing_list_show = false;
      this.login_show = false;
      this.about_show = false;
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
    },
    load_processings() {
      this.hide_all();
      this.processings = [];
      fetch(this.server + '/request/my')
      .then(response => response.json()).then(result => {
        this.processings = result;
        this.processing_list_show = true;
      });
    },
    load_login() {
      this.hide_all();
      this.login_show = true;
    },
    load_about() {
      this.hide_all();
      this.about_show = true;
    }
  }
}
</script>
<style>
#main-menu {
    padding: 0;
}

#tg_flag {
    height: 20px;
}

#imm-1 {
    background-color: #5BCEFA;
}

#imm-2 {
    background-color: #F5A9B8;
}

#imm-3 {
    background-color: #FFF;
}

#imm-4 {
    background-color: #F5A9B8;
}

#imm-5 {
    background-color: #5BCEFA;
}

.li-imm {
    padding: 10px;
    min-width: 170px;
}

.page {
    display: flex;
}
</style>