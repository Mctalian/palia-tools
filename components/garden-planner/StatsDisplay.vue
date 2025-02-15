<script setup lang="ts">
import type { PlotStat } from 'assets/scripts/garden-planner/imports'
import { Bonus } from 'assets/scripts/garden-planner/imports'

defineProps<{
  gardenTilesAreWide: boolean
  plotStatTotal: PlotStat
  hoveredBonus: Bonus
}>()

const emit = defineEmits(['update:hoveredBonus'])

const statsDisplay = ref<HTMLDivElement | null>(null)
function getStatsDisplay() {
  return statsDisplay.value
}

function modifyStatsDisplayClassList(callback: (classList: DOMTokenList) => void) {
  const statsDisplay = getStatsDisplay()
  if (statsDisplay)
    callback(statsDisplay.classList)
}

function updateHoveredBonus(bonus: Bonus) {
  emit('update:hoveredBonus', bonus)
}

defineExpose({
  getStatsDisplay,
  modifyStatsDisplayClassList,
})
</script>

<template>
  <div class="my-2 px-2 w-fit">
    <div
      ref="statsDisplay" class="flex flex-wrap gap-2 w-fit px-4 mt-4 cursor-help"
      :class="(gardenTilesAreWide) ? '' : 'lg:grid lg:grid-cols-2'"
    >
      <CoverageStat
        :total-crops="plotStatTotal.cropCount"
        :covered="plotStatTotal.cropBonusCoverage['Quality Increase']" class="text-amber-600"
        @mouseover="updateHoveredBonus(Bonus.QualityIncrease)" @mouseleave="updateHoveredBonus(Bonus.None)"
      >
        <template #icon>
          <font-awesome-icon :icon="['fas', 'star']" />
        </template>
        <template #title>
          Quality Increase
        </template>
      </CoverageStat>

      <CoverageStat
        :total-crops="plotStatTotal.cropCount"
        :covered="plotStatTotal.cropBonusCoverage['Harvest Increase']" class="text-green-600"
        @mouseover="updateHoveredBonus(Bonus.HarvestIncrease)" @mouseleave="updateHoveredBonus(Bonus.None)"
      >
        <template #icon>
          <font-awesome-icon :icon="['fas', 'wheat-awn']" />
        </template>
        <template #title>
          Harvest Increase
        </template>
      </CoverageStat>
      <CoverageStat
        :total-crops="plotStatTotal.cropCount"
        :covered="plotStatTotal.cropBonusCoverage['Water Retain']" class="text-sky-500"
        @mouseover="updateHoveredBonus(Bonus.WaterRetain)" @mouseleave="updateHoveredBonus(Bonus.None)"
      >
        <template #icon>
          <font-awesome-icon :icon="['fas', 'droplet']" />
        </template>
        <template #title>
          Water Retain
        </template>
      </CoverageStat>
      <CoverageStat
        :total-crops="plotStatTotal.cropCount"
        :covered="plotStatTotal.cropBonusCoverage['Speed Increase']" class="text-orange-400"
        @mouseover="updateHoveredBonus(Bonus.SpeedIncrease)" @mouseleave="updateHoveredBonus(Bonus.None)"
      >
        <template #icon>
          <font-awesome-icon :icon="['fas', 'forward-fast']" />
        </template>
        <template #title>
          Growth Boost
        </template>
      </CoverageStat>

      <CoverageStat
        :total-crops="plotStatTotal.cropCount"
        :covered="plotStatTotal.cropBonusCoverage['Weed Prevention']" class="text-rose-400"
        @mouseover="updateHoveredBonus(Bonus.WeedPrevention)" @mouseleave="updateHoveredBonus(Bonus.None)"
      >
        <template #icon>
          <font-awesome-icon :icon="['fas', 'shield']" />
        </template>
        <template #title>
          Weed Prevention
        </template>
      </CoverageStat>
    </div>
  </div>
</template>
