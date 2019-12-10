<template>
  <div class="container column is-fullheight-with-navbar">
    <label class="label">Host</label>
    <div class="control">
      <div class="field has-addons">
        <p class="button is-static">
          http://
        </p>
        <p class="control has-icons-left">
          <label>
            <input
              class="input"
              type="text"
              placeholder="example.local/upload"
              v-model="host"
            />
          </label>
          <span class="icon is-small is-left">
            <i class="fas fa-link"></i>
          </span>
        </p>
        <button v-on:click="addHosts()" class="button info">Add</button>
      </div>
    </div>

    <div class="file">
      <label class="file-label">
        <input
          class="file-input"
          v-on:change="onFileChanged"
          type="file"
          name="resume"
        />
        <span class="file-cta">
          <span class="file-icon">
            <i class="fas fa-upload"></i>
          </span>
          <span class="file-label">
            Choose a file…
          </span>
        </span>
        <span class="file-name">
          {{ file_name }}
        </span>
      </label>
    </div>
    <div class="control">
      <input
        type="button"
        class="button is-primary"
        v-on:click="fileUpload()"
        value="Submit"
      />
      <p class="help">
        {{ this.upload_status }}
      </p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'UploadForm',
  data() {
    return {
      file: {},
      file_name: 'Supports *jpg, *png, *.gif',
      headers: {
        'Access-Control-Allow-Origin': '*'
      },
      hosts: [],
      host: '',
      upload_status: 'Status'
    }
  },
  methods: {
    onFileChanged: function(e) {
      e.preventDefault()
      const files = e.target.files || e.dataTransfer.files
      this.file = files[0]
      this.file_name = files[0].name
    },
    async postData(address, formData) {
      try {
        await axios.post(`http://${address.text}:5000/upload`, formData, {
          headers: {
            'content-type': 'multipart/form-data'
          }
        })
      } catch (e) {
        // eslint-disable-next-line no-console
        console.log(e.toString())
      }
    },
    async fileUpload() {
      const urls = this.hosts
      const formData = new FormData()
      formData.append('file', this.file)
      await Promise.all(urls.map(address => this.postData(address, formData)))
    },
    addHosts: function() {
      const host = this.host
      this.hosts.push({
        text: host.toString()
      })
      this.host = ''
    }
  }
}
</script>

<style scoped></style>
