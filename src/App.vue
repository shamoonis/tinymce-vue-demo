<template>
  <div id="app">
  <img alt="Vue logo" src="./assets/logo.png">
  <input type="text" class="thaanaKeyboardInput" id="fullname">
  <editor
    class="thaana-keyboard"
    initialValue="<p>Initial editor content</p>"
    :init="{
      height: 500,
      menubar: false,
      plugins: [
        'advlist autolink lists link image charmap',
        'searchreplace visualblocks code fullscreen',
        'print preview anchor insertdatetime media',
        'paste code help wordcount table'
      ],
      toolbar:
        'undo redo | formatselect | bold italic | \
        alignleft aligncenter alignright | \
        bullist numlist outdent indent | help'
    }"
    v-model="value"
  />
  </div>
</template>

<script>
  import Editor from '@tinymce/tinymce-vue'
  import thaanaKeyboard from './jkt.js'

  export default {
    name: 'app',
    components: {
      editor: Editor
    },
    methods: {
            /*
             * Set the initial, internal value for the field.
             */
            setInitialValue() {
                this.value = this.field.value || ''
            },
            /**
             * Fill the given FormData object with the field's internal value.
             */
            fill(formData) {
                formData.append(this.field.attribute, this.value || '')
            },
            /**
             * Update the field's internal value.
             */
            handleChange(value) {
                this.value = value
            },
        },
    mounted(){
      // var ref = this;
      this.init = {
                // images_upload_handler: async function(blobInfo, success, failure) {
                //     let formData = new FormData();
                //     formData.append('file', blobInfo.blob());
                //     formData.append('driver', ref.field.driver);
                //     formData.append('folder', ref.field.folder);
                //     return await window.axios.post(ref.url,
                //         formData,
                //         {
                //             headers: {
                //                 'Content-Type': 'multipart/form-data'
                //             }
                //         }).then(function (response) {
                //             if(ref.field.path !== null){
                //                 success(ref.field.path + response.data.location);
                //             } else {
                //                 success(response.data.location);
                //             }
                //     }).catch(function (error) {
                //         failure(error.statusCode)
                //     })
                // },
      
      setup: function (editor) {
                    thaanaKeyboard.defaultKeyboard = 'phonetic';
                        editor.on('keypress', function (e) {
                          alert("hello")
                            thaanaKeyboard.value = '';
                            thaanaKeyboard.handleKey(e);
                            editor.insertContent(thaanaKeyboard.value);
                        });
                }
      }
    }


  }
</script>

