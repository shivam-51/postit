<template>
  <div style="overflow: hidden">
    <div>
      <h1 class="heading">Notice Board</h1>
    </div>
    <div class="twitter-wrap">
      <div class="sidebar-container">
        <ul class="sidebar-navigation">
          <li>
            <b-button @click.prevent="general">General Notice</b-button>
          </li>
          <li>
            <b-button @click.prevent="first">First Year Notices</b-button>
          </li>
          <li>
            <b-button @click.prevent="second">Second Year Notices</b-button>
          </li>
          <li>
            <b-button @click.prevent="third">Third Year Notices</b-button>
          </li>
          <li>
            <b-button @click.prevent="fourth">Fourth Year Notices</b-button>
          </li>
        </ul>
        <select v-model="kind" class="content">
          <option value="general_notice">General</option>
          <option value="first_notice">First</option>
          <option value="second_notice">Second</option>
          <option value="third_notice">Third</option>
          <option value="fourth_notice">Fourth</option>
        </select>
      </div>

      <div class="side-main" style="margin-top:20px">
        <div>
          <ul v-if="noticearr.length !== 0">
            <li v-for="not in noticearr" :key="not.id" style="padding:10px">
              <div style="float:left">
                <span style="color:blue"
                  ><medium
                    ><strong>{{ not.user + "  " }}</strong></medium
                  ></span
                >
                <span style="color:transparent">|</span>
                <i
                  class="far fa-calendar-alt"
                  style="font-size:11px;color:black"
                ></i>
                <span style="color:transparent">|</span>
              </div>
              <div style="margin:0px">
                <span style="color:black"
                  ><small>{{ not.timestamp }}</small></span
                >
              </div>
              <div style="text-align:left;clear:both">
                <div class="title">
                  <span style="margin-top:5px;"
                    ><b style="font-size:22px;"> {{ not.title }}</b></span
                  >
                </div>
                <iframe
                  v-bind:src="not.image"
                  onload='javascript:(function(o){o.style.height=o.contentWindow.document.body.scrollHeight+"px";}(this));'
                  style="height:600px;width:100%;border:none;overflow:hidden; "
                ></iframe>
              </div>
            </li>
          </ul>

          <ul v-else>
            <li>There is no notice at present right now</li>
          </ul>
        </div>
      </div>
      <div class="side-main center">
        <div class="fixed-btn ml-auto">
          <router-link
            v-show="kind == 'general_notice'"
            to="/addnotice/general_notice"
            ><i class="fas fa-plus fa-sm"></i
          ></router-link>
          <router-link
            v-show="kind == 'first_notice'"
            to="/addnotice/first_notice"
            ><i class="fas fa-plus fa-sm"></i
          ></router-link>
          <router-link
            v-show="kind == 'second_notice'"
            to="/addnotice/second_notice"
            ><i class="fas fa-plus fa-sm"></i
          ></router-link>
          <router-link
            v-show="kind == 'third_notice'"
            to="/addnotice/third_notice"
            ><i class="fas fa-plus fa-sm"></i
          ></router-link>
          <router-link
            v-show="kind == 'fourth_notice'"
            to="/addnotice/fourth_notice"
            ><i class="fas fa-plus fa-sm"></i
          ></router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import app from "firebase/app";
import "firebase/firestore";
export default {
  //   name: "AllNotice",
  data() {
    return {
      noticearr: [],
      kind: "general_notice"
    };
  },
  created() {
    this.fetchnotice();
  },
  methods: {
    async fetchnotice() {
      console.log("Entering");
      const db = app.firestore();
      db.collection(this.kind)
        .orderBy("timestamp", "desc")
        .onSnapshot(querySnapshot => {
          let allnotice = [];
          querySnapshot.forEach(doc => {
            allnotice.push(doc.data());
          });

          this.noticearr = allnotice;
        });
    },
    general() {
      this.kind = "general_notice";
      this.fetchnotice();
    },
    first() {
      this.kind = "first_notice";
      this.fetchnotice();
    },
    second() {
      this.kind = "second_notice";
      this.fetchnotice();
    },
    third() {
      this.kind = "third_notice";
      this.fetchnotice();
    },
    fourth() {
      this.kind = "fourth_notice";
      this.fetchnotice();
    }
  }
};
</script>
>

<style scoped>
.twitter-wrap {
  display: grid;
  grid-template-columns: 20% 60% 20%;
  /* position: relative; */
}
.heading {
  background-image: url("../assets/walpaper.jpg");
  background-size: 40rem;
  margin: auto;
  margin-top: 20px;
  width: 90%;
  max-width: 40rem;
  padding: 15px;
  border-radius: 10px;
  color: whitesmoke;
  text-align: center;
}
.heading1 {
  text-shadow: 0px 1px 2px;
  padding: 3px;
}
.center {
  /* height: 500px; */
  display: flex;
  align-items: center;
  justify-content: center;
}
.btn-secondary {
  width: 150px;
  margin-bottom: 20px;
}

.fixed-btn {
  position: fixed;
  height: 80px;
  text-shadow: 1px 1px 1px #ccc;
  text-shadow: 0 0 9px #000;
  right: 3%;
  top: 12%;
  cursor: pointer;
  display: flex;
  width: 5vw;
  height: 5vw;
  font-size: 4rem;
  border-radius: 25vw;
  overflow: hidden;
  background-size: cover;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  border: 6px solid #ffe14d;
  /* box-shadow: 0 1px 10px rgba(0, 0, 0, 0.46); */
  opacity: 0.8;
  transition: background 0.5s, color 1s, opacity 0.5s, border 0.5s;
}
.sidebar-container {
  /* display: flex; */
  align-items: center;
  justify-content: center;
  /* position: fixed; */
  max-width: 320px;
  height: 100%;
  left: 0;
  overflow-x: hidden;
  overflow-y: auto;
  background: #fff;
  color: #fff;
}

.content-container {
  padding-top: 20px;
}
.drop {
  text-align: center;
  /* float:left; */
}
.sidebar-logo {
  padding: 10px 15px 10px 30px;
  font-size: 20px;
  background-color: #2574a9;
}

.sidebar-navigation {
  padding: 50px;
  margin-top: 150px;
  margin-bottom: 150px;
  list-style-type: none;
  position: relative;
}

.sidebar-navigation li {
  background-color: transparent;
  position: relative;
  display: inline-block;
  line-height: 20px;
}

.sidebar-navigation li a {
  padding: 10px 15px 10px 30px;
  display: block;
  color: #fff;
}

.sidebar-navigation li .fa {
  margin-right: 10px;
}

.sidebar-navigation li a:active,
.sidebar-navigation li a:hover,
.sidebar-navigation li a:focus {
  text-decoration: none;
  outline: none;
}

.sidebar-navigation li::before {
  background-color: #2574a9;
  position: absolute;
  content: "";
  height: 100%;
  left: 0;
  top: 0;
  -webkit-transition: width 0.2s ease-in;
  transition: width 0.2s ease-in;
  width: 3px;
  z-index: -1;
}
.sidebar-container select {
  display: none;
}

.content {
  position: absolute;
  background-color: #f9f9f9;
  /* min-width: 160px; */
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  padding: 12px 16px;
  overflow: none;
  z-index: 1;
  text-align: center;
}
.sidebar-navigation .header {
  font-size: 12px;
  text-transform: uppercase;
  background-color: #151515;
  padding: 10px 15px 10px 30px;
}

.sidebar-navigation .header::before {
  background-color: transparent;
}

.content-container {
  padding-left: 220px;
}
@media (max-width: 1024px) {
  .sidebar-container ul {
    display: none;
  }
  .sidebar-container select {
    display: inline-block;
    margin-left: 1rem;
  }
}
@media (max-width: 640px) {
  .sidebar-container ul {
    display: none;
  }
  .sidebar-container select {
    display: inline-block;
    margin-left: 0.5rem;
    width: 100px;
    text-align: center;
  }
  h1 {
    font-size: 32px;
  }
  .content {
    font-size: smaller;
    /* text-align: center; */
  }
  .side-main {
    margin-top: 3rem;
  }
  .fixed-btn {
    height: 1vw;
    width: 1vw;
  }
}
</style>
