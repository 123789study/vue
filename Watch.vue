<template>
<div id="index">
    <!-- 简简单单打印HelloWorld -->
    <p class="English">{{ str1 }}</p>
    <p class="Chinese">{{ str2 }}</p>
    <input type="text" v-model="str3" placeholder="请在里面输入内容" />
    <p class="Chinese">{{ str3 }}</p>
    <button @click="onChangeText">修改内容</button>

    <!-- 使用ref处理对象类型 -->
    <p class="Chinese" style="text-align: center">
        姓名:{{ person.name }}<br />年龄:{{ person.age }}
    </p>
    <button @click="onChangeName">修改名字</button>
    <button @click="onIncreaseAge">增加年龄</button>
    <button @click="onPerson">改变整改人</button>
    <!-- 使用reactive处理对象类型 -->
    <div id="list">
        <ul>
            <li v-for="game in games" :key="game.id">
                {{ game.name }}
                <button @click="onDelete(game)" style="color: red; width: 50px; height: 50px">
                    X
                </button>
            </li>
        </ul>
        <form @submit.prevent="onAddNewGame">
            <input required v-model="newGame" placeholder="请输入新的游戏名称" />
            <button>增加新的游戏</button>
        </form>
        <button @click="onClearGame">清空所有的游戏</button>
    </div>

    <div>
        <p class="Chinese" style="text-align: center;">
            富人名称:{{ richMan.name }}<br />
            富人年龄:{{ richMan.age }} <br />
            富人的车:{{ richMan.car }} <br />
            富人的房:{{ richMan.house }}<br />
        </p>
        <button @click="onChangeRichManName">修改名字</button>
        <button @click="onChangeRichManAge">修改年龄</button>
        <button @click="onChangeRichManCar">修改车</button>
        <button @click="onChangeRichManHouse">修改房子</button>
    </div>
</div>
</template>

<script>
import {
    ref,
    reactive,
    watch
} from "vue";

// 数据
let str1 = ref("Hello,World!");
let str2 = ref("你好,世界!");
let str3 = ref("");
let person = ref({
    name: "张三",
    age: 18,
});
let count = 0;
let newGame = "";
let games = reactive([{
        id: count++,
        name: "原神"
    },
    {
        id: count++,
        name: "明日方舟"
    },
    {
        id: count++,
        name: "三国杀"
    },
    {
        id: count++,
        name: "小小梦魇"
    },
]);
let richMan = reactive({
    name: ref("下北泽"),
    age: 114514,
    car: {
        c1: "奔驰",
        c2: "宝马",
    },
    house: ["楼房", "别墅", "桥洞"],
});

// 方法
function onChangeText() {
    str2.value = str3.value;
}

function onChangeName() {
    person.value.name += "~";
}

function onIncreaseAge() {
    person.value.age += 1;
}

function onPerson() {
    person.value = {
        name: "李四",
        age: 24,
    };
}

function onAddNewGame() {
    games.push({
        id: count++,
        name: newGame,
    });
    newGame = "";
}

function onDelete(game) {
    const index = games.findIndex((g) => g.id === game.id);
    if (index !== -1) {
        games.splice(index, 1);
    }
}

function onClearGame() {
    games.splice(0, games.length);
}

function onChangeRichManName() {
    richMan.name = "田所浩二"
}

function ChangeRichManAge() {
    richMan.age++
}

function ChangeRichManCar() {
    richMan.car = {
        c1: "解放",
        c2: "鸽子",
    }
}

function ChangeRichManHouse() {
    richMan.house = ["瓦房", "茅草屋"];
}
// 监视
//1.ref基本   2.ref对象   3.reactive对象  4.reactive,ref处理具体属性
watch(str2, (newValue, oldValue) => {
    console.log(newValue, oldValue);
});
watch(
    person,
    (newValue, oldValue) => {
        console.log("person变化了", newValue, oldValue);
    }, {
        deep: true,
        immediate: true
    }
);
watch(games, (newValue, oldValue) => {
    console.log(newValue, oldValue);
});
</script>


<style>
.English {
  font-size: larger;
  font-family: 微软雅黑;
  box-shadow: 0 0 10px;
  background-color: #7c859e;
  border-radius: 10px;
  padding: 20px;
  text-align: left;
}

.Chinese {
  font-size: larger;
  font-family: 楷体;
  box-shadow: 0 0 10px;
  background-color: #ddd;
  border-radius: 10px;
  padding: 20px;
  text-align: left;
}

#list {
  box-shadow: 0 0 10px;
  border-radius: 10px;
  background-color: #ddd;
  margin: 10px;
  padding: 20px;
}

input,
button {
  border-radius: 5px;
  width: 300px;
  height: 50px;
  font-family: 楷体;
  font-size: 30px;
}

li {
  font-family: 楷体;
  font-size: 30px;
  font-weight: 1000;
  list-style-type: none;
}
</style>


