<template>
  <div id="app">
    <main class="main__background">
      <h2 class="subheadline">Create new menu</h2>
      <!-- Elements for creating new menu content -->

      <form class="form" @submit.prevent="addCourtData">
        <!-- Classification in categories & times of day of meals 
        - Dropdown for uniform naming of category names and times of day to avoid different names. -->

        <!-- Dropdown list: filterCategory -->
        <div class="form__inputs">
          <div class="form__left">
            <label for="description-input-field" class="type__description"
              >Catergory</label
            ><br />

            <select
              name="based-category-name"
              class="based__dropdown"
              v-model="filterCategory"
              required
            >
              <option value="" disabled selected>Please select</option>
              <option value="good-morning">Good Morning</option>
              <option value="starter">Starter</option>
              <option value="main-course">Main course</option>
              <option value="childrens-menu">Children's menu</option>
              <option value="dessert">Dessert</option>
              <option value="beverage">Beverage</option></select
            ><br />
          </div>

          <!-- Dropdown list: filterTimeOfDay -->
          <div class="form__right">
            <label for="description-input-field" class="type__description"
              >Time of day</label
            ><br />

            <select
              name="based-time-of-day"
              class="based__dropdown"
              v-model="filterTimeOfDay"
              required
            >
              <option value="" disabled selected>Please select</option>
              <option value="breakfast">Breakfast</option>
              <option value="appetiser">Appetiser</option>
              <option value="lunch">Lunch</option>
              <option value="dinner">Dinner</option></select
            ><br />
          </div>
        </div>

        <!-- Input fields -->
        <div class="form__inputs">
          <div class="form__left">
            <label for="description-input-field" class="type__description"
              >Menu Name</label
            ><br />
            <input
              class="input__field"
              type="text"
              placeholder="What is the name of the menu?"
              v-model="inputMenuName"
              required
            /><br />

            <!-- For better usability, it should be defined here that only 
            letters and no special characters or numbers can be used.-->
            <label for="description-input-field" class="type__description"
              >Description</label
            ><br />
            <input
              class="input__field"
              type="text"
              placeholder="What best describes the menu?"
              v-model="inputDescriptionMenu"
              required
            /><br />
          </div>

          <!-- In the input field required preparation time, 
          it could be defined that only numbers can be entered and that the time span is output as minutes via JS.-->
          <div class="form__right">
            <label for="description-input-field" class="type__description"
              >Length of cooking</label
            ><br />
            <input
              id="input"
              class="input__field"
              type="text"
              placeholder="How long does the cooking take?"
              v-model="inputCookingLength"
              required
            /><br />

            <!-- For the input field Price, it could be defined that 
                  only numbers can be entered and that the currency is output via JS.-->
            <label for="description-input-field" class="type__description"
              >Prise</label
            ><br />
            <input
              id="input"
              class="input__field"
              type="text"
              placeholder="How much does the court cost?"
              v-model="inputMenuPrise"
              required
            /><br />
          </div>

          <!-- When the button is triggered, a check is made to see if all the fields have been filled in and if this is the case, 
            a new card with a new menu and all its data inserted in the API is output.-->
        </div>
        <section class="edit__btn">
          <button type="submit" id="add-btn" class="primary__button">
            Add Menu
          </button>
        </section>
      </form>
    </main>

    <div v-if="courtData.length">
      <article
        class="content__card"
        v-for="{
          index,
          categoryName,
          timeOfDay,
          menuName,
          descriptionMenu,
          cookingLength,
          menuPrise,
        } of courtData"
        :key="index"
      >
        <!-- Create fictitious data in order to be able to style the output data in advance -->

        <header>
          <div class="category__name">{{ categoryName }}</div>
          <div class="time__of__date">{{ timeOfDay }}</div>
        </header>
        <main>
          <div class="menu__name">{{ menuName }}</div>
          <div class="description__menu">{{ descriptionMenu }}</div>
          <div class="cooking__length">{{ cookingLength }}</div>
          <div class="menu__prise">{{ menuPrise }}</div>
        </main>

        <!-- Visually highlight the edit and deactivate button to avoid the extra work of deleting. -->
        <!-- Buttons are only displayed when content menu maps are output -->
        <footer class="edit__btn">
          <button class="primary__button">Edit</button>
          <button class="secondary__button" id="toggle-btn-deactivate">
            Deactivate
          </button>
          <button class="incognito__button">Delete</button>
        </footer>
      </article>
    </div>
  </div>
</template>

<!--JavaScript Part -->
<script>
export default {
  // Add the food to the menu – Create a content card

  // data() {
  //   return {
  //     filterCategory, "",
  //     filterTimeOfDay: "",
  //     inputMenuName: "",
  //     inputDescriptionMenu: "",
  //     inputCookingLength: "",
  //     inputMenuPrise: "",
  //     fromError: "",

  //     courtData: [],
  //     fetchData: [],
  //   };
  // },

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
      const menuName = this.inputMenuName;
      const menuDescription = this.inputDescriptionMenu;
      const cookingLength = this.inputCookingLength;
      const menuPrise = this.inputMenuPrise;
      const timeOfDay = this.filterTimeOfDay;
      const categoryName = this.filterCategory;

      this.courtData.push({
        categoryName: categoryName,
        timeOfDay: timeOfDay,
        menuName: menuName,
        descriptionMenu: menuDescription,
        cookingLength: cookingLength,
        menuPrise: menuPrise,
      });

      // Create a new menu with "POST" to save it in the API.
      // As well as outputting the saved information on the map with a menu.

      // fetch("http://localhost:9000/dishes", {
      //   methode: "POST",
      //   headers: { "Content-Type": "application/json" },
      //   body: JSON.stringify({
      //     categoryName: categoryName,
      //     timeOfDay: timeOfDay,
      //     menuName: menuName,
      //     descriptionMenu: menuDescription,
      //     cookingLength: cookingLength,
      //     menuPrise: menuPrise,
      //   }),
      // })
      //   .then((response) => response.json())
      //   .then((newCourt) => this.courtData.push(newCourt));
    },
  },

  //   created() {
  //     this.loadCourtCard();
  //   },

  // Create three buttons
  // Edit Menu (Update Menu) = "PUT"
  // Deactivated menus become grey
  // Button Toggle from Disable to Enable

  // Delete Menu "DELETE" with Button in the Menu Card

  // Create fictitious data in order to be able to style the output data in advance.
  data() {
    return {
      filterCategory: "",
      filterTimeOfDay: "",
      inputMenuName: "",
      inputDescriptionMenu: "",
      inputCookingLength: "",
      inputMenuPrise: "",

      // courtData: [],
      courtData: [
        {
          categoryName: "Good Morning",
          timeOfDay: "Breakfast",
          menuName: "Golden Toast",
          descriptionMenu:
            "dazu Butter, hausgemachte Marmelade nach Saison & Schokoladenaufstrich",
          cookingLength: "Zubereitung: 20 Minuten",
          menuPrise: "8,99 EUR",
        },
        {
          categoryName: "Main course",
          timeOfDay: "Dinner",
          menuName: "Pfeffertöpfchen",
          descriptionMenu:
            "dazu hausgemachte Spätzle in Rahmgeschnetzeltem mit Champignons, Pfefferbeeren und Gurkenstreifen",
          cookingLength: "Zubereitung: 45 Minuten",
          menuPrise: "18,50 EUR",
        },
      ],
    };
  },

  name: "App",
  mounted() {},
};
</script>

<!-- CSS Part -->
