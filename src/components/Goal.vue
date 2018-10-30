<template v-if="goal.GoalGetterName">
  <!-- 0:1 player (62.) -->
   <li class="list-group-item">
     {{ goal.ScoreTeam1 }}:{{ goal.ScoreTeam2 }} {{ goal.GoalGetterName }} ({{ goal.MatchMinute }}.) {{zusatz}}</li>
</template>

<script>
export default {
  props: ['goal'],
  
  computed:{
    zusatz(){
      if(this.goal.IsOwnGoal){
        return `(ET)`;
      }
      else if(this.goal.IsPenalty){
        return `(E)`;
      }
    }
  }
}
</script>

<style scoped>

</style>
