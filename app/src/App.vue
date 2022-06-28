<template>
  <div id="app">
    <header>
      <h2 class="subheadline">Create menu</h2>
    </header>
    <main class="main-background">
      <!-- Elements for creating new menu content -->
      <article class="create-menu">
        <!-- Descriptive text above to know which selection to make -->
        <label for="description-input-field" class="type-description"
          >Based on time of day</label
        ><br />

        <!-- Dropdown list = consistency in category names & avoid different names for subdivision -->
        <select name="based-time-of-day">
          <option value="please-select">Please select</option>
          <option value="breakfast">Breakfast</option>
          <option value="appetiser">Appetiser</option>
          <option value="lunch">Lunch</option>
          <option value="dinner">Dinner</option>
          <option value="dessert">Dessert</option></select
        ><br />

        <label for="description-input-field" class="type-description"
          >Menu Name</label
        ><br />
        <input class="input-field" type="text" placeholder="Court Name" /><br />

        <label for="description-input-field" class="type-description"
          >Description</label
        ><br />
        <input
          class="input-field"
          type="text"
          placeholder="Describes the court"
        /><br />

        <label for="description-input-field" class="type-description"
          >Length of cooking</label
        ><br />
        <input
          class="input-field"
          type="text"
          placeholder="Cooking Length"
        /><br />

        <label for="description-input-field" class="type-description"
          >Prise</label
        ><br />
        <input class="input-field" type="text" placeholder="Prise" /><br />
        <button class="primary-button">Add Menu</button>
      </article>
    </main>

    <section class="content-card">
      <div class="time-of-date">{{ courtData.timeOfDay }}</div>
      <div class="menu-name">{{ courtData.menuName }}</div>
      <div class="description-menu">{{ courtData.descriptionMenu }}</div>
      <div class="cooking-length">{{ courtData.cookingLength }}</div>
      <div class="menu-prise">{{ courtData.menuPrise }}</div>

      <button class="primary-button">Edit</button>
      <button class="primary-variant-button">Deactivate</button>
      <button class="secondary-button">Delete</button>
    </section>
  </div>
</template>
<!-- JavaScript Part -->
<!-- Add the food to the menu – Create a content card -->

<!-- Deactivated menus become grey -->

<!-- Button Toggle from Disable to Enable -->

<!-- CSS Part -->
<script>
export default {
  data() {
    return {
      courtData: {
        timeOfDay: "Breakfast",
        menuName: "Rumpsteak mit Schmorzwiebeln",
        descriptionMenu: "dazu Bratkartoffel",
        cookingLength: "45 Minuten",
        menuPrise: "22 EUR",
      },
    };
  },

  name: "App",
  mounted() {},
};
</script>
