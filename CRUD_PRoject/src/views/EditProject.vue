<template>
  <form @submit.prevent="handleUpdate">
    <label for="title"> Title</label>
    <input type="text" v-model="title" id="title">
    <label for="title"> Details</label>
    <textarea name="detials" id="" cols="30" rows="10" v-model="details"></textarea>
    <button >Update Project</button>
  </form>
</template>

<script>
export default {
props: ['id'],
data(){
    return{
        title: '',
        details: '',
        url: 'http://localhost:3000/projects/'+ this.id
    }
},
mounted(){
    fetch(this.url)
    .then(resp => resp.json())
    .then(data => {
        this.title = data.title;
        this.details = data.details
    })
},
methods: {
    handleUpdate(){
        let updatedProject = {
            title: this.title,
            details : this.details
        }
        fetch(this.url, {
            method: "PATCH",
            headers: {"content-type": "application/json"},
            body: JSON.stringify(updatedProject)
        })
        .then(() => {
            this.$router.push('/');
        })
        .catch(err => console.log(err.message))
    }
}
}
</script>

<style>
form{
    background: #fff;
    padding: 20px;
    border-radius: 10px;
}
label{
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0;
    text-align: left;
}
input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
}
textarea{
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
}
form button{
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: #fff;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
}
</style>