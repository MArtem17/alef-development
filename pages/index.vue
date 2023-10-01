<template>
  <div>
    <v-form ref="form" v-model="valid" lazy-validation>
      <h2>Персональные данные</h2>
      <v-text-field v-model="name" :rules="nameRules" label="Имя" placeholder="Введите своё имя" outlined></v-text-field>
      <v-text-field v-model="age" :rules="ageRules" label="Возраст" placeholder="Введите свой возраст"
        outlined></v-text-field>
      <div class="child__header">
        <h2>Дети (макс. 5)</h2>
        <v-spacer></v-spacer>
        <v-btn class="btn" v-if="childrens.length < 5" rounded outlined color="#01A7FD" @click="addNewChild()">
          + Добавить ребёнка
        </v-btn>
      </div>
      <v-row v-for="(child, i) in childrens" :key="i" style="margin-top: -30px;">
        <v-col cols="5">
          <v-text-field v-model="child.name" :rules="nameRules" label="Имя" placeholder="Введите имя ребёнка"
            outlined></v-text-field>
        </v-col>
        <v-col cols="5">
          <v-text-field v-model="child.age" :rules="ageRules" label="Возраст" placeholder="Введите возраст ребёнка"
            outlined></v-text-field>
        </v-col>
        <v-col cols="2">
          <v-btn class="btn" plain color="#01A7FD" style="margin-top: 10px;" @click="delChild(i)">
            Удалить
          </v-btn>
        </v-col>
      </v-row>
      <v-btn class="btn" dark rounded color="#01A7FD" @click="saveData()">
        Сохранить
      </v-btn>
    </v-form>
    <v-snackbar absolute :timeout="5000" v-model="snackbar" color="success" outlined rounded="pill">
      Данные успешно сохранены, Вы можете их увидеть на станице Превью
    </v-snackbar>
  </div>
</template>

<style>
.child__header {
  display: flex;
  margin-bottom: 40px;
}

.btn {
  text-transform: none;
  font-size: 14px;
  line-height: 24px;
  font-weight: 400;
}
</style>

<script>
export default {
  name: 'index',
  data: () => ({
    name: "",
    age: "",
    childrens: [],
    valid: true,
    nameRules: [
      v => !!v || 'Введите имя',
      v => /^[A-Za-zА-Яа-я ]+$/.test(v) || 'В имени могут присутствовать только буквы',
    ],
    ageRules: [
      v => !!v || 'E-mail is required',
      v => /^[0-9]+$/.test(v) || 'В возрасте могут присутствовать только цифры',
    ],
    snackbar: false,
  }),
  methods: {
    addNewChild() {
      this.childrens.push({
        name: "",
        age: null
      })
    },
    delChild(i) {
      this.childrens.splice(i, 1)
    },
    saveData() {
      if (this.$refs.form.validate()) {
        const data = {
          name: this.name,
          age: this.age,
          childrens: this.childrens
        }
        sessionStorage.setItem("data", JSON.stringify(data))
        this.snackbar = true
      }
    }
  }
}
</script>
