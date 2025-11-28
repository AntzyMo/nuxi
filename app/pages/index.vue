<script setup lang="ts">
  // 使用 Nuxt 4 的 useSeoMeta 设置页面 SEO
  useSeoMeta({
    title: 'Nuxt 4 Starter - 现代化全栈框架示例',
    description: '探索 Nuxt 4 框架特性与 shadcn-vue 组件库的完美集成'
  })

  // Nuxt 4 核心特性列表
  const features = [
    { icon: 'lucide:sparkles', title: 'Auto-imports', description: '组件、composables 和工具函数自动导入，无需手动 import' },
    { icon: 'lucide:server', title: 'SSR / SSG', description: '服务端渲染与静态生成，开箱即用的 SEO 优化' },
    { icon: 'lucide:folder-tree', title: '文件路由', description: '基于文件系统的路由，pages 目录自动生成路由配置' },
    { icon: 'lucide:zap', title: 'useFetch', description: 'SSR 友好的数据获取，自动处理服务端/客户端状态同步' }
  ]

  // 技术栈展示
  const techStack = [
    { name: 'Nuxt 4', role: '全栈框架', avatar: 'N4' },
    { name: 'Vue 3', role: '响应式 UI', avatar: 'V3' },
    { name: 'shadcn-vue', role: '组件库', avatar: 'SV' }
  ]
</script>

<template>
  <div class="min-h-screen bg-background">
    <!-- Hero Section -->
    <header class="container mx-auto px-4 py-16 text-center">
      <Badge variant="secondary" class="mb-4">
        <Icon name="lucide:rocket" class="mr-1 size-3" />
        Nuxt 4 + shadcn-vue
      </Badge>
      <h1 class="mb-4 text-4xl font-bold tracking-tight md:text-6xl">
        <span class="text-gradient">Nuxt 4 Starter</span>
      </h1>
      <p class="mx-auto mb-8 max-w-2xl text-lg text-muted-foreground">
        探索 Nuxt 4 框架特性与 shadcn-vue 组件库的完美集成
      </p>
      <div class="flex justify-center gap-4">
        <NuxtLink to="/explore">
          <Button size="lg">
            <Icon name="lucide:compass" class="mr-2 size-4" />
            探索示例
          </Button>
        </NuxtLink>
        <NuxtLink to="https://nuxt.com/docs" external target="_blank">
          <Button variant="outline" size="lg">
            <Icon name="lucide:book-open" class="mr-2 size-4" />
            查看文档
          </Button>
        </NuxtLink>
      </div>
    </header>

    <Separator />

    <!-- Features Section -->
    <section class="container mx-auto px-4 py-16">
      <h2 class="mb-12 text-center text-3xl font-bold">
        Nuxt 4 核心特性
      </h2>
      <div class="grid gap-6 md:grid-cols-2 lg:grid-cols-4">
        <Card v-for="feature in features" :key="feature.title" class="transition-shadow hover:shadow-lg">
          <CardHeader>
            <div class="mb-2 flex size-12 items-center justify-center rounded-lg bg-primary/10">
              <Icon :name="feature.icon" class="size-6 text-primary" />
            </div>
            <CardTitle>{{ feature.title }}</CardTitle>
          </CardHeader>
          <CardContent>
            <CardDescription>{{ feature.description }}</CardDescription>
          </CardContent>
        </Card>
      </div>
    </section>

    <!-- Tech Stack Section -->
    <section class="container mx-auto px-4 py-16">
      <h2 class="mb-12 text-center text-3xl font-bold">
        技术栈
      </h2>
      <div class="flex flex-wrap justify-center gap-8">
        <Card v-for="tech in techStack" :key="tech.name" class="w-64 text-center">
          <CardHeader class="items-center">
            <Avatar class="size-20">
              <AvatarFallback class="text-lg font-bold">
                {{ tech.avatar }}
              </AvatarFallback>
            </Avatar>
            <CardTitle class="mt-4">
              {{ tech.name }}
            </CardTitle>
            <Badge variant="outline">
              {{ tech.role }}
            </Badge>
          </CardHeader>
        </Card>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="container mx-auto px-4 py-16">
      <Card class="glass mx-auto max-w-xl p-8 text-center">
        <CardHeader>
          <CardTitle class="text-2xl">
            <Icon name="lucide:github" class="mr-2 inline size-6" />
            开始使用
          </CardTitle>
          <CardDescription>
            克隆此模板，快速启动你的 Nuxt 4 项目
          </CardDescription>
        </CardHeader>
        <CardContent>
          <div class="flex gap-2">
            <Input readonly value="npx nuxi init my-app" class="flex-1 font-mono text-sm" />
            <Button>
              <Icon name="lucide:copy" class="size-4" />
            </Button>
          </div>
        </CardContent>
      </Card>
    </section>

    <!-- Footer -->
    <footer class="border-t py-8 text-center text-sm text-muted-foreground">
      <p>Built with Nuxt 4 & shadcn-vue · Open Source</p>
    </footer>
  </div>
</template>
