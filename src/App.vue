<template>
  <!-- <button type="button" @click="flag = !flag">Toggle</button> -->

  <button type="button" @click="AddItem">Add Item</button>
  <!-- <Transition name="fade" mode="out-in">
    <h2 v-if="flag" key="main">Hello World!</h2>
    <h2 v-else key="secondary">another Hello!</h2>
  </Transition> -->

  <!-- <transition name="zoom" type="animation" appear>
    <h2 v-if="flag">hello</h2>
  </transition> -->

  <!-- <transition
    @before-enter="BeforeEnter"
    @enter="Enter"
    @after-enter="AfterEnter"
    @before-leave="BeforeLeave"
    @leave="Leave"
    @after-leave="AfterLeave"
    :css="true"
    name="fade"
  >
    <h2 v-if="flag">Hey</h2>
  </transition> -->

  <ul>
    <transition-group name="fade">
      <li
        v-for="(number, index) in numbers"
        :key="number"
        @click="removeItem(index)"
      >
        {{ number }}
      </li>
    </transition-group>
  </ul>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      flag: false,
      numbers: [1, 2, 3, 4, 5],
    };
  },
  methods: {
    AddItem() {
      const number = Math.floor(Math.random() * 100 + 1);
      const index = Math.floor(Math.random() * this.numbers.length);
      this.numbers.splice(index, 0, number);
    },
    removeItem(index) {
      this.numbers.splice(index, 1);
    },
    BeforeEnter(element) {
      console.log("before-enter ", element);
    },

    Enter(element, done) {
      console.log("enter", element);

      const animation = element.animate([{}, { transform: "scale3d(0,0,0)" }], {
        duration: 1000,
      });

      animation.onfinish = () => {
        done();
      };
    },

    AfterEnter(element) {
      console.log("after-enter", element);
    },

    BeforeLeave(element) {
      console.log("before-leave", element);
    },

    Leave(element, done) {
      console.log("leave", element);

      const animation = element.animate([{ transform: "scale3d(0,0,0)" }, {}], {
        duration: 1000,
      });

      animation.onfinish = () => {
        done();
      };
    },

    AfterLeave(element) {
      console.log("after-leave", element);
    },
  },
};
</script>

<style>
li {
  font-size: 22px;
  cursor: pointer;
}

h2 {
  width: 400px;
  padding: 20px;
  margin: 20px;
}

.fade-enter-from {
  opacity: 0;
}

.fade-enter-active {
  transition: all 1s linear;
}

.fade-enter-to {
  transition: all 1s linear;
  color: chartreuse;
}

.fade-leave-form {
  transition: all 1s linear;
  background-color: aquamarine;
}

.fade-leave-active {
  transition: all 2s;
  position: absolute;
}

.fade-leave-to {
  transition: all 1s linear;
  opacity: 1;
  color: red;
}

.fade-move {
  transition: all 1s linear;
}

.zoom-enter-active {
  animation: zoom-in 1s linear forwards;
  transition: all 2s linear;
}

.zoom-leave-active {
  animation: zoom-out 1s linear forwards;
  transition: all 2s linear;
}

@keyframes zoom-in {
  from {
    transform: scale(0, 0);
  }
  to {
    transform: scale(1, 1);
  }
}

@keyframes zoom-out {
  from {
    transform: scale(1, 1);
  }
  to {
    transform: scale(0, 0);
  }
}
</style>
