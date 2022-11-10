<template>
    <div class="form-todo form-group">
        <p>
            <input  placeholder="Nome" type="text" name="author" class="form-control"
            v-model="name" />
        </p>
        <p>
        <textarea placeholder="Comentario" name="message" class="form-control" v-model="message"></textarea>
        </p>
        <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
    </div>
</template>

<script>

export default {
    data(){
        return {
            name: '',
            message: '',
        }
    },
    methods: {
        addComment() {
            if(this.message.trim() === '') {
                return;
            }
            const myComment = JSON.stringify({name: this.name, message: this.message})
            const actualLocal = localStorage.getItem('comments');
            actualLocal ? localStorage.setItem('comments',
             [...actualLocal, myComment]) :
              localStorage.setItem('comments', myComment)

            this.$emit('add-todo', {
                name: this.name,
                message: this.message,
            })

            this.name = '';
            this.message = '';
        }
    }
}
</script>