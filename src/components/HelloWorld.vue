<template>
  <div class="hello">
    <ul>
      <li :class="{'seen':notification.seen}" v-for="(notification, index) in notifications" v-bind:key="index">
        <div class="">
          <span @click="markAsSeen(index)" class="circle"></span>
          <span>{{notification.title}}</span>
          <span>{{notification.timestamp}}</span>
        </div>
        </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      notifications: [
        {
          title: "Be yourself; everyone else is already taken",
          seen: false,
          timestamp: 1591194180
        },
        {
          title: "Two things are infinite: the universe and human stupidity; and I'm not sure about the universe.",
          seen: false,
          timestamp: 1591105180
        },
        {
          title: "You only live once, but if you do it right, once is enough.",
          seen: false,
          timestamp: 1591203260
        },
        {
          title: "Be the change that you wish to see in the world.",
          seen: true,
          timestamp: 1591406020
        },
        {
          title: "No one can make you feel inferior without your consent.",
          seen: true,
          timestamp: 1591306020
        }
      ],
      dateObject: {
        day: 'numeric', 
        month: 'long', 
        year:'numeric', 
        hour:'numeric',
        minute:'numeric'
      }
    }
  },
  methods: {
    markAsSeen(index) {
      this.notifications[index].seen = true
    },
    sortNotifications: function(){
      this.notifications.sort(function(a,b){
        return b.timestamp - a.timestamp;
      })
    },
    unixToText() {
      for(var i = 0; i < this.notifications.length; i++) {
        this.notifications[i].timestamp = new Date(this.notifications[i].timestamp * 1000).toLocaleString("en-US", this.dateObject)
        }
      }
    },
    
    beforeMount() {
      this.sortNotifications();
      this.unixToText();
    }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
  list-style-type: none;
}
li {
  max-width: 1000px;
  text-align: left;
  margin: 0px auto;
  background: lightseagreen;
  line-height: 50px;
}
li.seen {
  background: grey;
}
span {
  vertical-align: middle;
  margin: 0px 10px;
}
.circle {
  height: 20px;
  width: 20px;
  border-radius: 50%;
  background: lime;
  display: inline-block;
  margin: 0px 10px;
}
</style>
