<template>
  <div class="wrapper-row">
    <div class="wrapper img">
      <div class="row-item" 
      v-for="photo_url in PhotosUrl" 
      :key="photo_url.url">
        <img
          :src="photo_url.url"
          :alt="photo_url.description"
          @click="selectedPhotos(photo_url)"
        />
        <div class="item-deskription">
          <span>id:{{ photo_url.id }}</span>
          <p>{{ photo_url.description }}</p>
        </div>
      </div>
    </div>
    <div class="wrapper user">
        <div 
          v-for="user in users" 
          :key="user.id"
          >
           <button
            @click ="user_active = user.id"
           >
            {{ user.name }}
          </button>

          <img
             v-for="(selectedPhoto, index) in user.selectedPhotos"
             :src="selectedPhoto"
             :key="index"
         />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  beforeCreate() {
    console.clear();
  },
  data() {
    return {
      photosID: [],
      postitemsphotos: {},
      result_click: "",
      PhotosUrl: [],
      users: [
        { id: 1, name: "User 1", selectedPhotos: [] },
        { id: 2, name: "User 2", selectedPhotos: [] },
      ],
      user_active: null,
    };
  },
  async mounted() {
    await this.requestApi();
  },
  methods: {
    async requestApi() {
      try {
        const response = await fetch("/galery.json");
        this.postitemsphotos = await response.json();
        //this.postitemsphotos = this.postitemsphotos.slice(0, 15);
        //console.log(this.postitemsphotos);
        let message = this.postitemsphotos.message;
        //console.log(message);
        let title_photos = this.postitemsphotos.total_photos;
        //console.log(title_photos);
        this.photosID = this.postitemsphotos.photos;
        //console.log(this.photosID);
        this.PhotosUrl = this.postitemsphotos.photos;
        //console.log(this.PhotosUrl);
      } catch (error) {
        console.error("Ошибка загрузки:", error);
      }
    },
    selectedPhotos(selectedPhoto) {
        if (!this.user_active) {
          alert("Выберите пользователя");
          //return;
        } else {
            //console.log(this.user_active);
        }
        const user = this.users.find((k) => k.id === this.user_active);
        // console.log(user);

    },
  },
};
</script>

<style>
.wrapper {
  display: flex;
  flex-direction: column;
}
.wrapper-row {
  display: flex;
}
.wrapper.user {
  margin-left: 1%;
  display: flex;
  flex-direction: row;
  max-width: 200px;
  width: 100%;
  justify-content: space-between;
}
.wrapper.img {
  max-width: 400px;
  width: 100%;
}
.row {
  display: flex;
}
.row-item {
  display: flex;
  align-items: center;
}
.row-item img {
  max-width: 200px;
  width: 100%;
  height: 200px;
  object-fit: cover;
}
.item-deskription {
  display: flex;
  flex-direction: column;
}
.res_click {
  max-width: 300px;
  width: 100%;
  font-size: 14px;
}

</style>
