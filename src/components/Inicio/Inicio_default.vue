<template>
  <div class="containerIni">
    <h2 class="titleFont">Chuck Norris</h2>
    <img
      src="https://img.europapress.es/fotoweb/fotonoticia_20150310130850-732359_600.jpg"
      alt="Mi imagen"
      class="image_chuck"
    />
    <q-btn class="btnalign" @click="selectBtn">Mostrar Lema</q-btn>
    <div class="containerText">
      <h6 class="custom-h6">
        Fecha de Creacion: {{ formatDate(this.chuckResult.created_at) }}
      </h6>
      <h6 class="custom-h6">Lema: {{ this.chuckResult.value }}</h6>
      <h6 class="custom-h6">
        Fecha de Actualizacion: {{ formatDate(this.chuckResult.updated_at) }}
      </h6>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";

export default {
  data() {
    return {
      chuckResult: {
        categories: [],
        created_at: "",
        icon_url: "",
        id: "",
        updated_at: "",
        url: "",
        value: "",
      },
    };
  },
  methods: {
    selectBtn() {
      axios
        .get("https://api.chucknorris.io/jokes/random")
        .then((response) => {
          const StoreData = response.data;
          this.chuckResult = StoreData;
          // this.showNotification("Exito", "green", "top", 3000);
        })
        .catch((error) => {
          this.showNotification("Error", "red", "top", 3000);
          console.log(error);
        });
    },
    showNotification: function (message, color, position, timeout) {
      var notification = document.createElement("div");
      notification.textContent = message;
      notification.style.backgroundColor = color;
      notification.style.color = "#fff";
      notification.style.padding = "10px";
      notification.style.borderRadius = "4px";
      notification.style.boxShadow = "0 2px 6px rgba(0, 0, 0, 0.15)";
      notification.style.position = "fixed";
      notification.style.bottom = position === "bottom" ? "20px" : "";
      notification.style.top = position === "top" ? "20px" : "";
      notification.style.left = "50%";
      notification.style.transform = "translateX(-50%)";
      notification.style.zIndex = "9999";
      document.body.appendChild(notification);
      setTimeout(function () {
        document.body.removeChild(notification);
      }, timeout);
    },
    formatDate(date) {
      return moment(date).format("YYYY-MM-DD");
    },
  },
  mounted() {},
};
</script>

<style>
@import url(https://fonts.googleapis.com/css?family=Exo:100,200,400);

.titleFont {
  font-family: "Exo";
  font-size: 100px;
  text-align: center;
}
.btnalign {
  color: black;
  background-color: greenyellow;
  position: absolute;
  left: 45%;
  font-family: "Exo";
}
.btnalign:hover {
  background-color: rgb(132, 6, 6);
  color: white;
}
.containerText {
  margin-left: 35px;
  padding: 10px 5px;
  margin-bottom: -0.5em;
}
.custom-h6 {
  margin-bottom: -1em; /* Ajusta este valor según tus necesidades */
  font-family: "Exo";
}
.image_chuck {
  width: 120px;
  height: 130px;
  position: absolute;
  left: 45%;
  bottom: 40px;
}
</style>
