<template>
  <div class="container column is-10">
    <div class="field">
      <label class="label">Host</label>
      <div class="control">
        <div class="field has-addons">
          <p class="button is-static">
            http://
          </p>
          <p class="control has-icons-left has-icons-right">
            <input
              class="input"
              type="text"
              placeholder="example.local/upload"
              id="server_url"
            />
            <span class="icon is-small is-left">
              <i class="fas fa-link"></i>
            </span>
            <span class="icon is-small is-right">
              <i class="fas fa-link"></i>
            </span>
          </p>
        </div>
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
    fileUpload: function() {
      const url = 'http://' + document.getElementById('server_url').value
      const formData = new FormData()
      formData.append('file', this.file)
      if (url !== 'http://') {
        axios
          .post(url, formData, {
            headers: {
              'content-type': 'multipart/form-data'
            }
          })
          .then(function(response) {
            this.upload_status = response.status.toString()
          })
      }
    }
  }
}
</script>

<style scoped></style>
