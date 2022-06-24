<template>
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
      <Camera class="w-10 fixed bottom-3 bg-slate-200 rounded-lg" />
    </span>
  </div>

  <div>
    <div class="columns-3 gap-2">
      <div v-for="(file, key) in files">
        <img class="rounded-lg mb-2" v-bind:ref="'image' + parseInt(key)" />
      </div>
    </div>
  </div>
</template>

<script>
import Camera from "@/components/icons/Camera.vue";
export default {
  data() {
    return {
      files: [],
    };
  },
  components: {
    Camera,
  },
  methods: {
    // этот метод слушает изменения input при загрузке фотографий
    uploadImg() {
      // в переменную uploadedFiles устанавливаю все загруженные фотографии из input
      let uploadedFiles = this.$refs.files.files;
      for (var i = 0; i < uploadedFiles.length; i++) {
        this.files.push(uploadedFiles[i]);
      }
      this.getImagePreviews();
    },
    //данный метод отображает выбранные фотографии
    getImagePreviews() {
      //здесь перебираю все загруженные фотографии которые копируются в переменную files
      for (let i = 0; i < this.files.length; i++) {
        //FileReader слушает событие load
        let reader = new FileReader();
        reader.addEventListener(
          "load",
          function () {
            //здессь ссылаюсь на глобальный объект $refs с помощью ключевой ссылки которая находится в шаблоне. При переборе фотографий
            //индексы совпадают,что позволяет отобразить выбранные фотографии
            this.$refs["image" + parseInt(i)][0].src = reader.result;
            //с помощью .bind(this) связываю значение локального компонента прикрепленный к функции-обработчику
          }.bind(this),
          false
        );
        // readAsDataURL будет читать выбранные файлы по ключу в массиве
        // когда фотография будет загружена запустится событие load и установится src тега
        // фотографии в массиве $refs с индексом в котором он находится
        reader.readAsDataURL(this.files[i]);
      }
    },
  },
};
</script>
