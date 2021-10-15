<template>
  <div class="wrapper-popup" :class="{open: isOpenPopup}">
    <div class="rule">
      <h2>lorem ipsum</h2>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Facilis at mollitia, repellendus voluptas odio, ad veritatis fugiat recusandae rerum nemo, consequuntur ratione ullam reprehenderit debitis non perspiciatis. Officiis, voluptatem voluptatibus.</p>
      <button @click="$emit('confirmRule')">Ok</button>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      isOpenPopup: {
        type: Boolean,
        default: false
      }
    }
  }
</script>

<style>
  .wrapper-popup {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: rgba(0, 0, 0, 0.4);
    opacity: 0;
    visibility: hidden;
    transition: all .3s ease;
  }

  .wrapper-popup.open {
    opacity: 1;
    visibility: visible;
  }

  .rule {
    position: absolute;
    width: 350px;
    padding: 20px;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(1.2);
    background-color: #FFF;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    transition: all .3s ease;
  }

  .open .rule {
    transform: translate(-50%, -50%) scale(1);
  }

  .rule p {
    margin-top: 20px;
  }

  .rule button {
    border: 2px solid #333;
    background-color: #FFF;
    padding: 10px 15px;
    margin-top: 20px;
    cursor: pointer;
  }
</style>
