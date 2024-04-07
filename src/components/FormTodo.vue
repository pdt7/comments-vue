<template>
    <div class="form-todo form-group">
        <p>
        <input placeholder="nome" type="text" name="author"
            class="form-control" v-model="name"/>
        </p>
        <p>
        <textarea placeholder="Comentário" name="message"
            class="form-control" v-model="message"></textarea>
        </p>
        <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
    </div>
</template>
<script>
export default{
    data:() =>{
        return {
            name: '',
            message: ''
        }
    },  
    methods:{
    addComment(){
        if(this.message.trim()===''){
        return;
        }
        
        this.$emit('add-todo', {
            name: this.name,
            message: this.message
        })

        this.name = '';
        this.message = '';

    },
    removeComment(index){
        this.comments.splice(index, 1);
    }
    },
    computed: {
    allComments(){
        return this.comments.map(comment => ({
        ...comment,
        name: comment.name.trim() === '' ? 'Anônimo' : comment.name
        })

        )
    }
    },
    watch: {
    comments(val){
        console.log('val', val);
    }
    }  
}
</script>