<template>
<div>
    <h1>
        <p>姓名: {{ name }}</p>
        <p>年龄: {{ age }}</p>
        <button @click="onGetTel">获取电话号码</button>
        <button @click="onChangeName">名字修改</button>
        <button @click="onIncreaseAge">年龄增加</button>

        <p>品牌:{{ car.brand }}</p>
        <p>价格:{{ car.price }}万</p>
        <button @click="onChangeCarPrice">汽车涨价</button>
        <button @click="onChangeCar">修改整改汽车</button>

        <p v-for="game in games" :key="game.id" style="text-align: center;">
            {{ game.name }}
        </p>

        <input type="text" v-model="otherName">
        <button @click="onChangeGameName">修改游戏名字</button>
        <br>
    </h1>
    <p id="name">
        姓:<input type="text" v-model="firstName">
        名:<input type="text" v-model="lastName"><br>
        <span>{{ fullName }}</span>
    </p>
</div>
</template>

<script>
export default {
    name: "App",
}
</script>

<script>
import {
    ref,
    reactive,
    toRefs,
    computed
} from 'vue'
// 数据
let name = ref("张三")
let age = ref(24)
let tel = "18338519415"
let car = reactive({
    brand: "奔驰",
    price: 100
})
let games = ref([{
        id: 1,
        name: "原神"
    },
    {
        id: 2,
        name: "三国杀"
    },
    {
        id: 3,
        name: "逃生2"
    },
])
let otherName = ''
let {
    price
} = toRefs(car)
let firstName = ref('张')
let lastName = ref('小三')
let fullName = computed({
    get() {
        return firstName.value.slice(0, 1).toUpperCase() + firstName.value.slice(1) + lastName.value
    },
    set(val) {
        const [str1, str2] = val.split("-")
        firstName.value = str1
        lastName.value = str2
    }
})

// 方法
function onGetTel() {
    alert(tel)
}

function onChangeName() {
    name.value = "李四"
}

function onIncreaseAge() {
    age.value++
}

function onChangeCarPrice() {
    price.value += 10
}

function onChangeCar() {
    Object.assign(car, {
        brand: "宝马",
        price: 120
    })
    // car.value = { brand: "宝马", price: 120 }
}

function onChangeGameName() {
    games.value[0].name = otherName
}
</script>

<style>
h1 {
    font-family: 楷体;
    box-shadow: 0 0 10px;
    background-color: #ddd;
    border-radius: 10px;
    padding: 20px;
    text-align: left;
}

button {
    height: 30px;
    width: 110px;
    font-size: 10px;
    color: red;
    font-family: 楷体;
    margin: 5px;
    border-radius: 5px;
}

#name {
    font-family: 楷体;
    box-shadow: 0 0 10px;
    background-color: #dff;
    border-radius: 10px;
    padding: 20px;
    font-size: 25px;
}

p input {
    width: 100px;
    height: 30px;
    font-size: 20px;
    font-family: 楷体;
    border-radius: 10px;
}
</style>
