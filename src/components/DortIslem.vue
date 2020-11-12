<template>
  <div class="form-group">
    <label for="">Sayı 1:</label>
    <input id="sayiBir" type="text" v-model="dortIslem.sayiBir" />
    <label for="">Sayı 2:</label>
    <input id="sayiIki" type="text" v-model="dortIslem.sayiIki" /><br /><br />
    <button class="btn btn-primary" @click="carp">Çarpma</button>
    <button class="btn btn-primary" @click="bol">Bölme</button>
    <button class="btn btn-primary" @click="topla">Toplama</button>
    <button class="btn btn-primary" @click="cikar">Çıkarma</button><br />
    <p>{{ sonuc }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dortIslem: {
        sayiBir: "",
        sayiIki: ""
      },
      sonuc: ""
    };
  },
  methods: {
    carp() {
      var result = this.dortIslem.sayiBir * this.dortIslem.sayiIki;
      this.sonuc = result;
      this.dortIslem = {};
      setTimeout(() => {
        this.sonuc = "";
      }, 3000);
      //   alert(sonuc);
      console.log(result);
    },
    bol() {
      var result = this.dortIslem.sayiBir / this.dortIslem.sayiIki;
      this.sonuc = result;
      this.dortIslem = {};
      setTimeout(() => {
        this.sonuc = "";
      }, 3000);
    },
    topla() {
      var result =
        parseInt(this.dortIslem.sayiBir) + parseInt(this.dortIslem.sayiIki);
      this.sonuc = result;
      this.dortIslem = {};
      setTimeout(() => {
        this.sonuc = "";
      }, 3000);
    },
    cikar() {
      var result = this.dortIslem.sayiBir - this.dortIslem.sayiIki;
      this.sonuc = result;
      this.dortIslem = {};
      //   setTimeout(() => {
      //     this.sonuc = "";
      //   }, 3000);
    }
  }
};
</script>

<style scoped></style>




    <ul class="list-group">
          <!-- <pre>{{ postList }}</pre> -->
          <li class="list-group-item" v-for="post in postList" :key="post.id">
            <div class="col-6">
              <h4>
                <h5>{{ post.userName }}</h5>
              </h4>
              <br />
              <h6>{{ post.password }}</h6>
              <br />
            </div>
            <br />
            <button class="btn btn-warning" @click="deleteUser(post.id)">
              Sil
            </button>
            <button class="btn btn-success" @click="updateUser(post.id)">
              Güncelle
            </button>
          </li>
        </ul>