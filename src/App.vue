<template>
  <main>
    <div class="clientData" v-if="this.personDataIsVisible">
      <section class="moreInfoAboutClient">
        <h2>Dane klienta</h2>
        <div class="aboutClient">
          <p>
            Imię: <span>{{ VueShowClient.currentClient.name }}</span>
          </p>
          <p>
            Nazwisko:
            <span>{{ VueShowClient.currentClient.surname }}</span>
          </p>
          <p>
            Nazwa firmy:
            <span>{{ VueShowClient.currentClient.companyName }}</span>
          </p>
          <p>
            NIP: <span>{{ VueShowClient.currentClient.nip }}</span>
          </p>
          <p>
            Adres: <span>{{ VueShowClient.currentClient.address }}</span>
          </p>
          <p>
            Pesel: <span>{{ VueShowClient.currentClient.pesel }}</span>
          </p>
          <p>
            Telefon: <span>{{ VueShowClient.currentClient.phoneNumber }}</span>
          </p>
          <p>
            E-mail: <span>{{ VueShowClient.currentClient.email }}</span>
          </p>
        </div>
        <div class="clientCars">
          <h4>Auta klienta</h4>
          <button class="addNewCar">Dodaj / usuń auto</button>
          <div class="clientCarsList">
            <div class="oneClientCar">
              <tr>
                <td>Marka: <span>asd</span></td>
                <td>Model: <span>asd</span></td>
                <td>Silnik: <span>2.0 diesel 180km</span></td>
                <td>skrzynia biegów: <span>Manualna</span></td>
                <td>Rok produkcji: <span>2009</span></td>
                <td>Kolor: <span>czarny</span></td>
                <td>VIN: <span>xdddd</span></td>
              </tr>
            </div>
          </div>
        </div>
        <button class="closeClientData" @click="closeClientData">X</button>
      </section>
    </div>
    <header>
      <h1>Autoryzowany serwis aut</h1>
    </header>
    <section class="aboutClient">
      <div class="clientList">
        <form @submit.prevent="searchClient">
          <input
            type="text"
            placeholder="Wyszukaj klienta po numerze PESEL..."
            v-model="typedPesel"
          />
          <button class="searchClient">Wyszukaj klienta</button>
          <button class="addClient">Dodaj klienta</button>
        </form>
        <aside>
          <!-- <h3 v-if="this.clientList.length == 0">
            Nie znaleziono klienta w bazie danych
          </h3> -->
          <div class="oneClient">
            <tr>
              <h4>Imię i nazwisko</h4>
              <td>{{ VueShowClient.currentClient.name }}</td>
              <td>{{ VueShowClient.currentClient.surname }}</td>
            </tr>
            <tr>
              <h4>Nazwa i NIP firmy</h4>
              <td>
                {{ VueShowClient.currentClient.companyName }}
              </td>
              <td>{{ VueShowClient.currentClient.nip }}</td>
            </tr>
            <tr>
              <h4>Adres i pesel</h4>
              <td>{{ VueShowClient.currentClient.address }}</td>
              <td class="pesel">{{ VueShowClient.currentClient.pesel }}</td>
            </tr>
            <tr>
              <h4>Dane kontaktowe</h4>
              <td>{{ VueShowClient.currentClient.phoneNumber }}</td>
              <td>{{ VueShowClient.currentClient.email }}</td>
            </tr>
            <button class="showMoreInfo" @click="showPerson">
              Pokaż więcej informacji
            </button>
          </div>
        </aside>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  data: () => ({
    VueShowClient: {},
    typedPesel: "",
    personDataIsVisible: false,
    pickedClient: [],
    clientList: [],
  }),
  mounted() {
    this.VueShowClient = this.coachViewContext.binding.value;
    console.log(this.VueShowClient);
    //console.log(this.kierunkiStudiow);
  },
  methods: {
    showPerson() {
      this.personDataIsVisible = true;
    },
    showTestResult() {
      console.log(this.pickedClient);
    },
    closeClientData() {
      this.personDataIsVisible = false;
      this.pickedClient = [];
    },
    searchClient() {
      this.coachViewContext.binding.set("value", this.VueShowClient);
      this.coachViewContext.trigger();

      // const clientPesel = document.querySelectorAll(".oneClient tr .pesel");
      // console.log(
      //   clientPesel.forEach((pesel) => {
      //     const client = pesel.parentNode.parentNode;
      //     if (this.typedPesel !== pesel.textContent) {
      //       client.style.display = "none";
      //     } else {
      //       client.style.display = "flex";
      //     }
      //     console.log(pesel.textContent);
      //     console.log(pesel.parentNode.parentNode);
      //   })
      // );
      console.log(this.clientList);
    },
  },
};
</script>

<style scoped>
@import "./css/app.css";
</style>
