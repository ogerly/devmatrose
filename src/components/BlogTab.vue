<template>
  <div class="container mx-auto py-12">
    <BlogList 
      showHeader
      title="Blog"
      subtitle="Deep Dives, Architektur-Entscheidungen und technische Insights"
      @read-more="handleReadMore"
    />
  </div>
</template>

<script setup>
import BlogList from './blog/BlogList.vue'

const handleReadMore = (post) => {
  // Später: Detail-Ansicht mit Markdown-Rendering
  console.log('Navigate to post:', post.slug)
  alert(`Detail-Ansicht für "${post.title}" kommt in der nächsten Phase!`)
}
</script>
