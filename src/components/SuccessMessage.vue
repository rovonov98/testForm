<template>
  <div class="success-message">
      <p class="new-client">Новый клиент успешно создан.</p>
      <div class="buttons">
          <button class="cancel-button" @click="back">Назад</button>
          <button class="next-button" @click="reload">Продолжить</button>
      </div>
  </div>
</template>

<script>
export default {
    methods: {
        reload() {
            window.location.reload()
        },
        back() {
            this.$emit('back', ' ')
        }
    }
}
</script>

<style scoped lang="scss">
    .success-message {
        text-align: center;
        position: fixed;
        z-index: 3;
        flex-direction: column;
        background: #FFFFFF;
        border: 1px solid #0061d9;
        border-radius: 8px;
        top: 45%;
        padding: 1em;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .new-client {
        font-size: 2rem;
    }
    .next-button {
        padding: .8rem;
        background: #0061d9;
        border: none;
        color: #FFFFFF;
        font-size: 1.5rem;
        border-radius: 8px;
        margin: 1rem;
        cursor: pointer;
    }
    .cancel-button {
        padding: .8rem;
        background: #FFFFFF;
        border: 2px solid #0061d9;
        color: #0061d9;
        font-size: 1.5rem;
        border-radius: 8px;
        margin: 1rem;
        cursor: pointer;
    }
</style>