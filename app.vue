<template>
  <div @keyup.esc="infoOn = false" class="container-xl">
    <header class="w-[100wv] bg-blue-500 h-24 m-8">
          <h2 class="text-4xl pt-6 pl-8 font-bold text-gray-50 w-max">Lorem Ipsum Dolor Sit <span class="bg-gray-50 text-blue-500 px-2">Amet</span></h2>
    </header>
    <main class="flex flex-row">
        <div :class="infoOn ? 'opacity-0' : 'visible'" class="basis-5/12 bg-slate-200 m-2 ml-8 w-max pb-6 transition-opacity duration-600">
          <div class="w-100 bg-slate-300 h-16">
            <h2 class="text-2xl font-bold text-gray-800 font-sans ml-6 pt-3">Credit Card Benefits</h2>
          </div>
          
          <!-- Sliders -->
          <template v-for="sliders in SliderValues" :key="sliders.id">
          <h3 class="text-xl font-semibold font-sans mt-6 ml-6"> {{ sliders.name }}</h3>
          <div class="w-100 flex justify-center items-start">
            <input type="range" name="rangebonus" id="bonusrange" :min="this.minVal" :max="this.maxVal" class="w-[91%] pt-6  accent-slate-600" v-model="sliders.value">
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
          <li v-for="(card, index) in AmExCards" :key="index" class="flex flex-row">
            <div class="basis-5/12">
              <span class="rounded-full w-6 h-6 absolute bg-blue-600 text-center text-white font-mono font-bold"> {{ index + 1 }}</span>
              <img :src="card.image" alt="" srcset="" class="w-[288px] ml-2 mt-8">
            </div>
            <div class="basis-7/12 text-center mt-8">
                <h3 class="font-bold text-gray-800 text-lg px-32 mt-5"> {{ card.name }}</h3>
                <div class="flex flex-row justify-evenly mt-16">
                    <button @keyup.esc="infoOn = false" @click="infoOn = !infoOn, buttonId = index" type="button" class="border border-blue-600 text-green-500 w-40 h-10 mr-4">Matches {{ Math.round(card.score) }}%</button>
                    <button type="button" class="border bg-blue-600 w-40 text-white underline h-10 ml-4">Purchase</button>
                </div>
            </div>
            <hr v-if="card.value < 50">
          </li>
        </ul>
        
        <div @keyup.esc="infoOn = false" :class="infoOn ? '-translate-x-0' : '-translate-x-[200%]'" class="order-first absolute top-[10.5rem] left-8 w-[39.2%] h-[125%] overflow-auto transition-transform duration-500 bg-gray-200">
          <h2 class="text-green-700 text-2xl ml-6 mt-4 font-medium mb-6">Matches {{ Math.round(AmExCards[buttonId].score) }}% to your Preferences!</h2>
          <div class="flex flex-row">
            <div class="basis-[55%]">
               <img :src="AmExCards[buttonId].image" alt="" class="w-56 bg-slate-300 h-36 ml-6 mt-6">
            </div>
            <div class="basis-[45%] flex flex-col">
              <h2 class="font-bold text-gray-800 text-2xl">Lorem Ipsum</h2>
              <h3 class="" style="font-size: 12px;"><span class="font-bold text-base">{{ AmExCards[buttonId].cost }} Euros </span>Annually</h3>
              <div class="flex flex-row">
                <h3 class="font-bold basis-5/12" style="font-size: 12px;">Bonus Programs:</h3>
                <ul>
                  <li v-for="(card, index) in AmExCards[buttonId].CardBonusInfo" class="text-gray-500 text-left" style="font-size: 12px;">{{ card }}</li>
                </ul>
              </div>
              <div class="flex flex-row">
                <h3 class="font-bold basis-5/12" style="font-size: 12px;">Reserve Cards:</h3>
                <ul>
                  <li v-for="(card, index) in AmExCards[buttonId].CardReserve"  class="text-gray-500 text-left" style="font-size: 12px;">{{ card }}</li>
                </ul>
              </div>
              <div class="flex flex-row">
                <h3 class="font-bold mr-3" style="font-size: 12px;">Material:</h3>
                <ul>
                  <li v-for="(card, index) in AmExCards[buttonId].CardProperties" class="text-gray-500 text-left" style="font-size: 12px;">{{ card }}</li>
                </ul>
              </div>
            </div>
          </div>
          <div class="flex mt-12">
            <div class="pl-8 flex flex-col border-r-gray-400 border-r-2 basis-3/8 px-2">
              <h2 class="text-gray-800 font-semibold leading-4 mb-2">Status Upgrades and More</h2>
              <ul>
                <li v-for="(info, index) in AmExCards[0].CardUpgradeInfo" :key="index" class="text-center text-gray-500 mb-2" style="font-size: 12px">
                  {{ info }}
                </li>
              </ul>
            </div>
            <div class="flex flex-col border-r-gray-400 border-r-2 basis-2/8 px-2">
              <h2 class="text-gray-800 font-semibold leading-4 mb-2">Bonus Programs and Benefits</h2> 
              <ul>
                <li v-for="(info, index) in AmExCards[0].CardBonusInfo" :key="index" class="text-center text-gray-500 mb-2" style="font-size: 12px">
                  {{ info }}
                </li>
              </ul>
            </div>
            <div class="pr-8 flex flex-col basis-3/8 px-2">
              <h2 class="text-gray-800 font-semibold leading-4 mb-2">Insurance and Protection</h2>
              <ul>
                <li v-for="(info, index) in AmExCards[0].CardInsuranceInfo" :key="index" class="text-center text-gray-500 mb-2" style="font-size: 12px">
                  {{ info }}
                </li> 
              </ul>
            </div>
          </div>
          <div class="mt-24">
            <ol class="list-decimal px-8 font-thin text-gray-600">
              <li>The complete terms and conditions and participating partners can be found <a href="#" class="text-blue-500">here</a>.</li><br>
              <li>All details about the services and insurance can be found <a href="#" class="text-blue-500">here</a>.</li><br>
              <li>For more information, refer to the price and performance list <a href="#" class="text-blue-500">here</a>.</li>
              <li>The value of the additional cards will not be paid out or credited to the card account if the additional card is not used. For detailed information on protection and security, see <a href="#" class="text-blue-500">here</a>. Google Pay is a trademark of Google LLC. Apple Pay is a registered trademark of Apple Inc. All rights reserved. American Express Europe S.A. (Germany branch), Theodor-Heuss-Allee 112, 60486 Frankfurt am Main, Registergericht Frankfurt am Main, HRB 112342. The conditions of the American Express website rules and regulations apply.</li><br>
            </ol>
          </div>
        </div>
    </main> 
  </div>
</template>

<script>
import AmExPlatImg from "./src/AmericanExpressPlatinum.png"
import AmExGoldImg from "./src/AmericanExpressGold.jpg"
import AmExCorpImg from "./src/AmericanExpressCorporate.jpg"
import AmExRewImg from "./src/AmericanExpressRewards.jpg"

import { ref, onMounted, watch } from 'vue'

export default {
  setup() {
    const AmExCards = ref([
      {id: 1, rank: 1, name: 'American Express Platinum', image: AmExPlatImg, bonuses: 50, programs: 0, insurance: 100, travel: 80, interest: 10, price: -50, privacy : 100, score: 0, CardUpgradeInfo: ["Connect your account with other Cards", "Ability to Access your account offline", "Free Valet Parking in Popular Destinations", "Over 1200 VIP Lounges that can be accesses for free", "Free 200 Euros on Sign-up"], CardBonusInfo: ["Free Flight Points w/ Turkish Airlines and Air France", "Personal Military Grade AI Secretary", "Unlimited Capacity"], CardInsuranceInfo: ["80% Coverage, No matter the fee or situation", "Easy & Cheap Life Insurance Plan", "Special Deals with our Sponsors", "Presidential-level Healthcare & Therapy", "Easy Access to the Best Lawyers"], CardReserve: ["Backup Cards up to Three & Quick card cancelling", "Exclusive, to you", "Military-Grade Encoding techniques"], CardProperties: ["Gold", "Silver", "Hand-Made", "Metal",], cost: "695"},
      {id: 2, rank: 2, name: 'American Express Corporate', image: AmExCorpImg, bonuses: 100, programs: 30, insurance: 75, travel: 40, interest: 20, price: 35, privacy : 20, score: 0, CardUpgradeInfo: ["Connect your account with other Cards", "Ability to Access your account offline", "Easy Money Transfers & Automatic Annual Payments", "Over 1200 VIP Lounges that can be accesses for free", "Easy access to Employee Pays"], CardBonusInfo: ["Free Flight Points w/ Turkish Airlines and Air France", "Easy Secretary Access & Revenue Algorithms", "Self-limited Capacity to prevent Phishing", "Priority Pass on every East Coast Airliner & French Airliner"], CardInsuranceInfo: ["50% Coverage, No matter the fee or situation", "Bank Funded Insurence Plans for every Employee", "Special Deals with our Sponsors", "Anti-Scam Algorithms", "Easy Access to the Best Lawyers"], CardReserve: ["Backup Cards up to Three & Quick card cancelling", "Great for Companies", "Military-Grade Encoding techniques"], CardProperties: ["Plastic", "Silver", "Metal",], cost: "325"},
      {id: 3, rank: 3, name: 'American Express Rewards', image: AmExRewImg, bonuses: 0, programs: 100, insurance: 50, travel: -25, interest: 100, price: 100, privacy : -50, score: 0, CardUpgradeInfo: ["Connect your account with other Cards", "Ability to Access your account offline"], CardBonusInfo: ["80,000 Euro Capacity", "Gain 15% from each UberEats order", "50 Euro Sign-up bonus"], CardInsuranceInfo: ["Annually Fund Insurence, for Cheap", "Life Insurence provided to Loyal Customers"], CardReserve: ["Create an Alternative Account for family members and friends"], CardProperties: ["Plastic"], cost: "30"},
      {id: 4, rank: 4, name: 'American Express Gold', image: AmExGoldImg, bonuses: 60, programs: 60, insurance: -25, travel: 80, interest: 50, price: 50, privacy : 20, score: 0, CardUpgradeInfo: ["Connect your account with other Cards", "Ability to Access your account offline", "Easy Money Transfers"], CardBonusInfo: ["Free Flight Points w/ Turkish Airlines and Air France", "Gain 10% from Vacation Fees","1,000,000 Euro Capacity"], CardInsuranceInfo: ["Easy access to Lawyers"], CardReserve: ["Backup Cards up to Three & Quick card cancelling"], CardProperties: ["Gold", "Silver", "Metal", "Painted"], cost: "135"},
    ]);
    const SliderValues = ref([
      {id: 1, name: 'Bonuses and Offers', value: 0},
      {id: 2, name: 'Events and Programs', value: 0},
      {id: 3, name: 'Insurance and Protection', value: 0},
      {id: 4, name: 'Travel and Mobility', value: 0},
      {id: 5, name: 'Interest and Contributions', value: 0},
      {id: 6, name: 'Price and Upkeep', value: 0},
      {id: 7, name: 'Privacy and Exclusivity', value: 0},
    ]);
    const minVal = ref(0);
    const maxVal = ref(2);
    const infoOn = ref(false);
    const buttonId = ref(0);
    const getIndex = ref(0);
    const statusUpgrades = ref([]);

    watch(SliderValues, (newValues) => {
      newValues.forEach((SliderValues) => { 
        getProgress(SliderValues.value);
        calculateScore();  
      });
    }, {deep: true});

    const logSliderValues = () => {
      SliderValues.value.forEach(slider => {
        console.log(slider.value);
      });
    };
    const getProgress = (currentVal) => {
      const resultValue = currentVal; /*((currentVal - this.minVal) / (this.maxVal - this.minVal)) * 100;*/
      console.log(resultValue);
      return resultValue;
    };
     const calculateScore = () => {
      AmExCards.value.forEach(card => {
        let bonusScore, programScore, insuranceScore, travelScore, interestScore, priceScore, privacyScore = 0;

        bonusScore = SliderValues.value[0].value * card.bonuses;
        programScore = SliderValues.value[1].value * card.programs;
        insuranceScore = SliderValues.value[2].value * card.insurance;
        travelScore = SliderValues.value[3].value * card.travel;
        interestScore = SliderValues.value[4].value * card.interest;
        priceScore = SliderValues.value[5].value * card.price;
        privacyScore = SliderValues.value[6].value * card.privacy;

        let totalScore = 0;

        totalScore = (bonusScore+programScore+insuranceScore+privacyScore+travelScore+interestScore+priceScore) / 6;

        totalScore = Math.max(0, Math.min(100, totalScore))
        card.score = totalScore;

        AmExCards.value.sort((a, b) => b.score - a.score);
        console.log(AmExCards.value[0].name);
       
      });

      onMounted(() => {
        statusUpgrades.value = AmExCards.value[0].statusUpgrades;
      });
    };
    return {
        AmExCards,
        SliderValues,
        minVal,
        maxVal,
        infoOn,
        buttonId,
        statusUpgrades,
    };
  },
}
</script>
