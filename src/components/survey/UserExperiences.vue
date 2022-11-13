<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click="loadSubmittedExperiance">Load Submitted Experiences</base-button>
      </div>
      <ul>
        <survey-result
          v-for="result in results"
          :key="result.id"
          :name="result.name"
          :rating="result.rating"
        ></survey-result>
      </ul>
    </base-card>
  </section>
</template>

<script>
import { response } from 'express';
import SurveyResult from './SurveyResult.vue';

export default {
  props: ['results'],
  components: {
    SurveyResult,
  },
  data(){
    return {
      results:[],
    };
  },
  methods:{
    loadSubmittedExperiance(){
      
      fetch('https://vue-http-request-135bc-default-rtdb.asia-southeast1.firebasedatabase.app/survey.json').then((response) => {
        if(response.ok){
          return response.json();
        }
      }).then(function (data){
        const results =[];
        for (const id in data){
          results.push({
            id:id,
            name:data[id].name,
            rating:data[id].rating,
          })
        }
      })
    }
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>