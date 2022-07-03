<template>
  <div id="app">
    <main class="main-background">
      <h2 class="subheadline">Create new menu</h2>
      <!-- Elements for creating new menu content -->

      <form class="form">
        <!-- Descriptive text above to know which selection to make -->
        <label for="description-input-field" class="type-description"
          >Time of day</label
        ><br />

        <!-- Dropdown list: consistency in category names & avoid different names for subdivision -->
        <select
          name="based-time-of-day"
          class="based-time-of-day"
          placeholder="Please select"
          v-model="filterTimeOfDay"
        >
          <option value="breakfast">Breakfast</option>
          <option value="appetiser">Appetiser</option>
          <option value="lunch">Lunch</option>
          <option value="dinner">Dinner</option>
          <option value="dessert">Dessert</option></select
        ><br />

        <!-- Input fields:  -->
        <div class="form__inputs">
          <div class="form__left">
            <label for="description-input-field" class="type-description"
              >Menu Name</label
            ><br />
            <input
              class="input-field"
              type="text"
              placeholder="What is the name of the menu?"
              v-model="inputMenuName"
            /><br />

            <label for="description-input-field" class="type-description"
              >Description</label
            ><br />
            <input
              class="input-field"
              type="text"
              placeholder="What best describes the menu?"
              v-model="inputDescriptionMenu"
            /><br />
          </div>

          <div class="form__right">
            <label for="description-input-field" class="type-description"
              >Length of cooking</label
            ><br />
            <input
              id="input"
              class="input-field"
              type="text"
              placeholder="How long does the cooking take?"
              v-model="inputCookingLength"
            /><br />

            <label for="description-input-field" class="type-description"
              >Prise</label
            ><br />
            <input
              id="input"
              class="input-field"
              type="text"
              placeholder="How much does the court cost?"
              v-model="inputMenuPrise"
            /><br />
          </div>
        </div>
        <section class="edit-btn">
          <button
            type="submit"
            id="add-btn"
            class="primary-button"
            @click="newMenuCard('Hello')"
          >
            Add Menu
          </button>
        </section>
        <div class="alert-error" v-if="formError">{{ formError }}</div>
      </form>
    </main>

    <!-- Create fictitious data in order to be able to style the output data in advance -->
    <article id="menu-card">
      <!--<section class="content-card">-->
      <div class="time-of-date">{{ courtData.timeOfDay }}</div>
      <div class="menu-name">{{ courtData.menuName }}</div>
      <div class="description-menu">{{ courtData.descriptionMenu }}</div>
      <div class="cooking-length">{{ courtData.cookingLength }}</div>
      <div class="menu-prise">{{ courtData.menuPrise }}</div>

      <!-- Visually highlight the edit and deactivate button to avoid the extra work of deleting. -->
      <!-- Buttons are only displayed when content menu maps are output -->
      <!--<section class="edit-btn">
        <button class="primary-button">Edit</button>
        <button class="secondary-button" id="toggle-btn-deactivate">
          Deactivate
        </button>
        <button class="incognito-button">Delete</button>
      </section>
      </section>-->
    </article>
  </div>
</template>

<!--JavaScript Part -->
<script>
export default {
  // Add the food to the menu – Create a content card

  data() {
    return {
      filterTimeOfDay: "",
      inputMenuName: "",
      inputDescriptionMenu: "",
      inputCookingLength: "",
      inputMenuPrise: "",
      fromError: "",

      courtData: [],
      fetchData: [],
    };
  },
  methods: {
    loadCourtCard() {
      fetch("http://localhost:9000")
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          this.fetchData = data;
        });
    },
    addCourtData() {
      let errors = false;

      if (this.filterTimeOfDay === "") errors = true;
      if (this.inputMenuName === "") errors = true;
      if (this.inputDescriptionMenu === "") errors = true;
      if (this.inputCookingLength === "") errors = true;
      if (this.inputMenuPrise === "") errors = true;

      if (errors) {
        this.fromError = "Please correct the mistakes!";
        return false;
      } else {
        fetch("http://localhost:9000", {
          methode: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            id: "",
            description: {
              timeOfDay: this.filterTimeOfDay,
              menuName: this.inputMenuName,
              menuDescription: this.inputDescriptionMenu,
              cookingLength: this.inputCookingLength,
              menuPrise: this.inputMenuPrise,
            },
          })
            .then((response) => response.json())
            .then((newMenuCard) => {
              this.fetchData.push(newMenuCard);
            }),
        });
      }
    },

    createdNewMenuCard() {
      this.addCourtData();

      // Create three buttons when the new menu card is created (innerHTML)

      if (this.createdNewMenuCard === true) {
        const createThreeButtons = document.createElement("article");
        const createEditButtonInMenuCard = document.querySelector("#menu-card");
        createThreeButtons.classList.add(".edit-btn");

        createThreeButtons.innerHTML = `

      <secticon class="content-card">
        <div class="time-of-date">{{ courtData.timeOfDay }}</div>
        <div class="menu-name">{{ courtData.menuName }}</div>
        <div class="description-menu">{{ courtData.descriptionMenu }}</div>
        <div class="cooking-length">{{ courtData.cookingLength }}</div>
        <div class="menu-prise">{{ courtData.menuPrise }}</div>
     </section>

      <section class="edit-btn">
        <button class="primary-button">Edit</button>
        <button class="secondary-button" id="toggle-btn-deactivate"> Deactivate </button>
        <button class="incognito-button">Delete</button>
    </section>
        `;
        createEditButtonInMenuCard.appendChild(createThreeButtons);
      }
    },
  },

  // Edit Menu (Update Menu) = "PUT"

  // Deactivated menus become grey

  // Button Toggle from Disable to Enable

  // Delete Menu "DELETE" with Button in the Menu Card

  // Create fictitious data in order to be able to style the output data in advance.
  // data() {
  //   return {
  //     courtData: {
  //       timeOfDay: "Breakfast",
  //       menuName: "Golden Toast",
  //       descriptionMenu:
  //         "dazu Butter, hausgemachte Marmelade nach Saison & Schokoladenaufstrich",
  //       cookingLength: "Zubereitung: 20 Minuten",
  //       menuPrise: "12 EUR",
  //     },
  //   };
  // },

  name: "App",
  mounted() {},
};
</script>

<!-- CSS Part -->
