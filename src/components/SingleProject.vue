<template>
    <div class="single-todo" style="background-color: #353259" @click="closeOption">
        <!-- <div class="todo__header d-flex flex-row justify-content-between">
            <div class="todo__info">
                <router-link :to="{ name: 'tasks-detail', params: { id: todo.id } }">
                    <div class="todo__name">{{ todo.nameTask }}</div>
                </router-link>  
                <div class="todo__date">{{ todo.deadline }}</div>
            </div>
            <div class="todo__option">
                <i class="fa-solid fa-ellipsis-vertical todo__option-dot" @click="showOption = !showOption"></i>
                <div class="todo__option-menu d-flex flex-column" v-if="showOption">
                    <div class="option-menu__list d-flex align-items-center mb-2" @click="deleteTask">
                        <i class="fa-solid fa-trash"></i>
                        <span class="option-menu__name">Delete</span>
                    </div>
                    <div class="option-menu__list d-flex align-items-center">
                        <router-link :to="{ name: 'edit-todo', params: { id: todo.id } }">
                            <i class="fa-solid fa-pen-to-square"></i>
                            <span class="option-menu__name">Edit</span>
                        </router-link>
                    </div>
                </div>
            </div>
        </div> -->
        <div class="card" style="width: 16rem; border-radius: 10px; background-color: #231e42">
            <div class="card-body" style="position: relative">
                <div class="d-flex justify-content-between">
                    <router-link :to="{ name: 'tasks-detail', params: { id: todo.id } }">
                        <h5 class="card-title" style="color: #fff">{{ todo.nameTask }}</h5>
                    </router-link>
                    <div class="todo__option" style="position: relative; padding: 0 8px; border-radius: 10px" @click="handleClickOption">
                        <i class="fa-solid fa-ellipsis-vertical todo__option-dot" style="cursor: pointer; color: #fff"></i>
                        <div
                            class="todo__option-menu d-flex flex-column"
                            style="
                                position: absolute;
                                background: var(--white-color);
                                box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
                                border-radius: 8px;
                                top: -50px;
                                left: 20px;
                                width: 150px;
                                padding: 8px 16px;
                                z-index: 1;
                                font-size: 18px;
                                cursor: pointer;
                            "
                            v-if="showOption"
                        >
                            <div class="option-menu__list d-flex align-items-center mb-2" @click="deleteTask">
                                <i class="fa-solid fa-trash"></i>
                                <span class="option-menu__name ml-2">Delete</span>
                            </div>
                            <div class="option-menu__list d-flex align-items-center">
                                <router-link :to="{ name: 'edit-todo', params: { id: todo.id } }">
                                    <i class="fa-solid fa-pen-to-square"></i>
                                    <span class="option-menu__name ml-2">Edit</span>
                                </router-link>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="">
                    <p class="card-text" style="font-size: 12px; width: 60%; margin-bottom: 8px; color: #fff">{{ todo.deadline }}</p>
                    <div
                        v-if="todo.status === 'To Do'"
                        class="card-text d-flex justify-content-center"
                        style="font-size: 12px; padding: 4px 2px; background-color: #f3324c; border-radius: 20px; width: 50%"
                    >
                        <div style="color: #fff">{{ todo.status }}</div>
                    </div>
                    <div
                        v-if="todo.status === 'In Progress'"
                        class="card-text d-flex justify-content-center"
                        style="font-size: 12px; padding: 4px 2px; background-color: #feae52; border-radius: 20px; width: 50%"
                    >
                        <div style="color: #fff">{{ todo.status }}</div>
                    </div>
                    <div
                        v-if="todo.status === 'Done'"
                        class="card-text d-flex justify-content-center"
                        style="font-size: 12px; padding: 4px 2px; background-color: #00c664; border-radius: 20px; width: 50%"
                    >
                        <div style="color: #fff">{{ todo.status }}</div>
                    </div>
                </div>
                <!-- <router-link :to="{ name: 'tasks-detail', params: { id: todo.id } }">
                    <a href="#" class="btn btn-primary" style="width: 100%; background-color: #2f61a7">
                        See Details
                        <i class="fa-solid fa-arrow-right ml-2"></i>
                    </a>
                </router-link> -->
            </div>
        </div>
        <!-- <div class="todo__footer mt-4">
            <div class="todo__range">
                <div class="control-time__main">
                    <div class="control-time__current" :style="{ width: width + '%' }">
                        <div style="position: relative">
                            <div class="control-time__dot"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div> -->
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import { useRouter } from "vue-router";
import axios from "axios";

export default defineComponent({
    name: "single-project",
    props: ["user", "todo", "TaskStatusProgress"],
    data() {
        return {
            width: 75,
            showOption: false,
        };
    },
    methods: {
        async deleteTask() {
            await axios
                .delete("http://localhost:8081/tasks/" + this.todo.id, {
                    headers: {
                        Authorization: "Bearer " + localStorage.getItem("token"),
                    },
                })
                .then(() => this.$emit("delete", this.todo.id));
        },
        handleClickOption(event: any) {
            event.stopPropagation();
            this.showOption = !this.showOption;
        },
        closeOption() {
            this.showOption = false;
        },
    },
});
</script>

<style>
.single-todo {
    background-color: var(--white-color);
    padding: 10px 20px;
    border-radius: 10px;
}

.card {
    border: none;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.card-body {
    padding: 1rem 1.25rem;
}
.option-menu__list:hover {
    color: var(--black-color);
}

.option-menu__list:hover a {
    color: var(--black-color);
}
.option-menu__list {
    color: var(--text-color);
}
.option-menu__list a {
    color: var(--text-color);
}

.todo {
    color: rgb(193, 188, 188);
}

.inprogress {
    color: rgb(37, 174, 228);
}

.done {
    color: greenyellow;
}

.card-title {
    -webkit-line-clamp: 1;
    display: -webkit-box;
    overflow: hidden;
    -webkit-box-orient: vertical;
    white-space: normal;
}

.todo__option:hover {
    cursor: pointer;
    background-color: rgb(33, 10, 70);
}
</style>
/* .todo__header { } .todo__info { } .todo__name { font-weight: 600; font-size: 20px; color: var(--black-color); cursor: pointer; } .todo__date { color: var(--text-color); } .todo__range-input {
width: 100%; } .todo__option { font-size: 20px; color: var(--text-color); position: relative; } .todo__range { } .todo__option-dot:hover { cursor: pointer; color: var(--black-color); }
.control-time__main { cursor: pointer; flex: 1; border-radius: 100em; padding: 2.5px 0px; background-color: var(--border-color); position: relative; } .control-time__current { transition: width 0.5s;
position: absolute; border-radius: 100em; padding: 2.5px 0px; top: 0; left: 0; background-color: blueviolet; } .todo__option-menu { position: absolute; background: var(--white-color); box-shadow: 0 0
10px rgba(0, 0, 0, 0.2); border-radius: 8px; top: 25px; left: 0; width: 150px; padding: 8px 16px; z-index: 1; font-size: 18px; } .option-menu__list { cursor: pointer; } .option-menu__list a { color:
var(--text-color); } .option-menu__list:hover { color: var(--black-color); } .option-menu__name { margin-left: 16px; } */
