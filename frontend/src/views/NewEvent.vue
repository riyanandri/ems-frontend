<template>
  <div class="create-event-content">
    <b-row style="flex-wrap: inherit;">
      <b-col cols="8" style="overflow: auto;">
        <div class="new-event">
          <form @submit.prevent="pushData">
            <h2>Buat event baru</h2>
            <p>
              preview event ada di samping form
            </p>
            <br />
            <b-row>
              <b-col cols="4">
                <p class="field-name">Judul Event</p>
              </b-col>
              <b-col cols="8">
                <div class="form-group">
                  <vs-input
                    block
                    primary
                    class="form-control"
                    v-model="e_title"
                  >
                    <template
                      v-if="e_title.length < 3 && e_title.length > 0"
                      #message-danger
                    >
                      Nama event minimal 3 karakter
                    </template>
                  </vs-input>
                </div>
              </b-col>
            </b-row>

            <b-row>
              <b-col cols="4">
                <p class="field-name">Penyelenggara</p>
              </b-col>
              <b-col cols="8">
                <div class="form-group">
                  <vs-input
                    block
                    primary
                    class="form-control"
                    v-model="e_organizer"
                  />
                </div>
              </b-col>
            </b-row>
            <b-row>
              <b-col cols="4">
                <p class="field-name">Tanggal</p>
              </b-col>
              <b-col cols="8">
                <div class="form-group">
                  <vs-input
                    block
                    type="date"
                    primary
                    class="form-control"
                    v-model="e_date"
                  />
                </div>
              </b-col>
            </b-row>

            <b-row>
              <b-col cols="4">
                <p class="field-name">Durasi(hari)</p>
              </b-col>
              <b-col cols="8">
                <div class="form-group">
                  <vs-input
                    block
                    type="number"
                    primary
                    class="form-control"
                    v-model="e_duration"
                    placeholder="Days"
                  />
                </div>
              </b-col>
            </b-row>

            <b-row>
              <b-col cols="4">
                <p class="field-name">Lokasi</p>
              </b-col>
              <b-col cols="8">
                <div class="form-group">
                  <vs-input
                    block
                    primary
                    class="form-control"
                    v-model="e_location"
                  />
                </div>
              </b-col>
            </b-row>

            <b-row>
              <b-col cols="4">
                <p class="field-name">Gambar (URL)</p>
              </b-col>
              <b-col cols="8">
                <div class="form-group">
                  <vs-input
                    block
                    primary
                    class="form-control"
                    v-model="previewImage"
                  />
                </div>
              </b-col>
            </b-row>

            <b-row>
              <b-col cols="4">
                <p class="field-name">Deskripsi</p>
              </b-col>
              <b-col cols="8">
                <div class="form-group">
                  <b-form-textarea
                    id="textarea"
                    v-model="e_desc"
                    placeholder="deskripsikan event.."
                    rows="3"
                    max-rows="6"
                  ></b-form-textarea>
                </div>
              </b-col>
            </b-row>

            <b-row>
              <b-col cols="4">
                <p class="t-type">Tipe Tiket</p>
              </b-col>
              <b-col cols="2">
                <div>
                  <vs-switch warn v-model="t_type">
                    <template #on>
                      Premium
                    </template>
                    <template #off>
                      Normal
                    </template>
                  </vs-switch>
                </div>
              </b-col>
              <b-col cols="6">
                <div class="form-group t-sub">
                  <p>
                    *Pilih opsi premium untuk pilihan harga tiket yang lebih
                    banyak
                  </p>
                </div>
              </b-col>
            </b-row>

            <b-row>
              <b-col lg="4" md="12">
                <p class="field-name">Harga Tiket</p>
              </b-col>
              <b-col v-if="!t_type" lg="2" md="12">
                <div v-if="!t_type" class="form-group">
                  <b-card
                    border-variant="primary"
                    header="Normal"
                    header-bg-variant="primary"
                    header-text-variant="white"
                    align="center"
                  >
                    <b-card-text>harga</b-card-text>
                    <vs-input
                      block
                      type="number"
                      primary
                      class="form-control-price"
                      v-model="n_price"
                    />
                  </b-card>
                </div>
              </b-col>
              <b-col lg="2" md="12">
                <div v-if="t_type" class="form-group">
                  <b-card border-variant="info" header="Silver" align="center">
                    <b-card-text>harga</b-card-text>
                    <vs-input
                      block
                      type="number"
                      primary
                      class="form-control-price"
                      v-model="s_price"
                    />
                  </b-card>
                </div>
              </b-col>
              <b-col v-if="t_type" lg="2" md="12">
                <div class="form-group">
                  <b-card
                    bg-variant="warning"
                    header="Gold"
                    text-variant="white"
                    class="text-center"
                  >
                    <b-card-text>harga</b-card-text>
                    <vs-input
                      block
                      type="number"
                      primary
                      class="form-control-price"
                      v-model="g_price"
                    />
                  </b-card>
                </div>
              </b-col>
              <b-col v-if="t_type" lg="2" md="12">
                <div class="form-group">
                  <b-card
                    bg-variant="dark"
                    header="Platinum"
                    text-variant="white"
                    class="text-center"
                  >
                    <b-card-text>harga</b-card-text>
                    <vs-input
                      block
                      type="number"
                      primary
                      class="form-control-price"
                      v-model="p_price"
                    />
                  </b-card>
                </div>
              </b-col>
            </b-row>
            <br />

            <b-row>
              <b-col cols="4"> </b-col>
              <b-col cols="4">
                <div class="form-group">
                  <vs-button block type="submit">Tambah Event</vs-button>
                </div>
              </b-col>
              <b-col cols="4"> </b-col>
            </b-row>
          </form>
        </div>
      </b-col>

      <b-col cols="4">
        <div class="event-card">
          <h2>Preview</h2>
          <vs-card>
            <template #title>
              <h3>{{ e_title }}</h3>
            </template>
            <template #img>
              <img v-if="previewImage != null" :src="previewImage" alt="" />
              <img v-else :src="default_img" alt="" />
            </template>
            <template #text>
              <p class="overflow">
                {{ e_desc }}
              </p>
            </template>
            <template #interactions>
              <vs-button v-if="t_type" warn icon>
                <i class="bx bx-dollar-circle"></i>
              </vs-button>
              <vs-button v-if="!t_type" icon>
                <i class="bx bx-dollar-circle"></i>
              </vs-button>
              <vs-button class="btn-chat" shadow primary>
                <box-icon name="calendar"></box-icon>
                <span class="span">
                  {{ e_date }}
                </span>
              </vs-button>
            </template>
          </vs-card>
        </div>
      </b-col>
    </b-row>
    <template>
      <div class="center">
        <vs-dialog blur v-model="active_dialogue">
          <template #header>
            <h4 class="not-margin">Event berhasil ditambahkan!</h4>
          </template>
          <div>
            <img
              class="popup"
              src="https://cdn.dribbble.com/users/2173054/screenshots/8143107/media/d5e2d1d137f0e7c374d66dd339d9b184.gif"
              alt=""
            />
          </div>
        </vs-dialog>
      </div>
    </template>
  </div>
</template>

<script>
import axios from '../vuexios';

export default {
  data() {
    return {
      active_dialogue: false,
      previewImage:
        'https://www1.chester.ac.uk/sites/default/files/styles/hero_mobile/public/Music-Production-and-Promotion_0.jpg?itok=AMRG5XBn',
      e_title: '',
      e_desc: '',
      e_organizer: '',
      e_location: '',
      e_duration: 0,
      e_date: null,
      t_type: false,
      n_price: 0,
      s_price: 0,
      g_price: 0,
      p_price: 0,
      message: '',
    };
  },

  methods: {
    pushData() {
      if (!this.t_type && !this.n_price) {
        alert('Masukkan harga normal.');
        return;
      }
      if (this.t_type && (!this.s_price || !this.g_price || !this.p_price)) {
        alert('Masukkan harga tiket Silver, Gold dan Platinum.');
        return;
      }
      const content = {
        e_name: this.e_title,
        e_desc: this.e_desc,
        e_organizer: this.e_organizer,
        e_location: this.e_location,
        e_duration: this.e_duration,
        e_date: this.e_date,
        t_type: this.t_type,
        normal: this.n_price,
        silver: this.s_price,
        gold: this.g_price,
        platinum: this.p_price,
        e_image_url: this.previewImage,
      };
      console.log(content);
      axios
        .post('/createnewevent', content)
        .then(response => {
          this.message = response.data.message;
        })
        .then(() => {
          this.active_dialogue = true;
          setTimeout(() => {
            this.$router.push({ name: 'Dashboard' });
          }, 2000);
        })
        .catch(err => {
          alert('Semua kolom perlu di isi!');
          console.log(err);
        });
    },
  },
};
</script>

<style scoped>
.new-event {
  height: 1000px;
  background-size: cover;
  position: relative;
}

.popup {
  max-height: 17em;
  /* max-width: 400px; */
}

label {
  cursor: pointer;
  color: blue;
  font-size: 10px;
  margin-left: 10px;
}

.t-type {
  padding-bottom: 5px;
}

.t-sub {
  font-size: 10px;
  float: left;
  padding-top: 5px;
}

#upload-photo {
  opacity: 0;
  position: absolute;
  z-index: -1;
}

.overflow {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  line-height: 16px;
  max-height: 32px;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}

.imagePreviewWrapper {
  width: 100%;
  height: 250px;
  display: block;
  cursor: pointer;
  margin: 0 auto 30px;
  object-fit: contain;
  background-size: cover;
  background-position: center center;
  border-radius: 10px;
}

.event-card {
  padding-top: 15rem;
}

.new-event form {
  text-align: center;
  max-width: 1000px;
  width: 90%;
  background-color: #ffffff;
  padding: 40px;
  border-radius: 4px;
  transform: translate(-50%, -50%);
  position: absolute;
  top: 45%;
  left: 55%;
  color: rgb(0, 0, 0);
  box-shadow: 3px 3px 4px rgba(255, 249, 249, 0.2);
}

.field-name {
  padding-top: 15px;
}

.new-event form .form-control {
  background: none;
  border: none;
  border-radius: 0;
  box-shadow: none;
  outline: none;
  color: inherit;
}
.form-control-price {
  min-width: 20px;
}
.create-event-content {
  overflow: hidden;
}
.create-event-content .card-header {
  font-size: small;
}
</style>
