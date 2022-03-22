<template>
  <div>
    <h1>Hello Vue!! {{ subject }}</h1>
    <!-- ↑ [mustache syntax] -->
    <input type="text" v-model="food" />
    <div v-html="alertMessage"></div>
    <div v-html="subscribeHTML"></div>
    <!-- ↑ 확실한 데이터 값을 받아올때 사용함(믿을수있는) -->
    <hr />
    <h1>v-bind use example</h1>
    <img v-bind:src="imageSource" alt="random" />
    <p><a :href="naverUrl">naver 바로가기</a></p>
    <!-- ↑ v-bind, 생략하고 :만 써도된다. -->
    <h2 v-bind:class="{ red: food === 'apple' }">
      원숭이는{{ food }}를 사용한다.
    </h2>
    <h2 v-bind:class="{ red: food === 'apple', 'not-good': food === 'rice' }">
      태용이는{{ food }}를 사용한다.
    </h2>
    <hr />
    <!--동적으로 클래스 연결 / v-bind / 색변경-->
    <h1>v-if // Conditional example</h1>
    <input type="text" size="3" v-model="age" />
    <h3>당신의 나이는 {{ age }} 입니다.</h3>
    <!--형제, 연결요소여야함-->
    <h3 v-if="age >= 20">당신은 어른입니다.</h3>
    <h3 v-else-if="age > 13 && age <= 19">당신은 청소년입니다.</h3>
    <h3 v-else>당신은 어린이입니다.</h3>
    <!--형제, 연결요소여야함-->
    <hr />
    <h1>v-if vs v-show</h1>
    <h2 v-if="display">if 보입니다!!</h2>
    <!-- display=false 일때 ↑ 아예 안나옴-->
    <h2 v-show="display">show 보입니다!!</h2>
    <!-- display= false 일때↑ 태그는 형성이 된다.-->
    <hr />
    <h1>v-for // loop example</h1>
    <h3 v-for="(animal, index) in animals" :key="index">
      <span v-if="animal !== 'monkey'">{{ animal }} 인덱스 ::{{ index }}</span>
    </h3>
    <ul>
      <li v-for="(user, index) in users" :key="index">
        {{ user.name }}은 직업은 {{ user.job }}
        <p v-for="item in user.skill" :key="item">
          {{ item }}
        </p>
      </li>
    </ul>
    <hr />
    <h1>v-on // methods 사용</h1>
    <!-- v-on:click 은 @click로 사용가능하다-->
    <h2 style="color: red">{{ count }}</h2>
    <button v-on:click="addNumber(1)">증가 버튼</button>
    <button v-on:click="minusNumber(1)">감소 버튼</button><br />
    <button v-on:mouseover="addNumber(10)">10씩 증가 버튼</button>
    <button v-on:mouseover="minusNumber(10)">10씩 감소 버튼</button>
    <h2>{{ message }}</h2>
    <button @click="greeting">인사하기</button>
    <button @click="goodbye">작별하기</button>
    <div @click="getMousePosition" class="box"></div>
    <button @click="addNumber($event, 10)">10더하기</button>
    <button @click="addNumber($event, 100)">100더하기</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      subject: "BASIC",
      food: "Apple",
      alertMessage: "<h2>Welcome!</h2>",
      subscribeHTML: `<button onclick="document.querySelector('body').style.background ='red'">구독하기 </button>`,
      imageSource: "https://placeimg.com/100/100/any",
      naverUrl: "https://www.naver.com",
      age: "20",
      display: true,
      animals: ["monkey", "dog", "taeyoung", "bongmin"],
      users: [
        {
          name: "kim",
          job: "developer",
          gender: "male",
          skill: ["html", "css", "js"],
        },
        {
          name: "park",
          job: "front",
          gender: "female",
          skill: ["hi", "bye", "bye2"],
        },
        { name: "yeon", job: "PM", gender: "male", skill: ["공", "무", "원"] },
      ],
      count: 0,
      message: "",
    };
  },
  methods: {
    getMousePosition(event) {
      this.message = `${event.offsetX}, ${event.offsetY}`;
    },
    greeting() {
      this.message = "안녕하세요";
    },
    goodbye() {
      this.message = "안녕히가세요";
    },
    addNumber(e, value) {
      e.offsetX;
      this.message = `${e.offsetX}와 더하기 ${value}는 ${e.offsetX + value}`;
    },
    minusNumber(value) {
      this.count = this.count - value;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
input {
  font-size: 20px;
}
.orange {
  color: orange;
}
.red {
  color: red;
}
.blue {
  color: blue;
}
.not-good {
  text-decoration: line-through;
}
h1 {
  color: rgb(36, 54, 160);
}
button {
  width: 150px;
  height: 50px;
  font-size: 15px;
}
.box {
  width: 50px;
  height: 50px;
  background: salmon;
}
</style>
