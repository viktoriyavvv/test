<template>
  <div class="container static p-2">
    <input
      class="fixed bottom-5 z-10 opacity-0"
      ref="imgInput"
      type="file"
      multiple
      accept="image/*"
      @change="uploadImg($event)"
    />
    <span>
      <img
        src="/src/assets/DownloadPhoto.png"
        alt="Download"
        class="w-10 fixed bottom-3 left-40"
      />
    </span>

    <div>
      <div class="columns-3 gap-2" v-show="isUpload">
        <div v-for="(list, index) in img" :key="list">
          <img class="rounded-lg mb-2" ref="imgimg" :src="list.url" alt="" />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Images",
  data() {
    return {
      isUpload: false,
      img: [],
    };
  },
  methods: {
    uploadImg(e) {
      this.isUpload = true;
      let file = e.target.files[0];
      let url = "";
      let reader = new FileReader();
      reader.readAsDataURL(file);
      let name = this;
      reader.onload = function (e) {
        url = this.result.substring(this.result.indexOf(",") + 1);
        name.img.push({
          id: name.img.length + 1,
          url: "data:image/png;base64," + url,
        });
      };
    },
  },
};
</script>
