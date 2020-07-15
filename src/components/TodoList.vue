<template>
    <div class="container">
        <input type="text" value="hello" class="inputBox" placeholder="Enter Text" v-model="newTask"/>
        <button @click="addNewTask">+ Add</button>
        <div class="display-box">
            <div v-for="(task,index) in tasks" :key="task.id">
                <span v-if="!task.isEditable">{{task.taskName}}</span>
                <input v-else type="text" @keyup.enter="editComplete(task)" v-model="editName"  /> 
                <span class="task-button" @click="editTask(task)">Edit</span>
                <span class="task-button" @click="deleteTask(index)">Delete</span>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "TodoList",
        editedNamed: "",
        data() {
            return {
                newTask: "",
                taskId: 1,
                tasks: []
            }
        },
        methods: {
            addNewTask: function() {
                this.tasks.push({
                    id: this.taskId,
                    taskName: this.newTask,
                    isCompleted: false,
                    isEditable: false 
                });
                this.newTask = "";
                this.taskId++;
            },
            editTask: function(task) { 
                this.editName = task.taskName;               
                task.isEditable = true;
            },
            deleteTask: function(index) {
                this.tasks.splice(index, 1);
            },
            editComplete: function(task) {                
                task.taskName = this.editName;
                task.isEditable = false;
            }
        }
    }
</script>
<style lang="scss">
.inputBox {
    font-size: 18px;
    width: 360px;
    padding: 10px;
    border-radius: 5px;
    &:focus {
        outline: 0;
    }
}

.display-box {
    max-width: 430px;
    margin: 30px auto 0;
    text-align: left;
    >div {
        margin-bottom: 10px;
        display: flex;
        justify-content: space-between;
        span {
            padding: 3px 5px;
        }
        .task-button {
            border: 1px solid #ccc;
            cursor: pointer;       
        }
        .task-button:hover {
            box-shadow: 1px 1px 4px rgba(0,0,0,0.4);      
        }
    }
}
</style>