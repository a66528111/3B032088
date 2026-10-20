<script setup>
import { ref, computed } from 'vue'

// 使用 ref 儲存身高與體重
const height = ref('')
const weight = ref('')

// 使用 computed 自動計算 BMI
const bmi = computed(() => {
  if (height.value > 0 && weight.value > 0) {
    const heightMeter = height.value / 100
    return (weight.value / (heightMeter * heightMeter)).toFixed(1)
  }

  return ''
})

// 使用 computed 判斷 BMI 結果
const result = computed(() => {
  if (bmi.value === '') {
    return '請輸入身高與體重'
  } else if (bmi.value < 18.5) {
    return '體重過輕'
  } else if (bmi.value < 24) {
    return '正常範圍'
  } else if (bmi.value < 27) {
    return '過重'
  } else {
    return '肥胖'
  }
})
</script>

<template>
  <div class="container">
    <div class="card">

      <h1>BMI 計算機</h1>
      <p class="subtitle">輸入身高與體重，自動計算 BMI</p>

      <div class="input-group">
        <label>身高（cm）</label>
        <input
          v-model.number="height"
          type="number"
          placeholder="例如：173"
        >
      </div>

      <div class="input-group">
        <label>體重（kg）</label>
        <input
          v-model.number="weight"
          type="number"
          placeholder="例如：60"
        >
      </div>

      <div class="result">
        <p>你的 BMI</p>
        <h2>{{ bmi || '--' }}</h2>
        <h3>{{ result }}</h3>
      </div>

    </div>
  </div>
</template>

<style scoped>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f2f5f9;
  font-family: Arial, sans-serif;
}

.card {
  width: 380px;
  background-color: white;
  padding: 40px;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
  margin: 0 0 8px;
  font-size: 36px;
}

.subtitle {
  text-align: center;
  color: #777;
  margin-bottom: 30px;
}

.input-group {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  font-weight: bold;
}

input {
  width: 100%;
  box-sizing: border-box;
  padding: 12px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 8px;
}

input:focus {
  outline: none;
  border-color: #4f75ff;
}

.result {
  margin-top: 30px;
  padding: 25px;
  text-align: center;
  background-color: #f1f4ff;
  border-radius: 12px;
}

.result p {
  margin: 0;
  color: #777;
}

.result h2 {
  margin: 10px 0;
  font-size: 45px;
  color: #4f75ff;
}

.result h3 {
  margin: 0;
}
</style>