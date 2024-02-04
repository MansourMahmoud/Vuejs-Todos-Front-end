<template>
  <footer>
    <div class="container">
      <p>This website was developed by <span>Mansour Mahmoud</span>.</p>
      <p>
        For inquiries, please contact me via email at
        <span> mansourmahmoud77a@gmail.com </span> or by phone at
        <span>+201158924239</span>.
      </p>
    </div>
  </footer>
</template>

<script setup></script>

<style lang="scss" scoped>
footer {
  background-color: #f1f1f1;
  div {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    padding: 40px 16px;
  }
  span {
    color: green;
    font-weight: 600;
  }
}
</style>
