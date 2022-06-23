<template>
  <div class="container relative mx-auto p-2">
    <div class="flex justify-center">
      <input
        class="fixed bottom-5 z-10 opacity-0"
        type="file"
        id="files"
        ref="files"
        accept="image/*"
        multiple
        v-on:change="uploadImg()"
      />
      <span>
        <img
          src="/src/assets/DownloadPhoto.png"
          alt="Download"
          class="w-10 fixed bottom-3 bg-slate-200 rounded-lg"
        />
      </span>
    </div>

    <div>
      <div class="columns-3 gap-2">
        <div v-for="(file, key) in files">
          <img class="rounded-lg mb-2" v-bind:ref="'image' + parseInt(key)" />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      files: [],
    };
  },
  methods: {
    uploadImg() {
      let uploadedFiles = this.$refs.files.files;
      for (var i = 0; i < uploadedFiles.length; i++) {
        this.files.push(uploadedFiles[i]);
      }
      this.getImagePreviews();
    },
    getImagePreviews() {
      for (let i = 0; i < this.files.length; i++) {
        if (/\.(jpe?g|png|gif)$/i.test(this.files[i].name)) {
          let reader = new FileReader();
          reader.addEventListener(
            "load",
            function () {
              this.$refs["image" + parseInt(i)][0].src = reader.result;
            }.bind(this),
            false
          );
          reader.readAsDataURL(this.files[i]);
        }
      }
    },
  },
};
</script>
