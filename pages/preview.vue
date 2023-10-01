<template>
  <client-only>
    <div>
      <div v-if="loaded">
        <h2>Персональные данные</h2>
        <p class="user">{{ dataUser.name }}, {{ dataUser.age }} {{ textAge(dataUser.age) }}</p>
        <div class="child" v-if="dataUser.childrens.length">
          <h2>Дети</h2>
          <v-sheet width="fit-content" class="child__item" color="#F1F1F1" rounded
            v-for="(child, i) in dataUser.childrens" :key="i">
            <span>{{ child.name }}, {{ child.age }} {{ textAge(child.age) }}</span>
          </v-sheet>
        </div>
      </div>
      <h2 v-else>Для просмотра необходимо заполнить и сохранить данные</h2>
    </div>
  </client-only>
</template>

<style>
.user {
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;
  color: #111111;
  margin: 20px 0px;
}

.child {
  margin-top: 60px;
}

.child__item {
  padding: 10px 20px;
  margin: 20px 0px;
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;
  color: black;
}
</style>

<script>
export default {
  name: 'preview',
  data: () => ({
    loaded: false,
    dataUser: null
  }),
  beforeMount() {
    if (JSON.parse(sessionStorage.getItem("data")) != null) {
      this.dataUser = JSON.parse(sessionStorage.getItem("data"))
      this.loaded = true
    }
  },
  methods: {
    textAge(age) {
      if (age % 10 == 1 && age % 100 != 11) {
        return "год"
      } else if ((age % 10 == 2 || age % 10 == 3 || age % 10 == 4) && (age % 100 != 12 || age % 100 != 13 || age % 100 != 14)) {
        return "года"
      } else {
        return "лет"
      }
    }
  }
}
</script>
