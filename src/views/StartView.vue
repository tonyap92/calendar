<script setup>
import { ref, reactive, computed } from 'vue';
import AppPopap from '@/components/AppPopap.vue';
import DayInfo from '@/components/DayInfo.vue';
import quotes from '@/data/quotes.js';
import images from '@/data/images.js';

const weekdays = ['MON', 'TUE', 'WEN', 'THY', 'FRI', 'SAT', 'SUN'];

const currentDate = reactive({ date: 0, month: 0, year: 0 });

const isInfoPopapVisible = ref(true);
const clickedDay = ref(null);

const getArrayObjectsItemByDatePropValue = (date, array) => {
  return array.find((item) => Number(item.date) === date);
};

const today = new Date();
currentDate.date = today.getDate();
currentDate.month = today.getMonth();
currentDate.year = today.getFullYear();

const getQtyOfDayLastMonth = computed(() => {
  return getStartDayOfMonth.value - 1;
});

const getQtyOfDayInPrevMonth = computed(() => {
  const year = currentDate.month === 0 ? currentDate.year - 1 : currentDate.year;
  const month = currentDate.month === 0 ? 12 : currentDate.month;

  return new Date(year, month, 0).getDate();
});

const getQtyOfDayLastMonthNotSee = computed(() => {
  return getQtyOfDayInPrevMonth.value + 1 - getStartDayOfMonth.value;
});

const getStartDayOfMonth = computed(() => {
  let firstDay = new Date(currentDate.year, currentDate.month, 1).getDay();
  if (firstDay === 0) firstDay = 7;
  return firstDay;
});

const getQtyOfDayCurMonth = computed(() => {
  return new Date(currentDate.year, currentDate.month + 1, 0).getDate();
});

const getNumberOfCurDay = computed(() => {
  return currentDate.date;
});

const getQtyOfDayNextMonth = computed(() => {
  return 43 - (getQtyOfDayCurMonth.value + getStartDayOfMonth.value);
});

const dayInfo = computed(() => {
  if (clickedDay.value === null) {
    return null;
  }
  return getArrayObjectsItemByDatePropValue(clickedDay.value, quotes);
});

const handleDayClick = (day) => {
  isInfoPopapVisible.value = !isInfoPopapVisible.value;
  clickedDay.value = day;
};

const isActiveDay = (day) => {
  const curDate = new Date();
  return (
    curDate.getDate() === day && curDate.getMonth() === currentDate.month && curDate.getFullYear() === currentDate.year
  );
};
</script>

<template>
  <div class="max-w-xl mx-auto">
    <div>
      <AppPopap @closePopap="handleDayClick" :isInfoPopapVisible="isInfoPopapVisible" class="w-20 fixed top-3 r-0 l-0">
        <DayInfo v-if="dayInfo" :day="dayInfo.date" :text="dayInfo.text" />
      </AppPopap>
    </div>

    <div class="mb-10 text-2xl text-center">Каждый день месяца будет открываться цитата дня.</div>

    <div class="mb-20 grid">
      <div class="justify-self-center">
        <div class="grid grid-cols-7 gap-2 px-2 py-4 text-white bg-gray-400">
          <div v-for="weekday in weekdays" class="flex justify-center items-center">
            {{ weekday }}
          </div>
        </div>

        <div class="date grid grid-cols-7 gap-2 px-2 py-2 justify-items-center">
          <div
            v-for="day in getQtyOfDayLastMonth"
            class="w-8 h-8 sm:w-12 sm:h-12 flex justify-center items-center text-gray-400"
          >
            {{ getQtyOfDayLastMonthNotSee + day }}
          </div>
          <div
            v-for="day in getQtyOfDayCurMonth"
            class="w-8 h-8 sm:w-12 sm:h-12 flex justify-center items-center rounded-3xl bg-cover"
            :class="[
              {
                disabled: day > getNumberOfCurDay,
                active: isActiveDay(day),
              },
            ]"
            :style="{ backgroundImage: `url(${images[day - 1]})` }"
          >
            <div v-if="day <= getNumberOfCurDay" @click="handleDayClick(day)" class="cursor-pointer">
              {{ day }}
            </div>
            <div v-else>
              {{ day }}
            </div>
          </div>

          <div
            v-for="day in getQtyOfDayNextMonth"
            class="w-8 h-8 sm:w-12 sm:h-12 flex justify-center items-center text-gray-400"
          >
            {{ day }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.date .active {
  background: rgb(249 235 167);
  color: black;
}

.date .disabled {
  opacity: 0.5;
}
</style>
