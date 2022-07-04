<template>
  <D3BarChart :config="config" :datum="data"></D3BarChart>
</template>

<script>
import { D3WordsCloud } from 'vue-d3-charts';
import axios from 'axios'

export default {
  name: 'WordsCloud',
  components: {
    D3WordsCloud,
  },
  mounted () {
    axios.get('http://localhost:8888/datas').then(res => {
      res.data.forEach(res => {
        let filename = res.path.replace('http://localhost:8888/', '')
        let id = filename.replace('.json', '')
        var file = {size: res.size, name: filename, type: "image/png", upload: {uuid: id}}
        this.$refs.myVueDropzone.manuallyAddFile(file, res.path)
      })
    }).catch(err => {
      console.error(err)
    })
  },
  methods: {
    sendingEvent: function (file, xhr, formData) {
      formData.append('uuid', file.upload.uuid)
    },
    removeEvent: function (file, error, xhr) {
      axios.delete(`http://localhost:8888/datas/${file.upload.uuid}`).then(res => {
        console.log(res.data)
      }).catch(err => {
        console.error(err)
      })
    }
  }
};
</script>
