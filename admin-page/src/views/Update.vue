<template>
  <div class="update">
    <h1>Update</h1>
    <form>
      <input
        type="text"
        v-model="post.name"
        placeholder="Navn på øl"
        required
      />
      <label for="kategori">Vælg øl kategori:</label>
      <select
        id="kategori"
        v-model="post.category"
        required
      >
    <option value="Juleøl">Jule øl</option>
    <option value="IpA">IPA</option>
    <option value="Stout">Stout</option>
    <option value="Belgisk Ale">Belgisk ale</option>
    <option value="Porter">Porter</option>
    <option value="Barley Wine">Barley wine</option>
    <option value="Hvedeøl">Hvede øl</option>
    <option value="Lager">Lager</option>
    <option value="Sour">Sour</option>
      </select><br>
      <input
        type="text"
        v-model="post.description"
        placeholder="Beskrivelse af øl"
        required
      />
      <input
        type="text"
        v-model="post.cl"
        placeholder="cl af øl"
        required
      />
      <input
        type="text"
        v-model="post.alc"
        placeholder="alc af øl"
        required
      />
      <input
        type="text"
        v-model="post.pris"
        placeholder="pris på øl"
        required
      />
      <input
        type="file"
        ref="fileInput"
        accept="image/*"
        v-on:change="previewImage"
      />
      <button class="choose-image" type="button" v-on:click="triggerChooseImg">
        Vælg billede
      </button>
      <div>
        <img :src="post.image" class="image-preview" />
      </div>
      <button class="example_a" type="button" v-on:click="updatePost">Opdater produkt</button>
    </form>
  </div>
</template>

<script>
import { postRef } from "../firebase-db";
export default {
  name: "Update",
  props: {
    post: Object
  },
  methods: {
    triggerChooseImg() {
      this.$refs.fileInput.click();
    },
    previewImage() {
      const imageFile = this.$refs.fileInput.files[0];
      const fileReader = new FileReader();
      fileReader.onload = event => {
        this.post.image = event.target.result;
      };
      fileReader.readAsDataURL(imageFile);
    },
    updatePost() {
      console.log(this.post);

      postRef.doc(this.post.id).set({
        description: this.post.description,
        image: this.post.image,
        name: this.post.name,
        category: this.post.category

      });

      this.$router.push("/");
    }
  }
};
</script>

<style scoped>
form {
  padding: 2em 1em 2.5em;
}

button.choose-image {
  background-color: var(--primary);
}

/* article button {
  text-align: center;
  cursor: pointer;
  border: none;
  padding: 10px 8px;
  border-radius: 0;
  color: var(--text-color-light);
  background-color: var(--green);
  width: 40%;
} */

input {
  margin: 1em auto;
  width: 100%;
  max-width: 350px;
  padding: 12px 15px;
  box-sizing: border-box;
  display: block;
}

input[type="file"] {
  display: none;
}

.image-preview {
  max-width: 350px;
  width: 100%;
  padding: 1em 0;
}
.example_a {
color: #fff !important;
text-transform: uppercase;
text-decoration: none;
background: lightblue;
padding: 15px;
border-radius: 5px;
display: inline-block;
border: none;
transition: all 0.4s ease 0s;
margin: 1%;
}

.example_a:hover {
background: #434343;
letter-spacing: 1px;
-webkit-box-shadow: 0px 5px 40px -10px rgba(0,0,0,0.57);
-moz-box-shadow: 0px 5px 40px -10px rgba(0,0,0,0.57);
box-shadow: 5px 40px -10px rgba(0,0,0,0.57);
transition: all 0.4s ease 0s;
}
</style>
