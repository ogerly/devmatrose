<template>
  <div class="flex gap-2 flex-wrap items-center">
    <!-- LinkedIn -->
    <a 
      :href="linkedInUrl" 
      target="_blank"
      rel="noopener noreferrer"
      class="btn btn-sm btn-outline border-copper-orange text-copper-orange hover:bg-copper-orange hover:text-void"
      title="Auf LinkedIn teilen"
    >
      <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24">
        <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
      </svg>
      <span class="ml-1">LinkedIn</span>
    </a>

    <!-- Twitter/X -->
    <a 
      :href="twitterUrl" 
      target="_blank"
      rel="noopener noreferrer"
      class="btn btn-sm btn-outline border-cyber-cyan text-cyber-cyan hover:bg-cyber-cyan hover:text-void"
      title="Auf X/Twitter teilen"
    >
      <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24">
        <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
      </svg>
      <span class="ml-1">X/Twitter</span>
    </a>

    <!-- Link kopieren -->
    <button 
      @click="copyLink" 
      class="btn btn-sm btn-outline border-off-white/30 text-off-white hover:bg-off-white hover:text-void"
      :class="{ 'btn-success': linkCopied }"
      title="Link kopieren"
    >
      <svg v-if="!linkCopied" class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z" />
      </svg>
      <svg v-else class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
      </svg>
      <span class="ml-1">{{ linkCopied ? 'Kopiert!' : 'Link' }}</span>
    </button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  post: {
    type: Object,
    required: true
  },
  url: {
    type: String,
    required: true
  }
})

const linkCopied = ref(false)

// LinkedIn Share URL
const linkedInUrl = computed(() => 
  `https://www.linkedin.com/sharing/share-offsite/?url=${encodeURIComponent(props.url)}`
)

// Twitter/X Share URL
const twitterUrl = computed(() => {
  const text = props.post.socialMedia?.twitter?.title || props.post.title
  const hashtags = props.post.socialMedia?.twitter?.hashtags?.join(',') || props.post.tags.slice(0, 3).join(',')
  return `https://twitter.com/intent/tweet?text=${encodeURIComponent(text)}&url=${encodeURIComponent(props.url)}&hashtags=${hashtags}`
})

// Copy Link to Clipboard
const copyLink = async () => {
  try {
    await navigator.clipboard.writeText(props.url)
    linkCopied.value = true
    setTimeout(() => {
      linkCopied.value = false
    }, 3000)
  } catch (err) {
    console.error('Failed to copy link:', err)
  }
}
</script>

<style scoped>
.btn {
  transition: all 0.3s ease;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}
</style>
