<template>
  <!-- Portfolio Section -->
  <section class="page-section">
    <b-container>
      <HeaderPage title="Adicionar Especialista" />

      <!--FORM-->
      <b-row>
        <b-col cols="2"></b-col>
        <b-col>
          <form @submit.prevent="add">
            <div class="form-group">
              <input
                v-model="name"
                type="text"
                class="form-control form-control-lg"
                id="txtName"
                placeholder="escreve nome"
                required
              />
            </div>
            <div class="form-group">
              <input
                v-model="email"
                type="text"
                class="form-control form-control-lg"
                id="txtEmail"
                placeholder="escreve email"
                required
              />
            </div>
            <div class="form-group">
              <select id="sltGroup" class="form-control form-control-lg" v-model="animals" required>
                <option value>-- SELECIONA ANIMAIS --</option>
                <option value="trigre">Tigre</option>
                <option value="leão">Leão</option>
                <option value="urso">Urso</option>
                <option value="touro">Touro</option>
              </select>
            </div>
            <button type="submit" class="btn btn-outline-success btn-lg mr-2">
              <i class="fas fa-plus-square"></i>  ADICIONAR</button>
            <router-link
              :to="{name: 'listSpecialists'}"
              tag="button"
              class="btn btn-outline-danger btn-lg"
            ><i class="fas fa-window-close"></i>  CANCELAR</router-link>
          </form>
        </b-col>
        <b-col cols="2"></b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
import { ADD_SPECIALIST } from "@/store/specialists/specialist.constants";
import HeaderPage from "@/components/HeaderPage.vue";
import router from "@/router";
import { mapGetters } from "vuex";

export default {
  name: "AddSpecialist",
  components: {
    HeaderPage
  },
  data: () => {
    return {
      name: "",
      email: "",
      budget: "",
      animals: [
        ""
      ]
    };
  },
  computed: {
    ...mapGetters("specialist", ["getMessage"])
  },
  methods: {
    add() {
      this.$store.dispatch(`specialist/${ADD_SPECIALIST}`, this.$data).then(
        () => {
          this.$alert(this.getMessage, "Especialista adicionado!", "success");
          router.push({ name: "listSpecialists" });
        },
        err => {
          err
          this.$alert("", "Especialista adicionado!", "success");
          router.push({ name: "listSpecialists" });
        }
      );
    }
  }
};
</script>
