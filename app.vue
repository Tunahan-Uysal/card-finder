<template>
  <div class="container-xl">
    <header class="w-[100wv] bg-blue-500 h-24 m-8">
          <h2 class="text-4xl pt-6 pl-8 font-bold text-gray-50 w-max">Lorem Ipsum Dolor Sit <span class="bg-gray-50 text-blue-500 px-2">Amet</span></h2>
    </header>
    <main class="flex flex-row">
        <div class="basis-5/12 bg-slate-200 m-2 ml-8 w-max pb-6">
          <div class="w-100 bg-slate-300 h-16">
            <h2 class="text-2xl font-bold text-gray-800 font-sans ml-6 pt-3">Credit Card Benefits</h2>
          </div>
          
          <!-- Sliders -->
          <template v-for="sliders in SliderValues" :key="sliders.id">
          <h3 class="text-xl font-semibold font-sans mt-6 ml-6"> {{ sliders.name }}</h3>
          <div class="w-100 flex justify-center items-start">
            <input type="range" name="rangebonus" id="bonusrange" min="0" max="2" class="w-[91%] pt-6  accent-slate-600" v-model="sliders.value">
          </div>
          <div class="flex flex-row mx-6 text-lgs font-thin text-gray-700">
            <h4 class="basis-1/3">Min</h4>
            <h4 class="basis-1/3 text-center">Med</h4>
            <h4 class="basis-1/3 text-end">Max</h4>
          </div>
          </template>
        </div>
      <!-- Credit Cards -->
        <ul class="basis-7/12 m-2 mr-8 w-max h-64 flex flex-col">
          <li v-for="card in AmExCards" :key="card.id" class="flex flex-row">
            <div class="basis-5/12">
              <img :src="card.image" alt="" srcset="" class="w-[288px] ml-2 mt-8">
            </div>
            <div class="basis-7/12 text-center mt-16">
                <h3 class="font-bold text-gray-800 text-lg"> {{ card.name }}</h3>
                <div class="flex flex-row justify-evenly mt-16">
                    <button type="button" class="border border-blue-600 text-green-500 w-40 h-10 mr-4">Info</button>
                    <button type="button" class="border bg-blue-600 w-40 text-white underline h-10 ml-4">Purchase</button>
                </div>
            </div>
          </li>
        </ul>
    </main>
  </div>
</template>

<script>
import AmExImg from "./src/AmericanExpressPlatinum.png"

export default {
  data() {
    return {
      AmExCards: [
        {id: 1, name: 'American Express Platinum', image: AmExImg},
        {id: 2, name: 'American Express Premium', image: AmExImg},
        {id: 3, name: 'American Express Basic', image: AmExImg},
        {id: 4, name: 'American Express Gold', image: AmExImg},
      ],
      SliderValues: [
        {id: 1, name: 'Bonuses and Offers', value: 0},
        {id: 2, name: 'Events and Programs', value: 0},
        {id: 3, name: 'Insurance and Protection', value: 0},
        {id: 4, name: 'Travel and Mobility', value: 0},
        {id: 5, name: 'Interest and Contributions', value: 0},
      ],
      minVal: 0,
      maxVal: 2,
    }
  },
  watch: {
    SliderValues: {
      handler(newValues) {
        newValues.forEach((SliderValues) => {
          this.getProgress(SliderValues.value);
        });
      },
      deep: true
    }
  },
  methods: {
    logSliderValues() {
      this.SliderValues.forEach(slider => {
        console.log(slider.value);
      });
    },
    getProgress(currentVal) {
      const resultValue = ((currentVal - this.minVal) / (this.maxVal - this.minVal)) * 100;
      console.log(resultValue);
      return resultValue;
    }
  }
}
</script>