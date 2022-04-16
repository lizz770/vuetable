<template>
  <div style="width:auto">
    <div>
      <input
        type="text"
        class="border-2 mb-5 rounded h-10 p-2"
        placeholder="Поиск..."
        @input="onSearch"
      />
    </div>
    <table>
      <thead>
        <tr>
          <th
            v-for="(column, index) in columns"
            v-bind:key="index"
            class="border-2 p-2 text-left"
            v-on:click="sortRecords(index)"
          >
            {{column}}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(row, index) in rows"
          v-bind:key="index"
        >
          <td
            v-for="(rowItem, itemIndex) in row"
            v-bind:key="itemIndex"
            class="border-2 p-2"
          >
            {{rowItem}}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
const performSearch = (rows, term) => {
  const results = rows.filter(
    row => row.join(" ").toLowerCase().includes(term.toLowerCase())
  )
  return results;
}
export default {
  name: 'Components__table',
  data () {
    return {
      term: '',
      rawRows: [
        [
          "1", "0253", "женский", "Дизайн","нет"
        ],
        [
          "2", "0368", "женский", "Реклама и СсО","Upper-Intermediate (В2)"
        ],
        [
          "3", "0221", "мужской", "Философия","Upper-Intermediate (В2)"
        ],
        [
          "4", "0316", "мужской", "Физическая культура","нет"
        ],
        [
          "5", "0339", "женский", "Социология","нет",
        ],
        [
          "6", "0258", "женский", "Дизайн","нет"
        ],
        [
          "7", "0268", "женский", "Дизайн","нет"
        ],
        [
          "8", "0159", "женский", "Журналистика","нет"
        ],
        [
          "9", "0183", "женский", "Культурология","Upper-Intermediate (В2)"
        ],
        [
          "10", "0396", "женский", "История","Pre-Intermediate (А2)"
        ],
        [
          "11", "0191", "мужской", "История","Advanced (С1)"
        ],
      ],
      rows: [],
      columns: [
        '#',
        'Шифр',
        'Пол',
        'Направление подготовки',
        'Уровень владения английским языком'
      ],
      sortIndex: null,
      sortDirection: null
    }
  },
  methods: {
    sortRecords (index) {
      if (this.sortIndex === index) {
        switch (this.sortDirection) {
          case null:
            this.sortDirection = 'asc';
            break;
          case 'asc':
            this.sortDirection = 'desc';
            break;
          case 'desc':
            this.sortDirection = null;
            break;
        }
      } else {
        this.sortDirection = 'asc'
      }
      this.sortIndex = index;
      if (!this.sortDirection) {
        this.rows = performSearch(this.rawRows, this.term);
        return;
      }
      this.rows = this.rows.sort(
        (rowA, rowB) => {
          if (this.sortDirection === 'desc') {
            return rowB[index].localeCompare(rowA[index]);
          }
          return rowA[index].localeCompare(rowB[index]);
        }
      )
    },
    onSearch (e) {
      this.term = e.target.value;
      this.rows = performSearch(this.rawRows, this.term);
    }
  },
  mounted () {
    this.rows = [...this.rawRows];
  }
}
</script>