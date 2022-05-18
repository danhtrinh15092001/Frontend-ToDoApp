<template>
    <div class="" style="padding: 20px">
        <div class="d-flex" @click="closeOption">
            <div class="d-flex flex-column" style="background-color: #353259; padding: 0 20px; border-radius: 10px; height: auto; position: fixed; z-index: 1">
                <div class="d-flex align-items-center mb-5">
                    <svg fill="#ffffff" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 30 30" width="30px" height="30px">
                        <path d="M23,27l-8-7l-8,7V5c0-1.105,0.895-2,2-2h12c1.105,0,2,0.895,2,2V27z" />
                    </svg>
                    <div class="" style="font-size: 28px; color: #fff; font-weight: 550">To Do App</div>
                </div>
                <div class="d-flex flex-column">
                    <div style="background-color: #231e42; border-radius: 10px">
                        <ul style="list-style-type: none; padding: 0 32px 0 20px; margin: 8px 0; color: #fff" class="list_activity">
                            <li class="d-flex align-items-center item_activity" style="padding: 14px 80px 14px 14px" ref="myItem">
                                <i class="fa-solid fa-tablet" style="margin-right: 12px"></i>
                                <div>Dashboard</div>
                            </li>
                            <li class="d-flex align-items-center item_activity" style="padding: 14px 100px 14px 14px" ref="myItem">
                                <i class="fa-solid fa-check-double" style="margin-right: 12px"></i>
                                <div>MyTask</div>
                            </li>
                            <li class="d-flex align-items-center item_activity" style="padding: 14px 80px 14px 14px" ref="myItem">
                                <i class="fa-solid fa-gear" style="margin-right: 12px"></i>
                                <div>Setting</div>
                            </li>
                        </ul>
                    </div>
                    <div>
                        <div
                            class="d-flex align-items-center"
                            style="margin-top: 200px; padding: 8px 0 8px 8px; border-radius: 10px; background-color: #231e42; cursor: pointer; position: relative"
                            @click="clickLogout"
                        >
                            <img
                                src="https://scontent.fsgn3-1.fna.fbcdn.net/v/t1.6435-9/120836647_113249040545341_5445297340173352633_n.jpg?_nc_cat=107&ccb=1-5&_nc_sid=174925&_nc_ohc=tGxdzjhN8OQAX-8tczI&_nc_ht=scontent.fsgn3-1.fna&oh=00_AT94mRFylE1fGJWSfK5BoHoBGcMsTCF1GEktbc9PO9QdlQ&oe=62965E37"
                                alt=""
                                style="height: 50px; weight: 50px; margin-right: 8px"
                                class="rounded-circle"
                            />
                            <div style="color: #fff">
                                <div class="" style="font-weight: 500; font-size: 18px">{{ user.name }}</div>
                                <div style="font-size: 14px">Computer Science</div>
                            </div>
                            <div
                                class="todo__option"
                                style="font-size: 20px; position: absolute; top: 0; right: 0; transform: translateY(-100%); background-color: #ddd; padding: 8px; border-radius: 8px"
                                ref="Logout"
                                v-if="show"
                                @click="handleClick"
                            >
                                <div class="todo__option-menu d-flex flex-column">
                                    <div class="option-menu__list d-flex align-items-center">
                                        <i class="fa-solid fa-right-from-bracket"></i>
                                        <span class="option-menu__name">Logout</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="" style="padding: 0 0 0 20px; position: relative; margin-left: 300px">
                <div class="d-flex justify-content-between">
                    <div>
                        <div style="font-size: 30px; font-weight: 550; margin-right: 20rem; color: #fff">
                            <i class="fa-solid fa-check"></i>
                            My Task
                        </div>
                        <div class="mt-2" style="width: 400px; font-size: 16px; color: #fff">
                            Click
                            <router-link :to="{ name: 'add-todo' }" style="padding: 4px; background-color: #eee; border-radius: 10px; margin: 0 4px; text-decoration: none"> + New Task </router-link>
                            or click the add button at the bottom right corner of the screen to create new task.
                        </div>
                    </div>

                    <div class="">
                        <div style="padding: 10px 20px; background-color: #fff; border-radius: 10px; box-shadow: 0 0 10px rgba(0, 0, 0, 0.1)">
                            <i class="fa-solid fa-magnifying-glass" style="color: #aaa"></i>
                            <input type="text" name="" id="" placeholder="Search..." v-model="search" style="border: none; margin-left: 1rem; width: 300px" class="search__input" />
                        </div>
                    </div>
                </div>
                <div class="pt-4 px-3" style="border-bottom: 1px solid #ccc; color: #fff">
                    <FilterNav @filterChange="current = $event" :current="current"></FilterNav>
                </div>
                <div class="home__center d-flex flex-wrap">
                    <div v-for="todo in filteredSearch" :key="todo.nameTask" class="todo__listx">
                        <SingleProject :user="user" :todo="todo" @delete="handleDelete"></SingleProject>
                    </div>
                </div>
                <router-link :to="{ name: 'add-todo' }">
                    <div style="position: fixed; padding: 24px; border-radius: 10px; background-color: #fff; box-shadow: 0 0 10px rgba(0, 0, 0, 0.2); cursor: pointer; bottom: 40px; right: 50px">
                        <i class="fa-solid fa-plus" style="font-size: 32px"></i>
                    </div>
                </router-link>
            </div>
        </div>
    </div>
    <!-- <div v-if="user" class="home__page mt-3 flex">
        <div class="home__header d-flex flex-row justify-content-between">
            <div class="home__header-title">To Do List</div>
            <div class="home__header-search">
                <div class="input-group">
                    <input type="text" class="form-control" v-model="search" placeholder="Search ToDo" aria-label="Search ToDo" aria-describedby="basic-addon2" />
                </div>
            </div>
        </div>
        <div class="home__nav pt-3 px-3">
            <FilterNav @filterChange="current = $event" :current="current"></FilterNav>
        </div>
        <div class="home__center">
            <div v-for="todo in filteredSearch" :key="todo.nameTask" class="todo__list mt-3">
                <SingleProject :user="user" :todo="todo" @delete="handleDelete"></SingleProject>
            </div>
        </div>
        <div class="home__footer-add">
            <div class="todo__add">
                <router-link :to="{ name: 'add-todo' }">
                    <div class="todo__add-btn d-flex flex-row justify-content-center">
                        <div class="add-btn__icon mr-3">
                            <i class="fa-solid fa-plus"></i>
                        </div>
                        <div class="add-btn__title">Add ToDo</div>
                    </div>
                </router-link>
            </div>
        </div>
    </div> -->
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from "vue";
import axios from "axios";
import SingleProject from "../components/SingleProject.vue";
import FilterNav from "../components/FilterNav.vue";
import { Task, TaskDetail, TaskStatus } from "../types/data";

export default defineComponent({
    name: "home-page",
    props: ["user"],
    components: { SingleProject, FilterNav },
    data() {
        return {
            search: "",
            todolist: [],
            current: "all",
            show: false,
            hover: false,
        };
    },

    async created() {
        const res = await axios.get("http://localhost:8081/users/me/tasks/all", {
            headers: {
                Authorization: "Bearer " + localStorage.getItem("token"),
            },
        });
        this.todolist = res.data;
        this.todolist.map((task: Task) => {
            const dateTransform = new Date(task.deadline).toDateString();
            task.deadline = dateTransform;
        });
    },
    computed: {
        filteredSearch(): Task[] {
            const statusTask = this.todolist.map((task: Task) => {
                const countFinishedTask = task.tasksDetail.reduce((result: number, taskDetail: TaskDetail) => {
                    return taskDetail.state ? result + 1 : result;
                }, 0);

                const numTaskDetail = task.tasksDetail.reduce((result: number, taskDetail: TaskDetail) => {
                    return result + 1;
                }, 0);

                if (numTaskDetail === 0) {
                    return TaskStatus.ToDo;
                } else if (countFinishedTask === numTaskDetail) {
                    return TaskStatus.Done;
                } else if (countFinishedTask !== numTaskDetail) {
                    return TaskStatus.InProgress;
                }
            });

            const newList = this.todolist.map((task: Task, index: number) => {
                return {
                    ...task,
                    status: statusTask[index],
                };
            });

            // return this.todolist.filter((todo: Task) => todo.nameTask.includes(this.search));
            return newList.filter((todo: Task) => todo.nameTask.includes(this.search));
        },
    },
    methods: {
        handleDelete(id: any) {
            this.todolist = this.todolist.filter((todo: Task) => {
                return todo.id !== id;
            });
        },
        async handleClick() {
            localStorage.removeItem("token");
            await this.$router.push("/login");
        },
        closeOption() {
            this.show = false;
        },
        clickLogout(event: any) {
            event.stopPropagation();
            this.show = !this.show;
            console.log(this.$refs.Logout);
        },
    },
});
</script>

<style>
.item_activity:hover {
    cursor: pointer;
    background-color: #353259;
    border-radius: 10px;
}

.hover__active {
    background-color: #353259;
    border-radius: 10px;
    font-weight: 550;
}

/* .home__page {
    width: 50%;
    margin: auto;
    margin-bottom: 2rem;
    background-color: rgb(247, 247, 247);
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    border-radius: 10px;
}

.home__header {
    background-color: var(--white-color);
    padding: 16px 16px;
    border-radius: 10px;
}

.home__header-title {
    font-size: 28px;
}

.home__header-search {
}

.home__header-search.open {
}

.header-search__input {
}

.header-search__btn {
    border-radius: 10px;
}

.home__footer-add {
    padding: 16px 16px;
}

.home__nav {
    border-bottom: 1px solid #ccc;
    background-color: var(--white-color);
}

.home__nav button {
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
}

.home__nav button.active {
    color: #555;
}

.todo__list {
    padding: 8px 16px;
}

.todo__add {
    padding: 10px 16px;
    border-radius: 10px;
    background-color: var(--primary-color);
}

.todo__add a:hover {
    text-decoration: none;
}

.todo__add-btn {
    color: var(--white-color);
} */
.search__input:focus {
    border: none !important;
    outline: none !important;
}
</style>
