<template>
  <Layout>
    <!-- Page Header -->
    <header
      class="masthead"
      :style="{backgroundImage: `url(${GRIDSOME_API_URL+general.cover.url})`}"
    >
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{general.title}}</h1>
              <span class="subheading">{{general.subtitle}}p</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div class="post-preview" v-for="edge in $page.posts.edges" :key="edge.node.id">
            <g-link :to="'post/'+edge.node.id">
              <h2 class="post-title">{{edge.node.title}}</h2>
            </g-link>
            <p class="post-meta">
              Posted by
              <a
                href="#"
              >{{edge.node.created_by.firstname + edge.node.created_by.lastname}}</a>
              on {{edge.node.created_at}}
            </p>
            <p>
              <span v-for="tag in edge.node.tags" :key="tag.id">
                <g-link :to="'/tag/'+ tag.id">{{tag.title}}</g-link>&nbsp;&nbsp;
              </span>
            </p>
            <hr />
          </div>
          <Pager :info="$page.posts.pageInfo" />
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query ($page: Int){
	posts:allStrapiPost (perPage: 1, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges{
      node{
        id
        title
        created_by{
          id
          firstname
          lastname
        }
        tags{
          id
          title
        }
        created_at
      }
    }
  }
 general: allStrapiGeneral {
    edges {
      node {
        title
        subtitle
        cover {
          url
        }
      }
    }
  }
}
</page-query>

<script>
import { Pager } from "gridsome";

export default {
  name: "HomePage",
  metaInfo: {
    title: "Hello, world!"
  },
  components: {
    Pager
  },
  computed: {
    general() {
      return this.$page.general.edges[0].node;
    }
  }
};
</script>

<style>
</style>
