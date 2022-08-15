<template>
  <!-- Country Details (Bootstrap column) -->
  <div class="col-7">
    <img
      src="https://www.pngall.com/wp-content/uploads/2016/05/Vietnam-Flag-PNG-Picture.png"
      alt="country flag"
      style="width: 300px"
    />
    <h1>{{ nameCountry }}</h1>
    <table class="table">
      <thead></thead>
      <tbody>
        <tr>
          <td style="width: 30%">Capital</td>
          <td>{{ capital }}</td>
        </tr>
        <tr>
          <td>Area</td>
          <td>{{ area }}<sup>2</sup></td>
        </tr>
        <tr>
          <td>Borders</td>
          <td>
            <ul>
              {{
                borderList
              }}
            </ul>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      image: "",
      nameCountry: "Vietnam",
      capital: "Hanoi",
      area: "	331.690 km²",
      borderList: "China",
    };
  },
};
</script>

<style></style>
