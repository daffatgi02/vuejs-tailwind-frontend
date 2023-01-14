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
  <table class="p-10">
    <tr>
      <th>Waktu</th>
      <th>Suhu</th>
    </tr>
    <tr v-for="item in suhu">
      <td>{{ item.waktu }}</td>
      <td>{{ item.suhu }}</td>
    </tr>
  </table>

  <div>
    <button class="rounded-3xl p-2 bg-red-500 text-white" @click="getData()">Ambil Data</button>
  </div>
</template>
