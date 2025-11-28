<script setup lang="ts">
// 使用 Nuxt 4 的 useSeoMeta
  useSeoMeta({
    title: '探索模块 - Nuxt 4 Starter',
    description: '探索 Nuxt 生态系统中的热门模块'
  })

  // 使用 useFetch 获取 Nuxt 模块数据 (SSR 友好)
  const { data: modules, status } = await useFetch<{
    modules: Array<{
      name: string
      description: string
      repo: string
      npm: string
      icon: string
      github: string
      website: string
      category: string
      stats: { downloads: number, stars: number }
    }>
  }>('https://api.nuxt.com/modules', {
    query: { version: '3.x' },
    pick: ['modules'],
    transform: res => ({
      modules: res.modules.slice(0, 8)
    })
  })

  // 格式化下载数
  function formatNumber(num: number): string {
    if (num >= 1000000)
      return `${(num / 1000000).toFixed(1)}M`
    if (num >= 1000)
      return `${(num / 1000).toFixed(1)}K`
    return num.toString()
  }
</script>

<template>
  <div class="min-h-screen bg-background">
    <div class="container mx-auto px-4 py-16">
      <!-- Header -->
      <div class="mb-12 text-center">
        <Badge variant="outline" class="mb-4">
          <Icon name="lucide:package" class="mr-1 size-3" />
          useFetch 示例
        </Badge>
        <h1 class="mb-4 text-3xl font-bold">
          探索 Nuxt 模块
        </h1>
        <p class="text-muted-foreground">
          使用 Nuxt 4 的 useFetch 从 API 获取数据
        </p>
      </div>

      <!-- Loading State -->
      <div v-if="status === 'pending'" class="flex justify-center py-20">
        <Icon name="lucide:loader-2" class="size-8 animate-spin text-primary" />
      </div>

      <!-- Modules Grid -->
      <div v-else-if="modules?.modules" class="grid gap-4 md:grid-cols-2 lg:grid-cols-4">
        <Card v-for="mod in modules.modules" :key="mod.name" class="group transition-all hover:shadow-lg">
          <CardHeader class="pb-2">
            <div class="flex items-start justify-between">
              <div class="flex size-10 items-center justify-center rounded-lg bg-muted">
                <Icon name="lucide:package" class="size-5" />
              </div>
              <Badge variant="secondary" class="text-xs">
                {{ mod.category }}
              </Badge>
            </div>
            <CardTitle class="mt-3 text-base">
              {{ mod.name }}
            </CardTitle>
          </CardHeader>
          <CardContent>
            <CardDescription class="line-clamp-2 text-sm">
              {{ mod.description }}
            </CardDescription>
            <div class="mt-4 flex items-center justify-between text-xs text-muted-foreground">
              <span>
                <Icon name="lucide:download" class="mr-1 inline size-3" />
                {{ formatNumber(mod.stats.downloads) }}
              </span>
              <span>
                <Icon name="lucide:star" class="mr-1 inline size-3" />
                {{ formatNumber(mod.stats.stars) }}
              </span>
            </div>
          </CardContent>
          <CardFooter class="pt-0">
            <NuxtLink
              :to="mod.website || `https://github.com/${mod.repo}`"
              external
              target="_blank"
              class="inline-flex items-center text-sm text-primary hover:underline"
            >
              查看详情
              <Icon name="lucide:external-link" class="ml-1 size-3" />
            </NuxtLink>
          </CardFooter>
        </Card>
      </div>

      <!-- Back Link -->
      <div class="mt-12 text-center">
        <NuxtLink to="/">
          <Button variant="outline">
            <Icon name="lucide:arrow-left" class="mr-2 size-4" />
            返回首页
          </Button>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>
