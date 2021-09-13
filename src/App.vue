<template>
  <main>
    <div class="clientData" v-if="this.personDataIsVisible">
      <div class="clientNotification" v-if="notificationDescIsVisible">
        <form @submit.prevent="sendNewNotification">
          <h2>Zgłoszenie serwisowe</h2>
          <textarea
            name="serviceDescription"
            cols="30"
            rows="10"
            v-model="typedNotificationDesc"
          ></textarea>
          <button class="sendNotification">Wyślij</button>
        </form>
        <button class="closeNotification" @click="closeNotificationDesc">
          X
        </button>
      </div>
      <section class="moreInfoAboutClient">
        <h2>Dane klienta</h2>
        <div class="aboutClient">
          <p>
            Imię: <span>{{ VueShowClient.currentClient.name }}Hubert</span>
          </p>
          <p>
            Nazwisko:
            <span>{{ VueShowClient.currentClient.surname }}Radziwonka</span>
          </p>
          <p>
            Nazwa firmy:
            <span
              >{{ VueShowClient.currentClient.companyName }}HUBREX COMPANY
              SA</span
            >
          </p>
          <p>
            NIP:
            <span>{{ VueShowClient.currentClient.nip }} xxxxxxxxxxxxxxxxx</span>
          </p>
          <p>
            Adres:
            <span>{{ VueShowClient.currentClient.address }} kwiatowa 1</span>
          </p>
          <p>
            Pesel:
            <span>{{ VueShowClient.currentClient.pesel }} 990506007091</span>
          </p>
          <p>
            Telefon:
            <span>{{ VueShowClient.currentClient.phoneNumber }}694224869</span>
          </p>
          <p>
            E-mail:
            <span
              >{{
                VueShowClient.currentClient.email
              }}hubert.radziwonka33@gmail.com</span
            >
          </p>
        </div>
        <div class="clientCars">
          <h4>Auta klienta</h4>
          <form @submit.prevent="addCarToClient">
            <button class="addNewCar">
              Dodaj auto
            </button>
          </form>

          <div class="clientCarsList">
            <div
              class="oneClientCar"
              v-for="(car, index) in VueShowClient.carAso.items"
              :key="index"
            >
              <tr>
                <td>
                  Marka: <span class="orderBrand">{{ car.brand }}</span>
                </td>
                <td>
                  Model: <span class="orderModel">{{ car.model }}</span>
                </td>
                <td>
                  Silnik: <span class="orderEngine">{{ car.engineType }}</span>
                </td>
                <td>
                  Napęd: <span class="orderDrive">{{ car.driveType }}</span>
                </td>
                <td>
                  skrzynia biegów:
                  <span class="orderGear">{{ car.gearType }}</span>
                </td>
                <td>
                  Rok produkcji:
                  <span class="orderProduction">{{ car.productionYear }}</span>
                </td>
                <td>
                  Kolor: <span class="orderColor">{{ car.color }}</span>
                </td>
                <td>
                  VIN: <span class="orderVin">{{ car.vinNumber }}</span>
                </td>
                <button
                  class="sendToService"
                  @click="openNotificationDesc(index)"
                >
                  Wyślij zgłoszenie do serwisu
                </button>
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
        <h3 v-if="this.showPeselError">
          Wpisz poprawnie numer pesel (11 znaków)
        </h3>
        <form @submit.prevent="searchClient">
          <input
            type="text"
            placeholder="Wyszukaj klienta po numerze PESEL..."
            v-model="typedPesel"
            class="clientInputSearch"
          />
          <button class="searchClient" @click="searchByPesel">
            Wyszukaj klienta
          </button>
          <button class="addClient" @click="addNewClient">
            Dodaj klienta
          </button>
        </form>
        <aside>
          <!-- <h3 v-if="this.clientList.length == 0">
            Nie znaleziono klienta w bazie danych
          </h3> -->
          <div class="oneClient">
            <tr>
              <h4>Imię i nazwisko</h4>
              <td>{{ VueShowClient.currentClient.name }}hubert</td>
              <td>
                {{ VueShowClient.currentClient.surname }}radziwasadasdasdas
              </td>
            </tr>
            <tr>
              <h4>Nazwa i NIP firmy</h4>
              <td>
                {{ VueShowClient.currentClient.companyName }}dsadasdadadas
              </td>
              <td>{{ VueShowClient.currentClient.nip }}dsadasdasdasdasd</td>
            </tr>
            <tr>
              <h4>Adres i pesel</h4>
              <td>{{ VueShowClient.currentClient.address }}asdassdasdasdas</td>
              <td class="pesel">
                {{ VueShowClient.currentClient.pesel }}dasdasdasdasdasd
              </td>
            </tr>
            <tr>
              <h4>Dane kontaktowe</h4>
              <td>
                {{ VueShowClient.currentClient.phoneNumber }}asdasdasdasdsadas
              </td>
              <td>{{ VueShowClient.currentClient.email }}dasdasdsa</td>
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
    carOrd: {},
    typedPesel: "",
    typedNotificationDesc: "",
    notificationDescIsVisible: false,
    personDataIsVisible: false,
    selectedCar: [],
    showPeselError: false,
  }),
  mounted() {
    this.VueShowClient = this.coachViewContext.binding.get("value");
  },
  methods: {
    showPerson() {
      this.personDataIsVisible = true;
    },
    searchByPesel() {
      this.VueShowClient.searchByPesel = this.typedPesel;
      this.VueShowClient.buttonSearchClient = true;
      this.VueShowClient.buttonAddCar = false;
      this.VueShowClient.buttonAddClient = false;
      this.VueShowClient.buttonAddOrder = false;
    },
    addNewClient() {
      this.VueShowClient.buttonSearchClient = false;
      this.VueShowClient.buttonAddCar = false;
      this.VueShowClient.buttonAddClient = true;
      this.VueShowClient.buttonAddOrder = false;
    },
    addCarToClient() {
      this.VueShowClient.buttonSearchClient = false;
      this.VueShowClient.buttonAddCar = true;
      this.VueShowClient.buttonAddOrder = false;
      this.VueShowClient.buttonAddClient = false;
      this.coachViewContext.binding.set("value", this.VueShowClient);
      this.coachViewContext.trigger();
    },
    closeClientData() {
      this.personDataIsVisible = false;
    },
    searchClient() {
      const searchClient = document.querySelector(".clientInputSearch");
      if (this.typedPesel.length !== 11) {
        searchClient.classList.add("active");
        this.showPeselError = true;
      } else {
        this.coachViewContext.binding.set("value", this.VueShowClient);
        this.coachViewContext.trigger();
        this.VueShowClient = this.coachViewContext.binding.get("value");
        this.typedPesel = "";
        searchClient.classList.remove("active");
        this.showPeselError = false;
      }
    },
    openNotificationDesc(index) {
      this.VueShowClient.carCaseid = this.VueShowClient.carAso.items[
        index
      ].mrcCaseHeader.caseId;
      console.log(this.VueShowClient);
      this.notificationDescIsVisible = true;
    },
    closeNotificationDesc() {
      this.notificationDescIsVisible = false;
      this.typedNotificationDesc = "";
      this.selectedCar = [];
    },
    sendNewNotification() {
      this.VueShowClient.clientsDescription = this.typedNotificationDesc;
      this.VueShowClient.buttonSearchClient = false;
      this.VueShowClient.buttonAddCar = false;
      this.VueShowClient.buttonAddClient = false;
      this.VueShowClient.buttonAddOrder = true;
      this.coachViewContext.binding.set("value", this.VueShowClient);
      this.coachViewContext.trigger();
    },
  },
};
</script>

<style scoped>
@import "./css/app.css";
</style>
