<template>
  <main>
    <div class="clientData" v-if="this.personDataIsVisible">
      <section class="moreInfoAboutClient">
        <h2>Dane klienta</h2>
        <div
          class="aboutClient"
          v-for="(client, index) in this.pickedClient"
          :key="index"
        >
          <p>
            Imię: <span> {{ client.name }}</span>
          </p>
          <p>
            Nazwisko: <span>{{ client.surname }}</span>
          </p>
          <p>
            Nazwa firmy: <span>{{ client.companyName }}</span>
          </p>
          <p>
            NIP: <span>{{ client.nip }}</span>
          </p>
          <p>
            Adres: <span>{{ client.address }}</span>
          </p>
          <p>
            Pesel: <span>{{ client.pesel }}</span>
          </p>
          <p>
            Telefon: <span>{{ client.phoneNumber }}</span>
          </p>
          <p>
            E-mail: <span>{{ client.email }}</span>
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
          />
          <button class="searchClient">Wyszukaj klienta</button>
          <button class="addClient">Dodaj klienta</button>
        </form>
        <aside>
          <h3 v-if="this.clientList.length == 0">
            Nie znaleziono klienta w bazie danych
          </h3>
          <div
            class="oneClient"
            v-for="(client, index) in clientList"
            :key="index"
            :id="client.id"
          >
            <tr>
              <h4>Klient</h4>
              <td>{{ client.name }}</td>
              <td>{{ client.surname }}</td>
            </tr>
            <tr>
              <h4>Dane firmy</h4>
              <td>{{ client.companyName }}</td>
              <td>{{ client.nip }}</td>
            </tr>
            <tr>
              <h4>Adres i pesel</h4>
              <td>{{ client.address }}</td>
              <td class="pesel">{{ client.pesel }}</td>
            </tr>
            <tr>
              <h4>Dane kontaktowe</h4>
              <td>{{ client.phoneNumber }}</td>
              <td>{{ client.email }}</td>
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
  data() {
    return {
      typedPesel: "",
      personDataIsVisible: false,
      pickedClient: [],
      clientList: [
        {
          id: 0,
          name: "Jan",
          surname: "Kowalski",
          companyName: "JanBud",
          pesel: "70052856839",
          nip: "5842751979",
          address: "Warszawa, ul. Złota 4",
          email: "jan.kowal@gmail.com",
          phoneNumber: "333-333-333",
        },
        {
          id: 1,
          name: "Hubert",
          surname: "Radziwonka",
          companyName: "Hubrex",
          pesel: "4052856839",
          nip: "5427342979",
          address: "Warszawa, ul. Złota 8",
          email: "hub.rad@gmail.com",
          phoneNumber: "444-444-444",
        },
      ],
    };
  },
  methods: {
    showPerson(e) {
      this.pickedClient = [];
      const pickedElement = e.target.parentNode.id;
      const person = this.clientList[pickedElement];
      this.pickedClient.push(person);
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
      const clientPesel = document.querySelectorAll(".oneClient tr .pesel");
      console.log(
        clientPesel.forEach((pesel) => {
          console.log(pesel.textContent);
          console.log(pesel.parentNode.parentNode);
        })
      );
    },
  },
};
</script>

<style scoped>
@import "./css/app.css";
</style>
