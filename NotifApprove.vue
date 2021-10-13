<template>
  <q-page
    :class="'row q-pa-md items-center justify-center ' + ($q.screen.sm ? 'background-bottom' : 'background')"
  >
    <div class="col-12 q-px-xl orientation-portrait">
      <div class="text-subtitle2">
        Selamat Datang di
      </div>
      <div class="text-h4 text-bold">
        BRI GTI Ragunan
      </div>
      <div class="column">
        <q-carousel
          v-model="slide"
          transition-prev="slide-right"
          transition-next="slide-left"
          swipeable
          animated
          navigation
          padding
          autoplay
          infinite
          control-color="primary"
          style="min-height: 180px"
          class="col bg-transparent"
        >
          <q-carousel-slide
            v-for="(b, idx) in banners"
            :key="idx"
            :name="b.id"
            class="column no-wrap"
          >
            <q-img
              :src="b.img"
              style="min-height: 180px"
              contain
            />
          </q-carousel-slide>
        </q-carousel>
      </div>
    </div>
    <div class="col-4 gt-sm q-px-xl">
      <div class="orientation-landscape">
        <div class="text-subtitle2">
          Selamat Datang di
        </div>
        <div class="text-h4 text-bold">
          BRI GTI Ragunan
        </div>
      </div>
      <img
        src="~assets/img/login/illus-self-service-2.svg"
        class="img-ilustrasi q-mt-lg"
      >
    </div>
    <div class="column col-md-8 col-sm-10 col-xs-12 justify-center q-gutter-md">
      <!-- <q-carousel
        v-if="!allMenu"
        v-model="slide"
        transition-prev="slide-right"
        transition-next="slide-left"
        swipeable
        animated
        navigation
        padding
        autoplay
        infinite
        control-color="primary"
        class="col bg-transparent orientation-landscape"
      >
        <q-carousel-slide
          v-for="(b, idx) in banners"
          :key="idx"
          :name="b.id"
          class="column no-wrap"
        >
          <q-img
            :src="b.img"
            style="min-height: 180px"
            contain
          />
        </q-carousel-slide>
      </q-carousel> -->
      <div class="column col">
        <div class="row justify-center">
          <div :class="'col-xl-9 col-lg-10 col-md-12 ' + (deviceMobile ? 'col-sm-12' : 'col-sm-8')">
            <div class="row q-col-gutter-lg q-pt-md">
              <div
                v-for="(d) in row"
                :key="d"
                :class="'col-md-3 ' + (deviceMobile ? 'col-sm-4 col-xs-4' : 'col-sm-6 col-xs-6')"
              >
                <div
                  v-if="menus.length >= d + firstIndexMenu"
                  class="row justify-center"
                >
                  <q-btn
                    stack
                    style="height: 170px; width: 170px;"
                    class="btn"
                    :to="menus[(d-1) + firstIndexMenu].to"
                  >
                    <q-img
                      class="btn-img"
                      :src="menus[(d-1) + firstIndexMenu].icon"
                    />
                    <div
                      class="btn-label text-bold text-capitalize"
                    >
                      {{ menus[(d-1) + firstIndexMenu].label }}
                    </div>
                  </q-btn>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div
        v-if="!allMenu"
        class="row q-pa-md q-mt-md"
      >
        <q-space />
        <q-btn
          padding="md"
          color="secondary"
          unelevated
          @click="changeAllMenu(true)"
        >
          <div class="q-mx-sm">
            Semua Menu
          </div>
          <q-icon name="chevron_right" />
        </q-btn>
      </div>
      <div
        v-else
        class="row q-pa-md"
      >
        <q-btn
          padding="md"
          color="warning"
          unelevated
          @click="changeAllMenu(false)"
        >
          <q-icon name="ion-home" />
          <div class="q-mx-sm">
            HOME
          </div>
        </q-btn>
        <q-space />
        <q-btn
          padding="md"
          class="q-mr-lg"
          color="grey-4"
          unelevated
          :disable="firstIndexMenu == 0"
          @click="back()"
        >
          <q-icon
            name="chevron_left"
            color="black"
          />
          <div class="q-mx-sm text-black">
            BACK
          </div>
        </q-btn>
        <q-btn
          padding="md"
          color="primary"
          unelevated
          :disable="lastIndexMenu >= (menus.length- 1)"
          @click="next()"
        >
          <div class="q-mx-sm">
            NEXT
          </div>
          <q-icon name="chevron_right" />
        </q-btn>
      </div>
    </div>
    <div class="lt-md padding-mobile" />
    <img
      src="~assets/img/login/illus-self-service-2.svg"
      class="lt-md img-ilustrasi-bottom"
    >
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      firstIndexMenu: 0,
      lastIndexMenu: 0,
      allMenu: false,
      slide: '',
      banners: [
        {
          id: 1,
          img: '/statics/img/banner/banner-example-1.png'
        },
        {
          id: 2,
          img: '/statics/img/banner/banner-example-1.png'
        },
        {
          id: 3,
          img: '/statics/img/banner/banner-example-1.png'
        }
      ]
    };
  },
  computed: {
    menus() {
      return [
        {
          label: 'Notifiasi Approval',
          icon: '/statics/img/icon/ico-ss-butab.svg',
          to: '/self-service/printaccountstatement'
        },
        {
          label: 'Rekening Baru',
          icon: '/statics/img/icon/ico-ss-butab.svg',
          to: '/self-service/printaccountstatement'
        },
        {
          label: 'Setoran Tunai',
          icon: '/statics/img/icon/ico-ss-butab.svg',
          to: '/self-service/printaccountstatement'
        },
        {
          label: 'Tarik Tunai',
          icon: '/statics/img/icon/ico-ss-butab.svg',
          to: '/self-service/printaccountstatement'
        },
        {
          label: 'Rekening Koran',
          icon: '/statics/img/icon/ico-ss-butab.svg',
          to: '/self-service/printaccountstatement'
        },
        {
          label: 'Promo BRI',
          icon: '/statics/img/icon/ico-ss-butab.svg',
          to: '/self-service/printaccountstatement'
        },
        {
          label: 'Transfer',
          icon: '/statics/img/icon/ico-ss-butab.svg',
          to: '/self-service/printaccountstatement'
        },
        {
          label: 'Customer Service',
          icon: '/statics/img/icon/ico-ss-butab.svg',
          to: '/self-service/printaccountstatement'
        },
        {
          label: 'Cetak Buku Tabungan',
          icon: '/statics/img/icon/ico-ss-butab.svg',
          to: '/self-service/printaccountstatement'
        }
      ];
      // return this.$store.getters["selfService/allMenu"];
    },
    row() {
      let row = 4;
      if (this.allMenu) {
        row = this.$q.screen.sm ? 3 : 4;
        row *= 2;
      }

      return row;
    },
    deviceMobile() {
      if (this.allMenu) return this.$q.screen.sm;
      return false;
    }
  },
  async preFetch({ store }) {
    const { default: storeModule } = await import('src/modules/core/store/selfService');
    await store.registerModuleSafely('selfService', storeModule);
  },
  mounted() {
    this.slide = this.banners[0].id;
  },
  methods: {
    changeAllMenu(val) {
      this.allMenu = val;
      this.firstIndexMenu = 0;
      this.lastIndexMenu = this.row - 1;
    },
    next() {
      this.lastIndexMenu += this.row;
      this.firstIndexMenu += this.row;
    },
    back() {
      this.lastIndexMenu -= this.row;
      this.firstIndexMenu -= this.row;
    }
  }
};
</script>

<style>
.btn {
  background: linear-gradient(180deg, #b184fd 0%, #9a66f2 100%);
  box-shadow: 0px 11.25px 33.75px rgba(72, 13, 201, 0.15);
  border-radius: 22.5px;
}
.btn-img {
  width: 50%;
  margin-bottom: 16px;
}
.btn-label {
  font-size: 1rem;
}
.img-ilustrasi {
  width: 100%;
  max-width: 150px;
}
.img-ilustrasi-bottom {
  width: 100%;
  max-width: 150px;
  position: absolute;
  bottom: 10px;
  left: 35px;
}
.padding-mobile {
  width: 100%;
  min-height: 10px;
  height: 15%;
  max-height: 100px;
}
.background {
  background: url("/statics/img/illus/background-self-service.svg") no-repeat;
  background-position: 0 -135px;
}
.background-bottom {
  background-image: url("../../../statics/img/illus/background-self-service.svg");
  background-repeat: no-repeat;
  padding-bottom: 120px;
  background-position: bottom left;
}
</style>
