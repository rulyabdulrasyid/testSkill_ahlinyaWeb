<template>
  <h1>Formulir Input Data</h1>
  <h2 class="mb-5">Penerima Bantuan Sosial (BANSOS)</h2>
  <div class="container">
    <div class="container text-start border rounded-3 p-5 mb-3 bg-dark-subtle">
      <form
        @submit.prevent="submitForm"
        class="row g-3"
        enctype="multipart/form-data"
      >
        <div class="col-md-6">
          <label for="nama" class="form-label fw-bolder">Nama</label>
          <input
            type="text"
            class="form-control"
            id="nama"
            v-model="formData.Nama"
            required
          />
        </div>
        <div class="col-md-3">
          <label for="umur" class="form-label fw-bolder">Umur</label>
          <input
            type="number"
            class="form-control"
            id="umur"
            v-model="formData.Umur"
            min="25"
            required
          />
        </div>
        <div class="col-md-3">
          <label for="gender" class="form-label fw-bolder">Jenis Kelamin</label>
          <select class="form-select" v-model="formData.Gender" required>
            <option value="" disabled>Pilih Gender...</option>
            <option value="Laki-Laki">Laki-Laki</option>
            <option value="Perempuan">Perempuan</option>
          </select>
        </div>
        <div class="col-md-6">
          <label for="nik" class="form-label fw-bolder">NIK</label>
          <input
            type="text"
            class="form-control"
            id="nik"
            v-model="formData.NIK"
            required
          />
        </div>
        <div class="col-md-6">
          <label for="kk" class="form-label fw-bolder">KK</label>
          <input
            type="text"
            class="form-control"
            id="kk"
            v-model="formData.KK"
            required
          />
        </div>

        <div class="mb-3 col-md-6">
          <label for="fotoktp" class="form-label fw-bolder">Foto KTP</label>
          <input
            class="form-control"
            type="file"
            id="fotoktp"
            ref="FotoKTP"
            @change="handleFileChange('FotoKTP')"
            accept=".jpg, .jpeg, .png, .bmp"
            required
          />
        </div>
        <div class="mb-3 col-md-6">
          <label for="fotokk" class="form-label fw-bolder">Foto KK</label>
          <input
            class="form-control"
            type="file"
            id="fotokk"
            ref="FotoKK"
            @change="handleFileChange('FotoKK')"
            accept=".jpg, .jpeg, .png, .bmp"
            required
          />
        </div>

        <div class="col-md-4">
          <label for="provinsi" class="form-label fw-bolder">Provinsi</label>
          <select
            id="provinsi"
            class="form-select"
            v-model="formData.selectedProvince"
            @change="onProvinsiChange"
            required
          >
            <option value="" disabled>Pilih Provinsi...</option>
            <option
              v-for="province in provinces"
              :key="province.id"
              :value="province.name"
            >
              {{ province.name }}
            </option>
          </select>
        </div>
        <div class="col-md-4">
          <label for="kab_kota" class="form-label fw-bolder">Kab/Kota</label>
          <select
            id="kab_kota"
            class="form-select"
            v-model="formData.selectedRegencies"
            @change="onRegenciesChange"
            required
          >
            <option value="" disabled>Pilih Kab/Kota...</option>
            <option
              v-for="regencies in regencies"
              :key="regencies.id"
              :value="regencies.name"
            >
              {{ regencies.name }}
            </option>
          </select>
        </div>
        <div class="col-md-4">
          <label for="kecamatan" class="form-label fw-bolder">Kecamatan</label>
          <select
            id="inputState"
            class="form-select"
            v-model="formData.selectedDistricts"
            @change="onDistrictsChange"
            required
          >
            <option value="" disabled>Pilih Kecamatan...</option>
            <option
              v-for="districts in districts"
              :key="districts.id"
              :value="districts.name"
            >
              {{ districts.name }}
            </option>
          </select>
        </div>
        <div class="col-md-4">
          <label for="KelDesa" class="form-label fw-bolder"
            >Kelurahan/Desa</label
          >
          <select
            id="inputState"
            class="form-select"
            v-model="formData.selectedvillages"
            required
          >
            <option value="" disabled>Pilih Kelurahan...</option>
            <option
              v-for="villages in villages"
              :key="villages.id"
              :value="villages.name"
            >
              {{ villages.name }}
            </option>
          </select>
        </div>

        <div>
          <label for="alamat" class="form-label fw-bolder">Alamat</label>
          <textarea
            class="form-control"
            id="alamat"
            rows="3"
            v-model="formData.Alamat"
            required
          ></textarea>
        </div>

        <div class="col-md-6">
          <label for="rt" class="form-label fw-bolder">RT</label>
          <input
            type="text"
            class="form-control"
            id="rt"
            v-model="formData.RT"
            required
          />
        </div>
        <div class="col-md-6">
          <label for="rw" class="form-label fw-bolder">RW</label>
          <input
            type="text"
            class="form-control"
            id="rw"
            v-model="formData.RW"
            required
          />
        </div>

        <div class="col-md-6">
          <label for="before" class="form-label fw-bolder"
            >Penghasilan Sebelum Pandemi</label
          >
          <input
            type="number"
            class="form-control"
            id="before"
            v-model="formData.Before"
            required
          />
        </div>
        <div class="col-md-6">
          <label for="after" class="form-label fw-bolder"
            >Penghasilan Seteleh Pandemi</label
          >
          <input
            type="number"
            class="form-control"
            id="after"
            v-model="formData.After"
            required
          />
        </div>
        <div>
          <label for="alasan" class="form-label fw-bolder"
            >Alasan Membutuhkan Bantuan</label
          >
          <select
            id="inputState"
            class="form-select"
            v-model="formData.Alasan"
            required
          >
            <option value="" disabled>Pilih Alasan...</option>
            <option value="Kehilangan Pekerjaan">Kehilangan pekerjaan</option>
            <option value="Kepala Keluarga">Kepala keluarga</option>
            <option value="Tergolong Fakir/Miskin">
              Tergolong fakir/miskin
            </option>
            <option value="Lainnya">Lainnya</option>
          </select>
          <div v-if="formData.Alasan === 'Lainnya'">
            <label for="alasanLainnya" class="form-label fw-bolder"
              >Alasan Lainnya</label
            >
            <input
              type="text"
              class="form-control"
              id="alasanLainnya"
              v-model="formData.AlasanLainnya"
              required
            />
          </div>
        </div>

        <div class="col-12">
          <div class="form-check">
            <input
              class="form-check-input"
              type="checkbox"
              id="gridCheck"
              v-model="formData.PernyataanKebenaran"
              required
            />
            <label class="form-check-label" for="gridCheck">
              Saya menyatakan bahwa data yang diisikan adalah benar dan siap
              mempertanggungjawabkan apabila ditemukan ketidaksesuaian dalam
              data tersebut.
            </label>
          </div>
        </div>

        <div class="col-12">
          <button
            type="button"
            class="btn btn-primary"
            @click="openPreviewModal"
            :disabled="!isFormValid"
          >
            Preview Data
          </button>
        </div>

        <ReviewData
          v-if="showPreviewModal"
          :formData="formData"
          @close="closePreviewModal"
        />
      </form>
    </div>
    <button
      type="submit"
      class="btn btn-success mb-5"
      v-if="formData.PernyataanKebenaran && isFormValid"
      @click="submitForm"
    >
      Submit
    </button>
  </div>
</template>

<script>
import ReviewData from "./ReviewData.vue";

export default {
  components: {
    ReviewData,
  },

  data() {
    return {
      formData: {
        Nama: "",
        NIK: null,
        KK: null,
        FotoKTP: null,
        FotoKK: null,
        Umur: null,
        Gender: "",
        Alamat: "",
        RT: "",
        RW: "",
        Before: null,
        After: null,
        Alasan: "",
        AlasanLainnya: "",
        selectedProvince: "",
        selectedRegencies: "",
        selectedDistricts: "",
        selectedvillages: "",
      },
      villages: [],
      districts: [],
      regencies: [],
      provinces: [],
      showPreviewModal: false,
      isFormValid: false,
      cachedData: {},
    };
  },
  mounted() {
    this.fetchProvinces();
  },
  methods: {
    async fetchProvinces() {
      try {
        if (!this.cachedData.provinces) {
          const response = await fetch(
            "https://www.emsifa.com/api-wilayah-indonesia/api/provinces.json"
          );
          const provinces = await response.json();
          this.cachedData.provinces = provinces;
        }
        this.provinces = this.cachedData.provinces;
      } catch (error) {
        console.error("Error fetching provinces:", error);
      }
    },
    async onProvinsiChange() {
      try {
        const selectedProvinceId = this.provinces.find(
          (province) => province.name === this.formData.selectedProvince
        )?.id;

        const response = await fetch(
          `https://www.emsifa.com/api-wilayah-indonesia/api/regencies/${selectedProvinceId}.json`
        );
        const regencies = await response.json();
        this.regencies = regencies;
      } catch (error) {
        console.error("Error fetching regencies:", error);
      }
    },

    async onRegenciesChange() {
      try {
        const selectedRegenciesId = this.regencies.find(
          (regenci) => regenci.name === this.formData.selectedRegencies
        )?.id;

        const response = await fetch(
          `https://www.emsifa.com/api-wilayah-indonesia/api/districts/${selectedRegenciesId}.json`
        );
        const districts = await response.json();

        this.districts = districts;
      } catch (error) {
        console.error("Error fetching regencies:", error);
      }
    },

    async onDistrictsChange() {
      try {
        const selectedDistrictsId = this.districts.find(
          (distric) => distric.name === this.formData.selectedDistricts
        )?.id;

        const response = await fetch(
          `https://www.emsifa.com/api-wilayah-indonesia/api/villages/${selectedDistrictsId}.json`
        );
        const villages = await response.json();

        this.villages = villages;
      } catch (error) {
        console.error("Error fetching Districts:", error);
      }
    },

    handleFileChange(fileType) {
      const fileInput = this.$refs[fileType];
      const file = fileInput.files[0];

      if (file) {
        const maxFileSize = 2; // MB
        const allowedFileTypes = [
          "image/jpeg",
          "image/jpg",
          "image/png",
          "image/bmp",
        ];

        if (file.size / (1024 * 1024) > maxFileSize) {
          // File terlalu besar
          console.error(
            "Ukuran file terlalu besar. Maksimum: " + maxFileSize + "MB"
          );
        } else if (!allowedFileTypes.includes(file.type)) {
          // Tipe file tidak diizinkan
          console.error(
            "Tipe file tidak diizinkan. Pilih file dengan tipe: " +
              allowedFileTypes.join(", ")
          );
        } else {
          console.log("File valid:", file.name);
          this.formData[fileType] = file;
        }
      }
    },

    openPreviewModal() {
      // Buka modul tampilan preview
      this.showPreviewModal = true;
    },

    closePreviewModal() {
      // Tutup modul tampilan preview
      this.showPreviewModal = false;
    },
    checkFormValidity() {
      // Anda dapat menyesuaikan ini sesuai dengan kebutuhan formulir Anda
      const requiredFields = [
        "Nama",
        "Umur",
        "Gender",
        "NIK",
        "KK",
        "FotoKTP",
        "FotoKK",
        "Umur",
        "Gender",
        "Alamat",
        "RT",
        "RW",
        "Before",
        "After",
        "Alasan",
        "selectedProvince",
        "selectedRegencies",
        "selectedDistricts",
        "selectedvillages",
      ];

      return requiredFields.every((field) => this.formData[field]);
    },
    getPhotoUrl(file) {
      if (file instanceof File) {
        return URL.createObjectURL(file);
      } else if (typeof file === "string") {
        return file;
      } else {
        return null;
      }
    },

    async submitForm() {
      try {
        // Simulasi waktu respons server menggunakan async/await
        await new Promise((resolve) => setTimeout(resolve, 1500));

        // Simulasi sukses atau gagal menggunakan Math.random()
        if (Math.random() > 0.5) {
          alert("Data berhasil dikirim!");
        } else {
          alert("Gagal mengirim data. Silakan coba lagi.");
        }
      } catch (error) {
        console.error("Error:", error);
      }
    },
  },
  watch: {
    formData: {
      deep: true,
      handler() {
        this.isFormValid = this.checkFormValidity();
      },
    },
  },
};
</script>
