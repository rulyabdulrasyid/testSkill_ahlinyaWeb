<template>
  <div>
    <div>
      <h3>Data yang akan di-submit:</h3>
      <ul>
        <li><strong>Nama:</strong> {{ formData.Nama }}</li>
        <li><strong>NIK:</strong> {{ formData.NIK }}</li>
        <li><strong>Nomor KK:</strong> {{ formData.KK }}</li>
        <li>
          <strong>Foto KTP:</strong>
          <img
            :src="getPhotoUrl(formData.FotoKTP)"
            class="img-thumbnail"
            alt="Foto KTP"
            style="width: 200px; height: 200px"
          />
        </li>
        <li>
          <strong>Foto KK:</strong>
          <img
            :src="getPhotoUrl(formData.FotoKK)"
            class="img-thumbnail"
            alt="Foto KK"
            style="max-height: 200px"
          />
        </li>
        <li><strong>Umur:</strong> {{ formData.Umur }}</li>
        <li><strong>Provinsi:</strong> {{ formData.selectedProvince }}</li>
        <li><strong>Kab/Kota:</strong> {{ formData.selectedRegencies }}</li>
        <li><strong>Kecamatan:</strong> {{ formData.selectedDistricts }}</li>
        <li>
          <strong>Kelurahan/Desa:</strong> {{ formData.selectedvillages }}
        </li>
        <li><strong>Alamat:</strong> {{ formData.Alamat }}</li>
        <li><strong>RT:</strong> {{ formData.RT }}</li>
        <li><strong>RW:</strong> {{ formData.RW }}</li>
        <li>
          <strong>Penghasilan Sebelum Pandemi:</strong> {{ formData.Before }}
        </li>
        <li>
          <strong>Penghasilan Setelah Pandemia:</strong> {{ formData.After }}
        </li>
        <li>
          <strong>Alasan Membutuhkan Bantuan:</strong> {{ formData.Alasan }}
        </li>
      </ul>
    </div>
    <button @click="goBack" class="btn btn-danger">Kembali</button>
  </div>
</template>

<script>
export default {
  props: {
    formData: Object,
  },
  methods: {
    goBack() {
      this.$emit("close");
    },
    getPhotoUrl(file) {
      if (file instanceof File) {
        // Mengonversi File ke URL menggunakan URL.createObjectURL
        return URL.createObjectURL(file);
      } else if (typeof file === "string") {
        // Menggunakan nilai yang sudah berupa URL (jika sudah diatur sebelumnya)
        return file;
      } else {
        return null;
      }
    },
  },
};
</script>
