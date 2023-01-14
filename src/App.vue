<script>
export default{
  data(){
    return{
      suhu: []
    }
  },
  methods:{
    async getData() {
      try {
        const response = await fetch("http://localhost:3000/sensor/suhu");
        const data = await response.json();
        this.suhu = data;
      } catch (error) {
        console.error(error);
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
</template>
