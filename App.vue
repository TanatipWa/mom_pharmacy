<template>
  <div id="app">
    <b>โปรแกรมคำนวณปริมาณยาน้ำพาราสำหรับเด็ก เพื่อคุณแม่</b><br />
    <p>
      ปกติยาน้ำเด็กเกือบทุกอย่างต้องคำนวณยาตามน้ำหนักตัวเด็ก<br />
      วิธีกินข้างขวด เป็นปริมาณสำหรับเด็กน้ำหนักตามเกณฑ์ แต่ถ้าเด็กผอม หรืออ้วน
      การกินตามข้างขวดอาจได้ยาเกินหรือยาน้อยเกิน
    </p>
    <br />

    <table border="0" align="center">
      <tr align="center">
        <td>น้ำหนักตัวเด็ก</td>
        <td><b-input type="text" v-model="weight" /></td>
        <td>กิโลกรัม (Kg.)</td>
      </tr>
      <tr align="center">
        <td>
          <br />ปริมาณยา ใน 5 มิลลิลิตร (ml.)<br />(ความแรงยาเท่าไรใน 1 ช้อนชา)
        </td>
        <td><br /><b-input type="text" v-model="mg_in_ml" /></td>
        <td>
          <br />มิลลิกรัม (mg.)<br />
          <b-button type="is-primary" @click="alert"> วิธีดูฉลากยา</b-button>
        </td>
      </tr>
      <tr align="center">
        <td colspan="3">
          <br />
          <b-button type="is-success" @click="calculate">คำนวณ</b-button>
          <b-button type="is-danger" @click="remove">ล้างข้อมูล</b-button
          ><br /><br />
          <div v-if="click == 1 && weight != 0 && mg_in_ml != 0">
            <h1>
              ดังนั้น จะป้อนยาลูกเพื่อลดไข้ได้ตั้งแต่ {{ cc_min }} -
              {{ cc_max }} มิลลิลิตร (ซีซี) ทุก 6 ชั่วโมง
            </h1>
          </div>
          <div v-else>
            <h1>ป้อนข้อมูลให้ถูกต้อง แล้วกดปุ่มคำนวณ</h1>
          </div>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      cc_min: 0,
      cc_max: 0,
      weight: 0,
      mg_in_ml: 0,
      click: 0,
    };
  },
  methods: {
    calculate: function() {
      this.cc_min =
        Math.round(((this.weight * 10 * 5) / (this.mg_in_ml * 1.0)) * 10) / 10;
      this.cc_max =
        Math.round(((this.weight * 15 * 5) / (this.mg_in_ml * 1.0)) * 10) / 10;
      this.click = 1;
    },
    remove: function() {
      this.c_min = 0;
      this.cc_max = 0;
      this.weight = 0;
      this.mg_in_ml = 0;
      this.click = 0;
    },
    alert() {
      this.$buefy.dialog.alert({
        title: "ดูได้จากกล่องหรือข้างขวดยา",
        message: "<img src='https://www.img.in.th/image/hygIcY'>",
        confirmText: "ตกลง",
      });
    },
  },
};
</script>

<style>
h1 {
  background: lightcyan;
}
</style>
