<template>
  <div class="flex flex-col">
    {{ inputan }}
    <input type="text" class="border rounded-full w-40" v-model="inputan" />

    <PersegiBaru @onClick="fetchData" />
    <PersegiBaru :latarBelakang="'bg-yellow-500'" @onClick="klikKedua" />

    <div class="w-80 h-72">
      <Bar v-if="cars" :data="cars" :options="options" />
      <Line v-if="cars" :data="cars" :options="options" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement
} from 'chart.js'
import { Bar } from 'vue-chartjs'
import { Line } from 'vue-chartjs'

ChartJS.register(
  CategoryScale,
  LinearScale,
  BarElement,
  Title,
  Tooltip,
  Legend,
  PointElement,
  LineElement
)

import PersegiBaru from '@/components/PersegiBaru.vue'

const inputan = ref('')
const cars = ref(null)

const klikPertama = () => {
  alert('klik pertama')
}

const klikKedua = () => {
  alert('klik kedua')
}

const fetchData = async () => {
  const { data } = await axios.get('https://mocki.io/v1/602f6ba0-2e88-4a43-bbe1-a5ded1a4f7c8')

  const labels = data.map((e) => e.merkMobil)
  const penjualan = data.map((e) => {
    return e.penjualan
  })
  const warnaArray = [
    '#FF0000', // Merah
    '#00FF00', // Hijau
    '#0000FF', // Biru
    '#FFFF00', // Kuning
    '#FF00FF', // Magenta
    '#00FFFF', // Cyan
    '#000000', // Hitam
    '#FFFFFF', // Putih
    '#808080', // Abu-abu
    '#FFA500' // Oranye
  ]

  cars.value = {
    labels: labels,
    datasets: [
      {
        data: penjualan,
        label: '2017',
        backgroundColor: warnaArray
      }
    ]
  }
}

const options = ref({
  responsive: true,
  indexAxis: 'y',
  scales: {
    y: {
      grid: {
        display: false
      }
    },
    x: {
      grid: {
        display: false
      }
    }
  },
  plugin: {
    legend: {
      display: false
    }
  }
})

onMounted(() => {
  fetchData()
})
</script>
