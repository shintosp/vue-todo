<template>
    <div class="container">
        <input type="text" value="hello" class="inputBox" placeholder="Enter Task" v-model="newTask"/>
        <button @click="addNewTask">+ Add</button>
        <div class="display-box">
            <div v-for="(task,index) in tasks" :key="task.id">
                <span v-if="!task.isEditable">{{task.taskName}}</span>
                <input v-else type="text" @keyup.enter="editComplete(task)" v-model="editName"  /> 
                <input type="checkbox" v-model="task.isCompleted" /> 
                <span class="task-button" @click="editTask(task)">Edit</span>
                <span class="task-button" @click="deleteTask(index)">Delete</span>
            </div>
            <button @click="tasks = []">Delete All</button>
            <button @click="sortTasks">Sort</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "TodoList",
        data() {
            return {
                editedName: "",
                newTask: "",
                taskId: 1,
                tasks: []
            }
        },
        methods: {
            addNewTask: function() {
                if(this.newTask.length>0) {
                    this.tasks.push({
                        id: this.taskId,
                        taskName: this.newTask,
                        isCompleted: false,
                        isEditable: false 
                    });
                    this.newTask = "";
                    this.taskId++;
                }
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
            },
            sortTasks: function() {
                let sortedArr = [];
                this.tasks.forEach(item => {
                    if(item.isCompleted==true)
                    {
                        sortedArr.unshift(item);
                    }
                    else {
                        sortedArr.push(item);
                    }
                })
                this.tasks = sortedArr;
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
    max-width: 480px;
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

input[type="checkbox"] {
    opacity: 0.5;
    cursor: pointer;
    &:hover, &:focus {
        opacity: 1;
    }
}

button {
    cursor: pointer;
    padding: 5px 10px;
    font-size: 14px;
    background-color: #962c2c;
    border: none;
    border-radius: 5px;
    margin: 0 10px;
    color: #fff;
    &:hover {
        background-color: #520303;
    }
}
</style>