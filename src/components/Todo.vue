<template>
    <div class="ui centered card">
        <div class="content" v-show="!isEditing">
            <div class="header">
                {{ todo.title }}
            </div>
            <div class="meta">
                {{ todo.project }}
            </div>
            <div class="extra content">
                <span class="right floated edit icon" v-on:click="showForm">
                    <i class="edit icon"></i>
                </span>
                <span class="right floated trash icon" v-on:click="deleteTodo(todo)">
                    <i class="trash icon"></i>
                </span>
            </div>
        </div>
        <div class="content" v-show="isEditing">
            <div class="ui form">
                <div class="field">
                    <label>Title</label>
                    <input type="text" v-model="todo.title">
                </div>
                <div class="field">
                    <label>Project</label>
                    <input type="text" v-model="todo.project">
                </div>
                <div class="ui two button attached buttons">
                    <button class="ui basic blue button" v-on:click="hideForm">
                        Close X
                    </button>
                </div>
            </div>
        </div>
        <div class="ui bottom attched green basic button" v-show="!isEditing && todo.done" disabled>
            Completed
        </div>
        <div class="ui bottom attched red basic button" v-show="!isEditing && !todo.done" v-on:click="completeTodo(todo)">
            Complete
        </div>
    </div>
</template>

<script>
export default {
    props: ['todo'],
    data: function() {
        return {
            isEditing: false
        }
    },
    methods: {
        showForm() {
            this.isEditing = true;
        },
        hideForm() {
            this.isEditing = false;
        },
        deleteTodo(todo) {
            this.$swal.fire({
                title: 'Are you sure?',
                text: "This To-Do will be permanently deleted!",
                icon: 'warning',
                showCancelButton: true,
                confirmButtonColor: '#3085d6',
                cancelButtonColor: '#d33',
                confirmButtonText: 'Yes, delete it!'
            }).then((result) => {
                if (result.isConfirmed) {
                    this.$emit('delete-todo', todo);
                    this.$swal.fire(
                        'Deleted!',
                        'Your To-Do has been deleted.',
                        'success'
                    )
                }
            })
        },
        completeTodo(todo) {
            this.$emit('complete-todo', todo);
        }
    }
}
</script>