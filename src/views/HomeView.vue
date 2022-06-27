<template>
  <v-containiter>
    <v-row>
      <v-col cols="12">
        <h1 class="text-center py-10">人員清單</h1>
      </v-col>
    </v-row>

    <v-row>
      <v-col md="4" cols="12" v-for="user in currentUsers" :key="user.UID">
        <v-card class="d-flex flex-column px-5 py-3 rounded-lg" height="150px">
          <div class="d-flex align-center flex-grow-0">
            <h3 class="primary--text"><strong>{{user.name}}</strong></h3>
            <h4 class="gray--text ml-auto">{{handleGender(user.gender)}}</h4>
          </div>
          <div class="flex-grow-0">
            <span class="gray--text">{{user.UID}}</span>
          </div>
          <div class="flex-grow-1 d-flex align-end">
            <v-icon left color="seconsary">
              mdi-gmail
            </v-icon>
            <span class="seconsary--text">{{user.email}}</span>
          </div>
        </v-card>
      </v-col>
    </v-row>


    <v-row class="mt-8">
      <v-col cols="12">
        <v-pagination v-model="page" :length="totalPages"/>
      </v-col>

    </v-row>
  </v-containiter>
</template>


<script>
import admin from "../assets/admin.json";
export default {
  data(){
    return {
      user:[],
      page: 1
    };
  },
  created(){
    this.getUsers();
  },
  computed: {
    //計算總頁數
    totalPages() {
      return Math.ceil(this.users.length / 9);
    },
    currentUsers() {
      const begin = (this.page - 1) * 9;
      const end = begin + 9;
      return this.users.slice(begin, end);
      },
  },
  methods: {
    getUsers() {
      this.users = admin.data.user;
    },

    handleGender(type) {
    if (type === "M") return "男";
    if (type === "W") return "女";
    return "其他";
    }
  },
};

  



</script>

<style>

</style>