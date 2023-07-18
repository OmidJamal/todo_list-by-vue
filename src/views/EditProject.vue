<template>
  <form @submit.prevent="submitHandler">
    <label>عنوان</label>
    <input v-model="title" type="text" required />
    <label>توضیحات</label>
    <textarea v-model="details"></textarea>
    <button>ذخیره</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
      url: "  http://localhost:3000/projects/" + this.id,
    };
  },
  mounted() {
    fetch(this.url)
      .then((res) => res.json())
      .then((data) => {
        this.title = data.title;
        this.details = data.details;
      });
  },
  methods: {
    submitHandler() {
        let updateProject = {
            title: this.title,
            details: this.details
        }
      fetch(this.url, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(updateProject),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => console.log(err.message));
    //   (this.title = ""), (this.details = "");
    },
  },
};
</script>

<style>
</style>