<template>
  <div class="container card">
    <form>
      <div class="alert alert-success">ກຳນົດເລກເຕັມຮູ</div>
      <div class="form-group row">
        <label for="roll_id" class="col-md-4 col-form-label">ເລກ 2 ໂຕ: <span style="color:red">[ {{expres.two}} ]</span></label>
        <div class="col-md-12">
          <input type="number" class="form-control" v-model="two" />
          
        </div>
        <label for="roll_id" class="col-md-4 col-form-label">ເລກ 3 ໂຕ: <span style="color:red">[ {{expres.three}} ]</span></label>
        <div class="col-md-12">
          <input type="number" class="form-control" v-model="three" />
          
        </div>
        <label for="roll_id" class="col-md-4 col-form-label">ເລກ 4 ໂຕ: <span style="color:red">[ {{expres.four}} ]</span></label>
        <div class="col-md-12">
          <input type="number" class="form-control" v-model="four" />
          
        </div>
        <label for="roll_id" class="col-md-4 col-form-label">ເລກ 5 ໂຕ: <span style="color:red">[ {{expres.five}} ]</span></label>
        <div class="col-md-12">
          <input type="number" class="form-control" v-model="five" />
          
        </div>
        <label for="roll_id" class="col-md-4 col-form-label">ເລກ 6 ໂຕ: <span style="color:red">[ {{expres.six}} ]</span></label>
        <div class="col-md-12">
          <input type="number" class="form-control" v-model="six" />
          
        </div>
        <label for="roll_id" class="col-md-4 col-form-label"></label>
        <div class="col-md-12">
          <button class="btn btn-success" @click.prevent="updatedata">
            ບັນທຶກ
          </button>
        </div>
      </div>
    </form>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      two: 0,
      three: 0,
      four: 0,
      five: 0,
      six: 0,
       expres:{
        two:0,
        three:0,
        four:0,
        five:0,
        six:0,
      }
    };
  },
   watch:{
    two(val){
      this.expres.two=this.formatNum(val);
    },
    three(val){
      this.expres.three=this.formatNum(val);
    },
    four(val){
      this.expres.four=this.formatNum(val);
    },
    five(val){
      this.expres.five=this.formatNum(val);
    },
    six(val){
      this.expres.six=this.formatNum(val);
    }
  },
  methods: {
    fetchsalelim() {
      axios
        .get("http://192.168.42.49:3001/getsalelimit")
        .then((res) => {
          this.two = res.data[0].two_digits;
          this.three = res.data[0].three_digits;
          this.four = res.data[0].four_digits;
          this.five = res.data[0].five_digits;
          this.six = res.data[0].six_digits;
        })
        .catch((err) => {
          alert(err);
        });
    },
    updatedata() {
      var r = confirm("ຕ້ອງການແກ້ໄຂຂໍ້ມູນ?");
      if (r === true) {
        axios
          .put("http://192.168.42.49:3001/updatesalelim/?id=" + 1, {
            two: this.two,
            three: this.three,
            four: this.four,
            five: this.five,
            six: this.six,
          })
          .then((res) => {
            alert(res.data);
          })
          .catch((er) => {
            alert("ເກີດຂໍ້ຜິດພາດ: " + er);
          });
      }
    },
    formatNum(val){
      return new Intl.NumberFormat().format(val);
      
    },
  },
  created() {
    this.fetchsalelim();
  },
};
</script>
<style scoped>
.card {
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  margin: 0.5rem auto;
  max-width: 40rem;
}
</style>