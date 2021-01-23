<template>
  <table id="tblUsers">
    <thead>
    <tr>
        <th>Shop Name</th>
        <th>Shop Address</th>
        <th>Shop Zip</th>
        <th>Shop Style</th>
        <th>Piercing Services?</th>
    </tr>
    </thead>
    <tbody>
      <tr>
        <td><input type="text" id="shopNameFilter" v-model="filter.shopName"/></td>
        <td><input type="text" id="addressFilter" v-model="filter.shopAddress"/></td>
        <td><input type="text" id="zipFilter" v-model="filter.shopZip"/></td>
        <td><input type="text" id="styleFilter" v-model ="filter.shopStyle"/></td>
        <td>
          <select id="statusFilter" v-model="filter.anyPiercings">
            <option value="">Show All</option>
            <option value="Active">Yes</option>
            <option value="Disabled">No</option>
          </select>
        </td>
      </tr>
      <!-- user listing goes here -->
    <tr v-for="shop in filteredList" v-bind:key="shop.id"> 
      <td> {{shop.shopName}}</td>
      <td> {{shop.shopAddress}}</td>
      <td> {{shop.shopZip}} </td>
      <td> {{shop.shopStyle}} </td>
      <td> {{shop.anyPiercings}}</td>
     </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'shop-list',
  data() {
    return {
      filter: {
        shopName: "",
        shopAddress: "",
        shopZip: "",
        shopStyle: "",
        anyPiercings: ""
      },

      shops: [
          {shopName: "Goodkind Tattoo", shopAddress: "3056 N. Clybourn Ave. Unit C", shopZip: "60618", shopStyle: "Both", anyPiercings: 'No'},
          {shopName: "Deluxe Tattoo", shopAddress: "1459 W. Irving Park Ave.", shopZip: "60618", shopStyle: "Both", anyPiercings: 'No'},
          {shopName: "Taylor Street Tattoo", shopAddress: "1150 W. Taylor St.", shopZip: "60607", shopStyle: "Traditional", anyPiercings: 'No'},
          {shopName: "Family Tattoo", shopAddress: "2125 W. Belmont Ave.", shopZip: "60618", shopStyle: "Neotraditional", anyPiercings: 'No'},
          {shopName: "Great Lakes Tattoo", shopAddress: "1148 W. Grand Ave.", shopZip: "", shopStyle: "Neotraditional", anyPiercings: 'No'},
          {shopName: "Fudo Tattoo", shopAddress: "5612 N. Western Ave.", shopZip: "60659", shopStyle: "Traditional", anyPiercings: 'No'},
          {shopName: "Time Being", shopAddress: "2409 W. Hirsch St.", shopZip: "60622", shopStyle: "Both", anyPiercings: 'No'},
          {shopName: "Good Omen", shopAddress: "2009 W. Belmont Ave. Ste. 1", shopZip: "60618", shopStyle: "Neotraditional", anyPiercings: 'No'},
          {shopName: "Chicago Tattoo & Piercing Co.", shopAddress: "1017 W. Belmont Ave.", shopZip: "60657", shopStyle: "Both", anyPiercings: 'Yes'}
      ]
    }
  }, 
  computed: {
    filteredList() {
      let shopOutput = [];
      // if the user types in a value for the first name box, then filtered list
      // should only contain the objects that match that first name

      // First, you need to check if there are any filters
      // Think back to what we did with the v-model
        for (let i = 0; i < this.shops.length; i++){
          if (
            (this.shops[i].shopName.toLowerCase().includes(this.filter.shopName.toLowerCase()) || this.filter.shopName == "")&&
            (this.shops[i].shopAddress.toLowerCase().includes(this.filter.shopAddress.toLowerCase()) || this.filter.shopAddress == "")&&
            (this.shops[i].shopZip.includes(this.filter.shopZip) || this.filter.shopZip == "")&&
            (this.shops[i].shopStyle.toLowerCase().includes(this.filter.shopStyle.toLowerCase()) || this.filter.shopStyle == "")&&
            (this.shops[i].anyPiercings.toLowerCase().includes(this.filter.anyPiercings.toLowerCase()) || this.filter.anyPiercings == ""))
            {
              shopOutput.push(this.shops[i])
          }
        } return shopOutput;
    }
  }

}
</script>

<style scoped>

#shop-header {
  font-size: 3rem;
  font-family: Arial, Helvetica, sans-serif;
  color: #721b1b;
}

table {
  margin-top: 20px;
  font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif
}
th {
  text-transform: uppercase
}
td {
  padding: 10px;
}
tr.disabled {
  color: red;
}
input, select {
  font-size: 16px;
}
</style>










