<script setup lang="ts">
import HelloWorld from "@/components/HelloWorld.vue";
import { onMounted, reactive, ref } from "vue";
import { RouterLink, RouterView } from "vue-router";
import CustomButton from "./components/CustomButton.vue";
import MultipleRootNode from "./components/MultipleRootNode.vue";

const name = ref("Hoàng Minh");
const rawHTML = ref("<h1>Hoàng Minh</h1>");
const state = reactive({ count: 1 });

const model = ref("test v-model");

function handleChange(e: Event) {
  const target = e.target as HTMLInputElement;

  name.value = target.value;

  rawHTML.value = `<h1>${target.value}</h1>`;
}

const showElement = ref(true);

const showElement2 = ref(false);

const showMultipleRootNode = ref(true);

const testVFor: Array<number> = [1, 2, 3];

const testClickedBtn = () => {
  showElement.value = !showElement.value;
  showElement2.value = !showElement2.value;
  showMultipleRootNode.value = !showMultipleRootNode.value;
};

const myObject = reactive({
  title: "How to do lists in Vue",
  author: "Jane Doe",
  publishedAt: "2016-04-10",
});

const countInline = ref(0);

const handleSubmitForm = () => {
  console.log("Hoàng Min");
};

const handleKeyEventHandler = () => {
  countInline.value++;
};

const data = ref([
  { id: 1, title: "Hoàng" },
  { id: 2, title: "Minh" },

  { id: 3, title: "A" },
]);

const vModelValueEx = ref<number>(1);

const multiLine = ref<string>("");

const multiCheckbox = ref<Array<string>>([]);

const inputValue = ref<any>("no");

const pick = ref<1 | 2>(1);

onMounted(() => {
  console.log("Mounted");
});
</script>

<template>
  <h1>Name:</h1>
  <div>{{ name }}</div>
  <input @input="handleChange" :value="name" />
  <div v-html="rawHTML"></div>
  <div>State is : {{ state.count }}</div>

  <h1>Model:</h1>
  <div>{{ model }}</div>
  <input v-model.lazy="model" />

  <!-- Test conditional and loop directive -->
  <div v-if="showElement">This Element Is Showed</div>
  <div v-else>This Element Is UnShowed</div>

  <div v-if="showElement2">This Is Second Showed Element</div>
  <div v-else>This Second Element Is Not Showed</div>

  <div v-show="showElement">Test V-Show Element</div>

  <ul>
    <li :key="number" v-for="number in testVFor">Test - {{ number }}</li>
  </ul>

  <ul>
    <li :key="key" v-for="(value, key) in myObject">
      Test Object Value {{ value }}
    </li>
  </ul>

  <div>Count Clicked Inline: {{ countInline }}</div>

  <button v-on:click="countInline++">Test On CLick Inline</button>

  <!-- Test modifier event -->
  <form @submit.prevent="handleSubmitForm">
    <button>Submit Form</button>
    <button type="button" @click.ctrl="handleKeyEventHandler">
      Ctrl Clicked
    </button>
  </form>

  <CustomButton @click="testClickedBtn" class="test-fall-through" />

  <MultipleRootNode v-if="showMultipleRootNode" class="abc" />

  <!-- Test V model select -->
  <select v-model="vModelValueEx">
    <option v-for="item in data" :key="item.id" :value="item.id">
      {{ item.title }}
    </option>
  </select>

  <div>V-Model Value {{ vModelValueEx }}</div>

  <!-- Test multitext -->
  <span>Multiline message</span>
  <p style="white-space: pre-line">{{ multiLine }}</p>
  <textarea v-model.lazy="multiLine" cols="3" rows="10"></textarea>

  <br />
  <!-- Test multiCheckbox -->
  <div>Choosen Checkbox Is: {{ multiCheckbox }}</div>
  <input type="checkbox" id="jack" value="jack" v-model="multiCheckbox" />
  <label for="jack">Jack</label>

  <input type="checkbox" id="john" value="john" v-model="multiCheckbox" />
  <label for="john">John</label>

  <input type="checkbox" id="jenny" value="jenny" v-model="multiCheckbox" />
  <label for="jenny">Jenny</label>

  <br />
  <!-- Test true false value -->
  <div>Current Input Value: {{ inputValue }}</div>
  <input
    type="checkbox"
    v-model="inputValue"
    true-value="yes"
    false-value="no"
  />

  <br />
  <!-- Radio Input -->
  <div>Radio Input Value: {{ pick }}</div>
  <input type="radio" v-model="pick" :value="1" />
  <input type="radio" v-model="pick" :value="2" />
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="@/assets/logo.svg"
      width="125"
      height="125"
    />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style>
@import "@/assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
