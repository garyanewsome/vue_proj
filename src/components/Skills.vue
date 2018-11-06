<template>
  <div class="container">
    <form @submit.prevent="addSkill">
      <input type="text" placeholder="Enter a skill you have.." v-model="skill" v-validate="'min:5'" name="skill">
<!--       <transition name="alert-in">
        <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
      </transition> -->
      <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
        <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
      </transition>
    </form>
    <div class="holder">
      <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li v-for="(skill, index) in skills" :key='index'>{{index}}. {{skill.skill}}
            <i class="fa fa-minus-circle right" v-on:click="remove(index)"></i>
          </li>
        </transition-group>
      </ul>
      <p>These are the skills that you possess.</p>

    </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data() {
    return {
      checked: false,
      skill: '',
      skills: [
        { "skill": "Vue.js" },
        { "skill": "Frontend Developer" }
      ]
    }
  },
  methods: {
    addSkill () {
      this.$validator.validateAll().then((result) => {
        if (result) {
          this.skills.push({skill: this.skill})
          this.skill = ''
        } else {
          // eslint-disable-next-line
          console.log('Invalid input 😔')
        }
      })
    },
    remove(id) {
      this.skills.splice(id, 1)
    }
  }
}
</script>

<style src="../assets/css/skills.css" scoped></style>
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";

.alert {
  background: #fdf2ce;
  font-weight: bold;
  display: inline-block;
  padding: 5px;
  margin-top: -20px;
  margin-bottom: 0;
}
.alert-in-enter-active {
  animation: bounce-in .5s;
}
.alert-in-leave-active {
  animation: bounce-in .5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
.right { float: right; }
</style>
