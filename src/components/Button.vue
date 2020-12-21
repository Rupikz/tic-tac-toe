<template>
  <button class="restart">Click</button>
</template>

<script>
export default {
  name: 'Button',
};
</script>

<style>
.restart {
  width: 100%;
  background-color: #e74c3c;
  border-radius: 0 0 15px 15px ;
  font-size: 1.4em;
  padding: 15px 0;
  border: 0;
  color: #e0e0e0;
  transition: .3s ;
}

.restart:hover {
  background-color: #c95143;
  color: #ffffff
}
</style>
