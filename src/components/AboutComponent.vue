<template>
    <div id="about_page">
        <h3>Справка</h3>
        <img id="about_tg_flag" src="../assets/transgender_pride_flag.svg" />
        <p>Эта админка - веб-приложение для управления заявками телеграм-бота помощи Центра Т <a target="_blank" href="https://t.me/help_centre_t_bot">@help_centre_t_bot</a></p>
        <p><a href="https://github.com/dwmargaritavia/help-tg-bot-admin" target="_blank">Ссылка</a> на репозиторий исходного кода (возможно потребуется запросить доступ)</p>
        <p>Разработчица <i>Margarita Vía</i> (она), Telegram: <a target="_blank" href="https://t.me/dwmargaritavia">@dwmargaritavia</a></p>
    </div>
</template>
<script>
export default {
  name: 'AboutComponent',
  data() {
    return {}
  },
  methods: {}
}
</script>
<style scoped>
#about_page {
    padding: 20px;
    text-align: center;
}

img#about_tg_flag {
    width: 320px;
    margin: 20px;
}
</style>