<template>
  <q-page class="flex flex-center" >
    <div class="q-pa-md" >
      <div class="q-gutter-md" style="min-width: 500px;max-width: 500px" >
        <q-carousel
          v-model="slide"
          transition-prev="scale"
          transition-next="scale"
          swipeable
          animated
          control-color="blue"
          navigation
          padding
          arrows
          height="600px"
          class="bg-grey-12 text-black shadow-1 rounded-borders"
        >
          <q-carousel-slide name="q1" class="flex-center">
            <div class="q-mt-md text-center" >
              <label>Q1. 请问您来自哪个国家或地区？</label>
              <q-input v-model="q1" :dense="true"/>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q2" class="no-wrap flex-center">
            <div class="q-mt-md text-center" >
              <div style="margin: 0 auto;"><label>Q2. 请问您2019年是否到过中国旅游？ </label></div>
              <div style="margin: 0 auto;max-width:200px;" >
                <q-item tag="label" v-ripple>
                  <q-item-section avatar>
                    <q-radio v-model="q2" val=1 color="teal" />
                  </q-item-section>
                  <q-item-section>
                    <q-item-label>1. 是</q-item-label>
                  </q-item-section>
                </q-item>

                <q-item tag="label" v-ripple>
                  <q-item-section avatar>
                    <q-radio v-model="q2" val=2 color="teal" />
                  </q-item-section>
                  <q-item-section>
                    <q-item-label>2. 否</q-item-label>
                  </q-item-section>
                </q-item>
              </div>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q3" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q3. 请问您这次是参加旅行团还是自己旅游？ </label>
            </div>
          </q-carousel-slide>
          <q-carousel-slide name="q4" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q4.您是第一次到中国来旅游吗？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q5" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q5.是第几次呢？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q6" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q6.请问您来华旅游的主要目的是? </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q7" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q7.请问您来中国主要接触了哪些景点、活动或风土人情？ 【选择最主要的1-3个】 </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q8" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q8.您这次旅游是和谁一起出来玩的？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q9" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q9.您这次出游前主要通过哪些渠道了解有关信息？【最多选三项】 </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q10" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q10.您这次出游前主要查找了哪些方面的信息？【最多选三项】 </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q11" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q11.您这次出游前在电视上看到过中国的旅游形象广告或专题片吗？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q12" class=" no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q12.是哪个城市（景区）呢？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q13" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q13.您选择一地作为目的地出行，下列因素哪些对您影响较大？【最多选三项】 </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q14" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q14.您这次旅游时人均花费是多少钱？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q15" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q15.您这次旅游花费最多的项目是？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q16" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q16.您这次旅游时参观了几个景点？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q17" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q17. 您这次旅游途经了哪些国家（地区）？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q18" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q18. 您这次在华旅游线路包含了哪些城市（景区）？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q19" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q19.您这次旅游了多长时间？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q20" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q20.您这次旅游时住在什么地方？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q21" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q21.您这次旅游时购买了保险吗？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q22" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q22.您购买了以下哪几种保险？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q23" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q23.在此次旅遊之前，您對以下城市的印象如何？（城市旅遊形象）？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q24" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q24.来这里旅游前，您对目的地的整体形象评价如何？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q25" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q25.在此次旅游之前，您对此次旅游的期望有多高？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q26" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q26.您对此次出游的定位如何评价？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q27" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q27.您对当地的总体评价如何？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q28" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q28.您对城市管理的满意程度如何？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q29" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q29.您对公共行业服务的满意程度如何？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q30" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q30.您对当地窗口服务具体评价如何？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q31" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q31.您对此次出游的总体评价如何？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q32" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q32.您旅途过程中有抱怨或投诉吗？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q33" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q33.投诉处理满意程度？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q34" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q34.您对中国有再游一次的想法吗？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q35" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q35. 您对目的地在旅游建设与旅游服务方面主要意见和建议是什么？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q36" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q36.您在2020 or 2021年有旅行计划吗？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q37" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q37.准备去那些地方旅行呢？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q38" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q38.如果您现在或将来准备前往中国，那您会为了什么来到中国呢？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q39" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q2. 请问您2019年是否到过中国旅游？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q40" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q2. 请问您2019年是否到过中国旅游？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q41" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q2. 请问您2019年是否到过中国旅游？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q42" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q2. 请问您2019年是否到过中国旅游？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q43" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q2. 请问您2019年是否到过中国旅游？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q44" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q2. 请问您2019年是否到过中国旅游？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q45" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q2. 请问您2019年是否到过中国旅游？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q46" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q2. 请问您2019年是否到过中国旅游？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q47" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q2. 请问您2019年是否到过中国旅游？ </label>
            </div>
          </q-carousel-slide>

          <q-carousel-slide name="q48" class="column no-wrap flex-center">
            <div class="q-mt-md text-center">
              <label>Q2. 请问您2019年是否到过中国旅游？ </label>
            </div>
          </q-carousel-slide>
        </q-carousel>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      slide: 'q1',
      q1: '',
      q2: '',
      lorem: 'I love you'
    }
  }
}
</script>
