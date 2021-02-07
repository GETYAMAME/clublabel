<template>
  <v-app>
    <v-main>
      <v-container>
        <v-row justify="center">
          <v-col cols="2"></v-col>
          <v-col cols="8">
            <p><canvas id="preview"></canvas></p>            
            <v-card>
              <v-card-title><input type="file" ref="preview" @change="uploadFile"></v-card-title>    
            </v-card>
            <br>
            <v-text-field id="canvas_text" label="設定したい文字を入力してください（例：作業中、移動中など）" value="作業中"></v-text-field>
            <v-btn
              color="secondary"
              depressed
              elevation="2"
              large
              @click="drawText('preview', 'canvas_text');"
            >文字を描く</v-btn>
          </v-col>
          <v-col cols="2"></v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  components: {
    Logo,
    VuetifyLogo
  },
  methods: {
    uploadFile(){
      const file = this.$refs.preview.files[0];
      this.url = URL.createObjectURL(file)
      
      var image = new Image();
      image.src = this.url;
      image.onload = (function () {
        //画像ロードが完了してからキャンバスの準備をする
        var canvas = document.getElementById("preview");
        var ctx = canvas.getContext('2d');
        //キャンバスのサイズを画像サイズに合わせる
        canvas.width = image.width;
        canvas.height = image.height;
        //キャンバスに画像を描画（開始位置0,0）
        ctx.drawImage(image, 0, 0);
      });
    },
    drawText (canvas_id,text_id) {
      var canvas = document.getElementById(canvas_id);
      var ctx = canvas.getContext('2d');
      var text = document.getElementById(text_id);
      //文字のスタイルを指定
      ctx.font = '32px serif';
      ctx.fillStyle = '#404040';
      //文字の配置を指定（左上基準にしたければtop/leftだが、文字の中心座標を指定するのでcenter
      ctx.textBaseline = 'center';
      ctx.textAlign = 'center';
      //座標を指定して文字を描く（座標は画像の中心に）
      var x = (canvas.width / 2);
      var y = (canvas.height / 2);
      ctx.fillText(text.value, x, y);
   },
 },
}
</script>
