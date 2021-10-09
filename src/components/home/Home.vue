<template>
  <h1>Alphabetical Listing</h1>
  <div class="container-main">
    <div
      class="container-section"
      v-for="(seasonData, heading, index) in groupbyAlphabets"
      :key="index"
    >
      <h2 style="border-bottom:2px solid red;">{{ heading }}</h2>
      <EpisodeDesc :episodeLists="seasonData">
        <template v-slot:btn1>
          <button>Button 1</button>
        </template>
        <template v-slot:btn2>
          <button>Button 2</button>
        </template>
      </EpisodeDesc>
    </div>
  </div>
</template>

<script>
import data from "@/data.json";
import EpisodeDesc from "./EpisodeDesc.vue";
export default {
  components: { EpisodeDesc },
  name: "home",
  data() {
    return {
      // letters:['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z'],
      episodeLists: [],
    };
  },
  computed: {
    // groupbySeason() {
    //   let list = {};
    //   this.episodeLists.forEach((ele) => {
    //     if (Object.keys(list).includes(ele.season.toString())) {
    //       list[ele.season] = [...list[ele.season], ele];
    //     } else {
    //       list[ele.season] = [ele];
    //     }
    //   });
    //   console.log(list);
    //   return list;
    // },

    // alphabets(){

    //   return alphabets;
    // },

    groupbyAlphabets() {
      let list1 = {};
      let i = 65;
      let j = 91;
      let alphabets = [];
      for (let k = i; k < j; k++) {
        alphabets.push(String.fromCharCode(k));
      }
      console.log("new list||", alphabets);
      this.episodeLists.forEach((ele) => {
        let splitName = ele.name.split(" ");
        let e = splitName[1].split("");
        for (let c = 0; c < 26; c++) {
          if (alphabets[c] === e[0]) {
            if (Object.keys(list1).includes(alphabets[c])) {
              list1[alphabets[c]] = [...list1[alphabets[c]], ele];
              break;
            } else {
              list1[alphabets[c]] = [ele];
            }
          }
        }
      });
      // console.log("list items||", list1);
      list1=Object.entries(list1).sort((a, b) => {
        if (b > a) {
          return -1;
        } else if (b < a) {
          return 1;
        } else return 0;
      });
      // list1=Object.fromEntries(list1);
      // console.log("sorted items||", list1);
      return list1;
    },
  },
  created() {
    this.episodeLists = data && data._embedded && data._embedded.episodes;
    console.log("created||", this.episodeLists);
  },

  methods: {},
};
</script>

<style>
</style>