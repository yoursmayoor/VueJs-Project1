<template>
  <div class="project" :class="{complete: project.complete}">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id }}">
        <span class="material-symbols-outlined"> edit </span>
        </router-link>
        <span @click="deleteProject" class="material-symbols-outlined"> delete </span>
        <span @click="toggleComplete" class="material-symbols-outlined tick"> check </span>
      </div>
    </div>
    <div class="details" v-if="showDetails">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "SingleProject",
  props: ["project"],
  data() {
    return {
      showDetails: false,
      url: 'http://localhost:3000/projects/' + this.project.id,
    };
  },
  methods: {
    deleteProject(){
        fetch(this.url, { method: "DELETE"})
        .then(() => { this.$emit('delete', this.project.id)})
        .catch(err => console.log(err.message))
    },
    toggleComplete(){
        fetch(this.url, {
            method: 'PATCH',
            headers: {'content-type': 'application/json'},
            body: JSON.stringify({complete: !this.project.complete})
        })
        .then(() => {
            this.$emit('complet', this.project.id);
        })
        .catch(err => console.log(err.message))
    }
  }
};
</script>

<style>
.project {
  margin: 20px auto;
  background: #fff;
  padding: 10px 20px;
  border-radius: 5px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.5);
  border-left: 4px solid #e90074;
  text-align: left;
}
h3 {
  cursor: pointer;
}
.actions{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.material-symbols-outlined{
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
}
.material-symbols-outlined:hover{
    color: #777;
}
.project.complete{
    border-left: 4px solid #00ce89;
}
.project.complete .tick{
    color: #00ce89;
}
</style>
