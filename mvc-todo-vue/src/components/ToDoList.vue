<script lang="ts">
export default {
    // props: {
    // },
    data() {
        return {
            todos: [
                {
                    id: 0,
                    text: "Lorem ipsum dolor sit, amet consectetur adipisicing elit. Nulla, suscipit. Doloremque soluta distinctio explicabo?",
                    checked: true
                },
                {
                    id: 1,
                    text: "Test",
                    checked: false
                }
            ],
            inputText: "",
            inputChecked: false,
            filterActive: false,
            filterCompleted: false,
            inputCircleHover: false,
            hoverCircleIndex: -1,
        }
    },
    methods: {
        addTodo(text: string, checked: boolean) {
            let id;
            if (this.todos.length > 0) {
                id = this.todos[this.todos.length - 1].id + 1;
            }
            else id = 0
            const item = {
                id: id,
                text: text,
                checked: checked
            }
            this.todos.push(item)
            this.inputText = "";
        },
        deleteTodo(id: number) {
            const elem = this.todos.find(elem => elem.id === id)
            const index = this.todos.indexOf(elem!);
            this.todos.splice(index, 1)
        },
        checkTodo(id: number) {
            console.log("CHECK");

            const elem = this.todos.find(elem => elem.id === id)
            const index = this.todos.indexOf(elem!);
            this.todos[index].checked = !this.todos[index].checked;
        },
        clearCompletedTodos() {
            let activeTodos = this.todos.filter(elem => elem.checked !== true)
            this.todos = activeTodos;
        },
        setFilter(mode: number) {
            this.filterActive = false;
            this.filterCompleted = false;
            if (mode === 0) return // 'all'
            else if (mode === 1) this.filterActive = true; //'active'
            else if (mode === 2) this.filterCompleted = true; //'completed' 
        },
        toggleInputChecked() { this.inputChecked = !this.inputChecked },

    },
    computed: {
        filterTodos() {
            if (this.filterActive)
                return this.todos.filter(elem => elem.checked === false);
            else if (this.filterCompleted)
                return this.todos.filter(elem => elem.checked === true);
            else return this.todos;
        }
    }
}
</script>

<template>
    <div class="todoItem content-section">
        <div @click="toggleInputChecked" class="circle circleOuter"
            :class="{circleActive: inputChecked, circleOuterHover: inputCircleHover}"
            @mouseover="inputCircleHover = true" @mouseout="inputCircleHover = false">
            <div class="circle innerCircle" :class="{ circleInnerHover: inputCircleHover }">
                <img v-show="inputChecked" class="checkImg" src="../assets/icons/icon-check.svg" alt="">
            </div>
        </div>
        <input type="text" v-model="inputText" @keydown.enter="addTodo(inputText, inputChecked)"
            @keydown.esc="toggleInputChecked" placeholder="type ToDo here..">
    </div>

    <div class="todo-list content-section">
        <div class="todoItem" v-for="(item, index) in filterTodos" :key="item.id">
            <div class="circle circleOuter" @mouseover="hoverCircleIndex = index" @mouseout="hoverCircleIndex = -1"
                :class="{ circleOuterHover: hoverCircleIndex === index }">
                <div @click="checkTodo(item.id)" class="circle innerCircle"
                    :class="{ circleActive: item.checked, circleInnerHover: hoverCircleIndex === index }">
                    <img v-show="item.checked" class="checkImg" src="../assets/icons/icon-check.svg" alt="">
                </div>
            </div>
            <p @click="checkTodo(item.id)" :class="{ completed: item.checked }" @mouseover="hoverCircleIndex = index"
                @mouseout="hoverCircleIndex = -1" class="todoItemText">{{ item.text }}</p>
            <button class="deleteBTN" @click="deleteTodo(item.id)"><img src="../assets/icons/icon-cross.svg"
                    alt="" /></button>
        </div>

        <div class="todoItem lastTodoRow">
            <div>{{ filterTodos.length }} items left</div>
            <button class="clearBTN" @click="clearCompletedTodos">Clear Completed</button>
        </div>
    </div>

    <div class="todoFilterRow content-section">
        <button @click="setFilter(0)" :class="{ filterActive: !filterActive && !filterCompleted }">All</button>
        <button @click="setFilter(1)" :class="{ filterActive: filterActive }">Active</button>
        <button @click="setFilter(2)" :class="{ filterActive: filterCompleted }">Completed</button>
    </div>
</template>

<style scoped>
.content-section {
    background-color: var(--color-elements);
    border-radius: .5em;
}

.todo-list {
    margin: 1em 0;
}

.todoItem {
    display: flex;
    align-items: center;
    padding: 0.8em 1.2em;
    gap: 0.7em;
    border-top: 1px solid var(--color-text-opac-0-5);
}

.todoItem:first-child {
    border: 0;
}

.todoItem p {
    flex: 1;
    cursor: pointer;
}

.completed {
    text-decoration: line-through;
    color: var(--color-text-opac-0-5);
}

.circle {
    width: 25px;
    height: 25px;
    /* margin: 1em; */
    border-radius: 100%;
    border: 1px solid var(--color-text-opac-0-5);
    display: flex;
    padding: 0.3em;
    cursor: pointer;
}

.circleOuterHover {
    background: linear-gradient(135deg, rgba(87, 221, 255, 1) 0%, rgba(192, 88, 243, 1) 100%);
    border: 0;
}

.circle.circleInnerHover {
    background-color: var(--color-elements);
    height: 22px;
    width: 22px;
    margin: auto;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    text-align: center;
}

.circle.circleActive .circleInnerHover {
    background-color: transparent;
}

/* .circleOuter:hover, .todoItemText:hover ~ .circleOuter{
    background: linear-gradient(135deg, rgba(87, 221, 255, 1) 0%, rgba(192, 88, 243, 1) 100%);
    border: 0;
}

.innerCircle:hover, .todoItemText:hover ~ .circleOuter > .innerCircle{
    background-color: var(--color-elements);
    height: 22px;
    width: 22px;
    margin: auto;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    text-align: center;
} */

.innerCircle {
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    border: 0;
}

.circleActive {
    background: linear-gradient(135deg, rgba(87, 221, 255, 1) 0%, rgba(192, 88, 243, 1) 100%);
    border: 0;
}

.checkImg {
    width: 100%
}

input[type=text] {
    background-color: var(--color-elements);
    border: 0;
    flex: 1;
}

input[type=text]:focus {
    outline: transparent;
}

.lastTodoRow {
    color: var(--color-text-opac-0-5);
    justify-content: space-between;
    /* ToDo: min height for this elem */
}

.todoFilterRow {
    display: flex;
    justify-content: center;
    gap: 1em;
    padding: 1em;
}

button {
    background-color: transparent;
    color: var(--color-text-opac-0-5);
    border: 0;
}

button:hover {
    color: var(--color-text-hover)
}

.filterActive {
    color: var(--color-text-active)
}

.deleteBTN img:hover {
    filter: invert(94%) sepia(4%) saturate(493%) hue-rotate(198deg) brightness(96%) contrast(97%);
}
</style>