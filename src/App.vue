<template>
  <body class="p-5">
    <div id="app">
      <div class="container" style="margin-top:20px">
        <button class="btn btn-info float-right" @click="userNew">
          Yeni Kullanıcı</button
        ><br /><br />
        <div class="modal fade" tabindex="-1" role="dialog" id="userModal">
          <div class="modal-dialog" role="document">
            <div class="modal-content">
              <form @submit.prevent="saveUser">
                <div class="modal-header">
                  <h3 class="modal-title">Kullanıcı Kaydı</h3>
                  <button
                    type="button"
                    class="close"
                    data-dismiss="modal"
                    aria-label="Close"
                  >
                    <span aria-hidden="true">&times;</span>
                  </button>
                </div>
                <div class="modal-body">
                  <div class="form-group">
                    <label for="userName">User Name</label>
                    <input
                      type="text"
                      name="userName"
                      id="userName"
                      v-model="post.userName"
                      class="form-control"
                    />
                  </div>
                  <div class="form-group">
                    <label for="password">Password</label>
                    <input
                      type="password"
                      name="password"
                      id="password"
                      v-model="post.password"
                      class="form-control"
                    />
                  </div>
                </div>
                <div class="modal-footer">
                  <input
                    type="submit"
                    class="btn btn-primary"
                    :value="post.id > 0 ? 'Güncelle' : 'Kaydet'"
                  />
                  <button
                    type="button"
                    class="btn btn-secondary"
                    data-dismiss="modal"
                  >
                    Kapat
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>

        <table class="table table-bordered table-hover">
          <tr v-for="post in postList" :key="post.id">
            <td>{{ post.userName }}</td>
            <td>{{ post.password }}</td>
            <td>
              <button class="btn btn-success" @click="updateUser(post.id)">
                Güncelle
              </button>
            </td>
            <td>
              <button class="btn btn-warning" @click="deleteUser(post.id)">
                Sil
              </button>
            </td>
          </tr>
        </table>
      </div>
    </div>
  </body>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      post: {
        id: null,
        userName: "",
        password: ""
      },
      postList: []
    };
  },
  // components: {
  //   "dort-islem": DortIslem
  // },
  created() {
    axios
      .get("http://localhost:8080/api/users")
      .then(response => {
        let data = response.data;
        this.postList = response.data;
      })
      .catch(e => {
        console.log(e);
      });
  },
  methods: {
    userNew() {
      this.post = {};
      $("#userModal").modal("show");
    },
    saveUser() {
      axios
        .post("http://localhost:8080/api/users/post/", { ...this.post })
        .then(response => {
          this.post = {};
          $("#userModal").modal("hide");
          window.location.reload();
        });
    },
    deleteUser(id) {
      axios
        .delete("http://localhost:8080/api/users/delete/" + id)
        .then(response => {
          this.postList.splice(id, 1);
        });
      window.location.reload();
    },
    updateUser(id) {
      axios
        .get("http://localhost:8080/api/users/" + id)
        .then(response => {
          let data = response.data;
          this.post = response.data;
          $("#userModal").modal("show");
        })
        .catch(e => {
          console.log(e);
        });
    }
  }
};
</script>

<style scoped></style>
