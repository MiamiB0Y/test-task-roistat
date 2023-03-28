<style>
.content {
  display: grid;
  padding: 2rem;
  gap: 2rem;
}

.form-button {
  color:black;
  width: 9rem;
  height: 3rem;
  border-radius: 1.5rem;
  margin: auto;
  font-size: 1.2rem;
  font-weight: bold;
  border: 0.05rem solid var(--box-border);
  background-color: rgb(115, 119, 124);
  color: var(--prime-light-color);
  transition: 0.28s;
  cursor: pointer;
}

.form-button:hover {
  background-color: rgb(37, 37, 37);
  scale: 1.05;
}
</style>

<template>
  <div class="content">
    <button class="form-button" v-on:click="showForm = !showForm">Добавить</button>

    <AppTable
      :tableHeader="tableHeader"
      :tableBody="tableBody"
      :hiddenParameters="hiddenParameters"
    />

    <AppForm
      v-if="showForm"
      :tableHeader="tableHeader"
      :tableBody="tableBody"
      @submit="tableBody.push($event)"
      @hideForm="showForm = !showForm"
    />
  </div>
</template>

<script>
import AppTable from './AppTable.vue'
import AppForm from './AppForm.vue'

export default {
  name: 'AppLayout',
  components: {
    AppTable,
    AppForm
  },
  data () {
    return {
      showForm: false,
      tableHeader: [
        {
          id: 'name',
          title: 'Имя',
          sortable: true,
          sortType: { type: String },
          inputType: 'text'
        },
        {
          id: 'phone',
          title: 'Телефон',
          sortable: false,
          sortType: { type: String },
          inputType: 'tel'
        }
      ],
      tableBody: [
        {
          name: 'Евгений',
          phone: '+78005553533',
          parentId: "",
          id: 1
        },
        {
          name: 'Алина',
          phone: '+78005553534',
          parentId: 1,
          id: 2
        },
        {
          name: 'Марк',
          phone: '+78005553535',
          parentId: "",
          id: 3
        },
        {
          name: 'Дмитрий',
          phone: '+78005553536',
          parentId: 2,
          id: 4
        }
      ],
      hiddenParameters: ['parentId', 'id']
    }
  },
  mounted () {
    const arrayString = localStorage.getItem('array')
    if (arrayString) {
      const array = JSON.parse(arrayString)
      this.tableBody = array
    }
    
    
    
}
}

</script>