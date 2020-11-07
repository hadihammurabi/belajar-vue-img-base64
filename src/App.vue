<template>
  <b-row>
    <b-col></b-col>
    <b-col lg="4" md="6" sm="10">
      <b-card>
        <b-form-file
          :state="Boolean(image)"
          placeholder="Pilih file..."
          drop-placeholder="Drop file here..."
          @change="onImageSelected"
          accept="image/*"
        ></b-form-file>

        <b-img :src="image" fluid alt="<<image>>"></b-img>
      </b-card>
    </b-col>
    <b-col></b-col>
  </b-row>
</template>

<script>
export default {
  data: () => ({
    image: "https://picsum.photos/1024/720/?image=41",
  }),
  methods: {
    onImageSelected(e) {
      const file = e.target.files[0];
      this.createBase64(file, (result) => {
        this.image = result;
      });
    },

    createBase64(file, onload) {
      const reader = new FileReader();
      reader.onload = (e) => {
        onload(e.target.result);
      };

      reader.readAsDataURL(file);
    }
  },
}
</script>
