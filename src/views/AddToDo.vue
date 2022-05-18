<template>
    <form class="form__add" @submit.prevent="handleSubmit">
        <div class="detail-header__icon d-flex align-items-center" @click="backHomePage">
            <i class="fa-solid fa-arrow-left mr-4"></i>
            <h3>Add New ToDo</h3>
        </div>

        <label class="form__add-name">Name Task</label>
        <input type="text" class="form__add-input" required v-model="newTask.nameTask" />
        <label class="form__add-name">Dealine</label>
        <input type="datetime-local" required class="form__add-input" v-model="newTask.deadline" />
        <label class="form__add-name">Description</label>
        <textarea required v-model="newTask.description"></textarea>
        <button style="background-color: #00c664">Add Project</button>
    </form>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { useRouter } from "vue-router";
import axios from "axios";
export default defineComponent({
    name: "add-todo",
    data() {
        return {
            newTask: {
                nameTask: "",
                deadline: "",
                description: "",
            },
        };
    },
    methods: {
        async handleSubmit() {
            let todo = {
                nameTask: this.newTask.nameTask,
                deadline: this.newTask.deadline + ":00.000Z",
                description: this.newTask.description,
            };

            const res = await axios.post("http://localhost:8081/users/me/tasks/store", todo, {
                headers: {
                    Authorization: "Bearer " + localStorage.getItem("token"),
                },
            });
            console.log(res);
            await this.$router.push("/users/me/tasks/all");
        },
        async backHomePage() {
            await this.$router.push("/users/me/tasks/all");
        },
    },
    computed: {
        dateLocal() {
            return this.newTask.deadline.substring(0, 16);
        },
    },
});
</script>

<style></style>
