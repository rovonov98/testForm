<template>
  <div id="app" class="app">
    <Form />
  </div>
</template>

<script>
import Form from './components/Form';
export default {
  components: {
    Form
  }
}
</script>

<style lang="scss">
  body {
    background: #E8E8E8;
  }
  * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
  .app {
    display: flex;
    align-items: center;
    justify-content: center;
  }
   @media(max-width: 576px) {
    :root {
      font-size: 10px;
    }
  }
  @media(min-width: 576px) {
    :root {
      font-size: 12px;
    }
  }
  @media(min-width: 768px) {
    :root {
      font-size: 14px;
      .form-group {
        max-width: 75%;
      }
    }
  }
  @media(min-width: 992px) {
    :root {
      font-size: 16px;
      .form-group {
      max-width: 60%;
      }
    }
  }
  @media(min-width: 1200x) {
    :root {
      font-size: 18px;
    }
  }
</style>
