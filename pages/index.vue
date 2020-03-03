<template>
  <div class="container">
    <div >
      <div ref="pdf">
      <logo />
      <h1 class="title">
        NuxtJs-generatePDF
      </h1>
      <h2 class="subtitle">
        Generate PDF with NuxtJs
      </h2>
      </div>
      <div>
      <button @click="generatePDF()" class="button--green" style="font-size:20px">
        Generate PDF
      </button>
    </div>
    </div>
    
  </div>
</template>

<script>
  import Logo from '~/components/Logo.vue'

  export default {
    components: {
      Logo
    },
    methods: {
      generatePDF() {
        if (process.browser) {
          const jsPDF = require('jspdf')
          const html2canvas = require("html2canvas")
          var e = this.$refs.pdf;
          var e_width = e.offsetWidth;
          var e_height = e.offsetHeight;
          var e_x_offset = window.scrollX + e.getBoundingClientRect().left;
          var e_y_offset = window.scrollY + e.getBoundingClientRect().top;
          html2canvas(e, {
            scale: 0.8,
            width: e_width,
            height: e_height,
            x: e_x_offset,
            y: e_y_offset
          }).then(function (canvas) {
            var doc = new jsPDF();
            const img = canvas.toDataURL("image/png"); 
            doc.addImage(img, 'PNG', 10, 10);
            doc.save("sample.pdf");
          });
        }
      }
    }
  }

</script>

<style>
  .container {
    margin: 0 auto;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  .title {
    font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
      'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
    display: block;
    font-weight: 300;
    font-size: 100px;
    color: #35495e;
    letter-spacing: 1px;
  }

  .subtitle {
    font-weight: 300;
    font-size: 42px;
    color: #526488;
    word-spacing: 5px;
    padding-bottom: 15px;
  }

  .links {
    padding-top: 15px;
  }

</style>
