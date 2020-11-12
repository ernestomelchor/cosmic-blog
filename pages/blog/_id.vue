<template>
  <div v-if="page">
    <div v-html="page"></div>
  </div>
</template>

<script>
import getPost from "~/queries/getPosts";
export default {
  async asyncData({ app, route, redirect }) {
    try {
      const {data} = await app.apolloProvider.defaultClient.query({
        query: getPost,
        variables: {
          slug: route.params.id,
        },
      });
      return {
        page: data.getObject.content, 
      };
    } catch(error) {
      console.log("error", error);
      redirect("/");
    }
  },
};
</script>

<style lang="scss" scoped>

</style>