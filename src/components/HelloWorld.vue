<script setup>
import { ref } from 'vue'
import { Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from '@/components/ui/table'
import { Badge } from '@/components/ui/badge'
import { Progress } from '@/components/ui/progress'

// 铁锈战争段位数据
const rankings = ref([
  { id: 1, name: 'RustLord', score: 9500, trend: 'up', rank: 'diamond', progress: 95 },
  { id: 2, name: 'MetalTitan', score: 8900, trend: 'down', rank: 'platinum', progress: 89 },
  { id: 3, name: 'IronWarlord', score: 8200, trend: 'up', rank: 'platinum', progress: 82 },
  { id: 4, name: 'SteelCommander', score: 7800, trend: 'up', rank: 'gold', progress: 78 },
  { id: 5, name: 'BronzeRaider', score: 6500, trend: 'down', rank: 'silver', progress: 65 },
  { id: 6, name: 'CopperMerc', score: 5200, trend: 'up', rank: 'bronze', progress: 52 },
  { id: 7, name: 'IronRecruit', score: 3200, trend: 'down', rank: 'iron', progress: 32 }
])

// 段位图标映射
const rankIcons = {
  diamond: '💎',
  platinum: '🔘',
  gold: '🏆',
  silver: '🥈',
  bronze: '🥉',
  iron: '⚙️'
}

// 段位颜色映射
const rankColors = {
  diamond: 'bg-gradient-to-r from-blue-400 to-purple-500',
  platinum: 'bg-gradient-to-r from-gray-300 to-gray-400',
  gold: 'bg-gradient-to-r from-yellow-400 to-yellow-600',
  silver: 'bg-gradient-to-r from-gray-200 to-gray-300',
  bronze: 'bg-gradient-to-r from-amber-600 to-amber-800',
  iron: 'bg-gradient-to-r from-gray-500 to-gray-700'
}
</script>

<template>
  <div class="p-4 bg-gray-900 rounded-lg">
    <h2 class="text-2xl font-bold mb-4 text-yellow-400 text-center">
      <span class="text-red-500">铁锈战争</span> 段位排行榜
    </h2>
    
    <Table class="w-full max-w-3xl mx-auto border border-yellow-600 rounded-lg bg-gray-800">
      <TableHeader class="bg-gray-700">
        <TableRow class="hover:bg-gray-700">
          <TableHead class="text-yellow-400 font-bold">排名</TableHead>
          <TableHead class="text-yellow-400 font-bold">玩家</TableHead>
          <TableHead class="text-yellow-400 font-bold">段位</TableHead>
          <TableHead class="text-yellow-400 font-bold text-right">分数</TableHead>
          <TableHead class="text-yellow-400 font-bold">进度</TableHead>
        </TableRow>
      </TableHeader>
      <TableBody>
        <TableRow 
          v-for="item in rankings" 
          :key="item.id"
          class="hover:bg-gray-700/50 transition-colors border-b border-gray-600"
        >
          <TableCell class="font-bold text-gray-300">#{{ item.id }}</TableCell>
          <TableCell class="font-medium text-gray-100">{{ item.name }}</TableCell>
          <TableCell>
            <Badge :class="[rankColors[item.rank], 'text-white']">
              <span class="mr-1">{{ rankIcons[item.rank] }}</span>
              {{ item.rank.toUpperCase() }}
            </Badge>
          </TableCell>
          <TableCell class="text-right">
            <Badge :variant="item.trend === 'up' ? 'success' : 'destructive'" class="font-mono">
              {{ item.score.toLocaleString() }}
              <span class="ml-1">{{ item.trend === 'up' ? '↑' : '↓' }}</span>
            </Badge>
          </TableCell>
          <TableCell>
            <div class="flex items-center gap-2">
              <Progress 
                :model-value="item.progress" 
                class="h-2 bg-gray-600"
                :class="{
                  'bg-blue-400': item.rank === 'diamond',
                  'bg-gray-300': item.rank === 'platinum',
                  'bg-yellow-400': item.rank === 'gold',
                  'bg-gray-200': item.rank === 'silver',
                  'bg-amber-600': item.rank === 'bronze',
                  'bg-gray-500': item.rank === 'iron'
                }"
              />
              <span class="text-xs text-gray-400">{{ item.progress }}%</span>
            </div>
          </TableCell>
        </TableRow>
      </TableBody>
    </Table>
    
    <div class="mt-4 text-center text-gray-400 text-sm">
      赛季结束时间: 2023-12-31 23:59
    </div>
  </div>
</template>

<style scoped>
/* 添加一些铁锈风格的装饰 */
.bg-gray-900 {
  background-color: #111827;
  background-image: 
    radial-gradient(circle at 10% 20%, rgba(139, 92, 0, 0.1) 0%, transparent 20%),
    radial-gradient(circle at 90% 80%, rgba(139, 92, 0, 0.1) 0%, transparent 20%);
}

.border-yellow-600 {
  border-color: #ca8a04;
}

.text-yellow-400 {
  color: #facc15;
}

.text-red-500 {
  color: #ef4444;
}
</style>
