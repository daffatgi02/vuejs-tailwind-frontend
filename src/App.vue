<script>
export default {
  data() {
    return {
      newData: {
        waktu: "",
        suhu: []
      }
    }
  },
  methods: {
    methods: {
      async getData() {
        try {
          const response = await axios.get("http://localhost:3000/sensor/suhu");
          this.listsuhu = response.data;
        } catch (error) {
          console.error(error);
          alert("Terjadi kesalahan saat mengambil data.");
        }
      },
    },
    async createData() {
      try {
        await axios.post("http://localhost:3000/sensor/suhu", this.newData);
        this.newData = { waktu: "", suhu: "" };
        this.$emit("data-created");
        alert("Data berhasil ditambahkan!");
      } catch (error) {
        console.error(error);
        alert("Terjadi kesalahan saat menambahkan data.");
      }
    },

  },
};
</script>

<template>
  <table class="table-auto text-center mx-auto">
    <thead class="bg-gray-200">
      <tr>
        <th class="px-4 py-2">Waktu</th>
        <th class="px-4 py-2">Suhu</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in suhu" :key="item.waktu" class="text-left">
        <td class="border px-4 py-2">{{ item.waktu }}</td>
        <td class="border px-4 py-2">{{ item.suhu }}</td>
      </tr>
    </tbody>
  </table>

  <div class="text-center">
    <button class="bg-red-500 text-white rounded-3xl p-2" @click="getData()">Ambil Data</button>
  </div>

  <form @submit.prevent="createData">
    <label for="waktu">Waktu:</label>
    <input type="text" v-model="newData.waktu" id="waktu" name="waktu">

    <label for="suhu">Suhu:</label>
    <input type="text" v-model="newData.suhu" id="suhu" name="suhu">

    <button type="submit" class="bg-blue-500 text-white rounded-3xl p-2">Create</button>
  </form>
</template>
