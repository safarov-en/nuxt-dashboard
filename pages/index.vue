<template>
    <div class="grid w-full gap-4">
        <header class="flex items-start justify-between">
            <div class="grow">
                <p>Hi, welcome back!</p>
                <h1>Dashboard</h1>
            </div>
            <div class="w-[120px] h-[36px] bg-neutral-200"></div>
        </header>
        <main class="grid gap-4">
            <Tabs default-value="Today">
                <TabsList class="max-w-[400px]">
                    <TabsTrigger v-for="item, index in list" :key='index' :value="item.title">
                        {{item.title}}
                    </TabsTrigger>
                </TabsList>
                <TabsContent v-for="item, index in list" :key="index" :value="item.title">
                    <!-- <component :is='item.component' /> -->
                     <highchart :options="options" />
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
        title: 'Today',
        component: resolveComponent("TabsToday")
    },
    {
        title: 'Week',
        component: resolveComponent("TabsToday")
    },
    {
        title: 'Month',
        component: resolveComponent("TabsToday")
    },
    {
        title: 'Year',
        component: resolveComponent("TabsToday")
    }
]
let data = ref([
            16.0, 18.2, 23.1, 27.9, 32.2, 36.4, 39.8, 38.4, 35.5, 29.2,
            22.0, 17.8
        ])
let categories = ref({
    'today': [],
    'week': [],
    'month': [],
    'year': []
})
let currentCategory = ref([
            'Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep',
            'Oct', 'Nov', 'Dec'
        ])
const options = computed(() => ({
    chart: {
        type: 'line',
        animation: {
            enabled: false
        }
    },
    legend: {
        enabled: false
    },
    title: {
        text: ''
    },
    xAxis: {
        gridLineColor: 'transparent',
        categories: currentCategory
    },
    yAxis: {
        gridLineColor: 'transparent',
        title: {
            text: ''
        }
    },
    plotOptions: {
        line: {
            marker: {
                enabled: false
            },
            dataLabels: {
                enabled: false
            },
            enableMouseTracking: true
        }
    },
    series: [{
        name: 'line',
        lineWidth: '4px',
        color: {
            linearGradient: {},
            stops: [
                [0, 'rgba(252, 176, 69, 1)'],
                [0.33, 'rgba(253, 29, 29, 1)'],
                [0.66, 'rgba(131, 58, 180, 1)'],
                [1, 'rgba(29, 217, 83, 1)']
            ]
        },
        data: data.value
    }]
}))
</script>
