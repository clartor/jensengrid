<template>

  <v-app>
    <div v-if="responseAvailable == true">
      <hr />
      <p>
        <i>{{ result }}</i>
      </p>
      <hr />
    </div>
  </v-app>
</template>

<script>
export default {
  data: () => {
    return {
      result: '',
      responseAvailable: false,
      // apiKey: 'Top-Secret-Shhh-Key',
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      this.responseAvailable = false;
      fetch("https://www.foaas.com/bag/Clara", {
        "method": "GET",
      })
        .then((response) => {
          if (response.ok) {
            response.text().then((response) => {
              this.result = response;
              this.responseAvailable = true;
              console.log("this.result: " + this.result);
            
            });
          } else {
            alert(
              "Server returned " + response.status + " : " + response.statusText
            );
          }
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>