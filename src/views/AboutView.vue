<template>
  <div class="container">
    <h1>Vue Todos</h1>
    <p>
      Vue Todos is a CRUD Todo tracking application created for learning Vue 3
      by Mansour Mahmoud. The application was last updated on February 5, 2024.
    </p>
    <br />
    <p>
      Track your daily tasks using this todo tracker with the ability to save,
      complete, edit, and delete todos.
    </p>
    <br />
    <p>
      Feel free to enhance this application by adding functionalities such as
      the ability to drag and reorder todos, animate the creation/deletion of
      todos, or even develop it into a full-stack application with the
      capability to have different lists for tracking todos on different days!
    </p>
  </div>
</template>

<style lang="scss" scoped>
div {
  display: flex;
  align-items: start;
  flex-direction: column;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
  p {
    line-height: 25px;
  }
}
</style>
