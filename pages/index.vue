<template>
    <div class="grid w-full gap-4">
        <header class="flex items-start justify-between">
            <div class="grow">
                <p>Hi, welcome back!</p>
                <h1>Dashboard</h1>
            </div>
            <div class="w-[120px] h-[36px] bg-neutral-200"></div>
        </header>
        <main class="grid w-full gap-4">
            <Tabs default-value="Today" class="w-full" @click="setCategory">
                <TabsList class="max-w-[400px]">
                    <TabsTrigger v-for="item, index in list" :key='index' :value="item.title">
                        {{item.title}}
                    </TabsTrigger>
                </TabsList>
                <TabsContent class="w-[100%]" v-for="item, index in list" :key="index" :value="item.title">
                    <Chart v-if="data.length > 0" :currentCategory="currentCategory" :data="data" />
                </TabsContent>
            </Tabs>
        </main>
        <footer>
            <div class="flex items-center gap-4">
                <div v-for="(item, index) in 3" :key="index" class="w-full h-[260px] bg-neutral-200"></div>
            </div>
        </footer>
    </div>
</template>
<script setup>
import { Tabs, TabsContent, TabsList, TabsTrigger } from '@/components/ui/tabs'
const list = [
    {
        title: 'Today'
    },
    {
        title: 'Week'
    },
    {
        title: 'Month'
    },
    {
        title: 'Year'
    }
]
let data = ref([])
let currentCategory = ref('today')
const setCategory = (e) => {
    let v = e.target.innerText.toLowerCase()
    currentCategory.value = v
    switch(v) {
        case 'today':
            generateRandomValue(24)
            break
        case 'week':
            generateRandomValue(7)
            break
        case 'month':
            generateRandomValue(31)
            break
        case 'year':
            generateRandomValue(12)
            break
    }
}
function generateRandomValue(number = 7) {
    let values = []
    for(let i = 0; i < number; i++) {
        values.push(Math.floor(Math.random() * 100))
    }
    data.value = values
    return values
}
onMounted(() => {
    generateRandomValue(24)
})
</script>
