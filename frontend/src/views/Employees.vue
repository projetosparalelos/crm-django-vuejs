<template>
  <div>
    <router-link :to="{name: 'employeeCreate'}">
      <button class="btn">Adicionar</button>
    </router-link>
    Employees
    
    <!-- <b-table striped hover :items="items"></b-table> -->
    <table class="table">
      <thead>
        <tr>
          <th>#</th>
          <th>Slug</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in items" :key="item.pk">
          <td>{{ item.pk }}</td>
          <td>
            <router-link :to="{name: 'employeeDetail', params: {id: item.pk}}">
              {{ item.slug }}
            </router-link>
          </td>
          <td>
            <b-btn variant="link" v-b-modal.modal1 @click="deletingItem=item">
              <i class="fa fa-close" style="color:red"></i>
            </b-btn>
          </td>
        </tr>
      </tbody>
    </table>

    <b-modal id="modal1" title="Bootstrap-Vue" @ok="deleteItem">
      <p class="my-4">Deseja mesmo apagar {{ deletingItem.slug }}?</p>
    </b-modal>

  </div>
</template>

<script>

export default {
  data () {
    return {
      deletingItem: {}
    }
  },
  methods: {
    deleteItem() {
      this.$store.dispatch('deleteEmployee', this.deletingItem)
    }
  },
  computed: {
    items() {
      return this.$store.state.employees.employees
    }
  }
}
</script>