<template>
  <div class="ecosystem">
    <h2>Ecosistema</h2>
    <div class="member-cards__wrapper">
        <div class="member-card" v-for="(member, index) in membersList" :key="index">
          <img 
          class="member-card__image"
          :src="member.profilePicture"
          :alt="`Profile_picture_${index + 1}`"
          >
          <div class="member-card__text-wrapper">
            <h4 class="member-card__name"> 
              {{ member.name }}
            </h4>
            <h4 class="member-card__position"> 
              {{ member.position }}
            </h4>
          </div>
        </div>
    </div>
  </div>
</template>

<script>
  import memberInfoList from './member-list.json';

  export default {
    name: "ecosystem-section",
    data() { 
      return {
        membersList: memberInfoList
      };
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>