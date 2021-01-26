<template>
  <div class="container column">
    <form class="card card-w30" @submit.prevent="submitHandler">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model="selectType">
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" rows="3" v-model.trim="formText"></textarea>
      </div>

      <button type="submit" :disabled="!isDisabled" class="btn primary">Добавить</button>
    </form>

    <div class="card card-w70">
      <div v-if="components.length > 0">
        <component
          v-for="componen in components"
          :key="componen.id"
          :is="componen.type"
          :elem="componen"
        ></component>
      </div>
      <h3 v-else>Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
  <div class="container">
    <p>
      <button class="btn primary">Загрузить комментарии</button>
    </p>
    <div class="card">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item">
          <div>
            <p><strong>test@microsoft.com</strong></p>
            <small>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi, reiciendis.</small>
          </div>
        </li>
      </ul>
    </div>
    <div class="loader"></div>
  </div>
</template>

<script>
import Title from './components/Title.vue';
import Avatar from './components/Avatar.vue';
import Subtitle from './components/Subtitle.vue';
import Text from './components/Text.vue';

export default {
  components: {
    Title, Avatar, Subtitle, Text
  },
  data: () => ({
    components: [],
    selectType: 'title',
    formText: '',
  }),
  computed: {
    isDisabled() {
      return this.formText.length > 2;
    },
  },
  methods: {
    reset() {
        this.selectType = 'title';
        this.formText = '';
    },
    submitHandler() {
      if (this.selectType === 'title') {
        this.components.push({
          type: 'Title',
          text: this.formText,
          id: Math.random(),
        })
      }
      if (this.selectType === 'avatar') {
        this.components.push({
          type: 'Avatar',
          text: this.formText,
          id: Math.random(),
        })
      }
      if (this.selectType === 'subtitle') {
        this.components.push({
          type: 'Subtitle',
          text: this.formText,
          id: Math.random(),
        })
      }
      if (this.selectType === 'text') {
        this.components.push({
          type: 'Text',
          text: this.formText,
          id: Math.random(),
        })
      }
      this.reset();
    }
  }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
