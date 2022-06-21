<template>
  <div class="container static p-2">
    <input
      class="fixed bottom-5 z-10 opacity-0"
      ref="imgInput"
      type="file"
      accept="image/*"
      @change="uploadImg($event)"
      multiple
    />
    <span>
      <img
        src="/src/assets/DownloadPhoto.png"
        alt="Download"
        class="w-10 fixed bottom-3 left-40"
      />
    </span>
    <div>
      <ul class="columns-3 gap-2" v-show="isUpload">
        <li v-for="(list, index) in img" :key="list">
          <img class="rounded-lg mt-2" ref="imgimg" :src="list.url" alt="" />
          <!-- <button class="remove" @click="remove(index)">Удалить</button> -->
        </li>
      </ul>
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
      // console.log(e.target.files);
      this.isUpload = true;
      let file = e.target.files[0];
      let url = "";
      var reader = new FileReader();
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
    // remove(index) {
    //   this.imgUrl.splice(index, 1);
    // },
  },
};
</script>
