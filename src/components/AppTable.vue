<style>
.table {
  border: 0.05rem solid var(--box-border);
  box-shadow: 1px 1px 30px var(--box-shadow);
  width: max-content;
  margin: auto;
  display: grid;
  grid-template-columns: 1fr 1fr;
  width: max-content;
}

.table-body-cell,
.table-header-cell {
  width: 100%;
  min-width: 12rem;
  border: 0.05rem solid var(--box-border);
  height: 3rem;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.table-header-cell {
  width: 100%;
  font-weight: bold;
  background-color: rgb(187, 187, 187);
  color: black;
  border-top: none;
}

.table-header-cell:first-child {
  border-left: none;
}

.table-header-cell:last-child {
  border-right: none;
}

.table-body-cell-colored {
    width: 18rem;
  display: flex;
  justify-content: space-between;
  padding-right: 1rem;
  gap: 2rem;
}
</style>

<template>
  <div class="table">
    <div
      class="table-header-cell"
      v-for="header in tableHeader"
      :key="header.id"
      @click="sortByName(header.id)"
    >

      {{ header.title }}
    </div>

    <template v-for="(row) in tableBody">       
      <div v-for="(cell, key, index) in row" v-bind:itemID="'cell-' + row.id + '-' + key" v-bind:class="!index ? 'table-body-cell table-body-cell-colored' : 'table-body-cell'" :key="cell.id" v-if="!hiddenParameters.includes(key)">
	    <div>
		  {{ key === 'name' ? (tableBody.filter(user => user.id === row.parentId)[0] ? tableBody.filter(user => user.id === row.parentId)[0].name + '(начальник) - ' : '') + cell : cell }}
	    </div>
</div>
    </template>
  </div>
</template>

<script>
export default {
  name: 'AppTable',
  props: {
    tableHeader: {
      type: Array,
      isAscSort: true
    },
    tableBody: {
      type: Array
    },
    hiddenParameters: {
      type: Array
    }
  },

  data () {
    return {
      isAscSort: true
    }
  },
  
  methods: {
    sortByName(id) {
      if (id === "name") {
        this.tableBody.sort((a, b) => {
          return this.isAscSort ? a.name.localeCompare(b.name) : b.name.localeCompare(a.name)
        })
      } else {
        const comparePhone = (a, b) => {
          let phoneA = a.phone.replace(/\D/g, '')
          let phoneB = b.phone.replace(/\D/g, '')
          return this.isAscSort ? phoneA.localeCompare(phoneB) : phoneB.localeCompare(phoneA)
        }
        this.tableBody.sort(comparePhone)
      }
      this.isAscSort = !this.isAscSort
    }
  }
}
</script>