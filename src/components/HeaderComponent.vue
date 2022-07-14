<template>
  <header>
    <div class="header-container">
      <img src="https://www.roadtvitalia.it/wp-content/uploads/2018/10/Netflix-1.jpg" alt="">
      <div class="input">
        <input v-model="getUserInput" type="text" placeholder="Cerca un film o serie TV" @keyup.enter="$emit('getInputApi', getUserInput)">
        <button  @click="$emit('getInputApi', getUserInput)">Cerca</button>
      </div> 
    </div>
  </header>
</template>

<script>
export default {
  name: 'HeaderComponent',
  data() {
    return {
      getUserInput: '',
    }
  },
}
</script>

<style lang="scss" scoped>
header {
  height: 70px;
  background-color: #0c0c0c;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1;
  .header-container {
    height: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    img {
      height: 100%;
    }
    .input {
      height: 50%;
      margin-right: 20px;
      input {
        height: 100%;
        margin-right: 20px;
        background-color: black;
        border: 2px solid red;
        border-radius: 20px;
        color: white;
        padding: 0 10px;
      }
      button {
        width: 100px;
        height: 100%;
        background-color: black;
        color: white;
        font-size: 18px;
        border: 2px solid red;
        border-radius: 20px;
      }
    }
  }
}
</style>