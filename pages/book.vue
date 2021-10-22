<template>
  <v-container fluid>
    <v-data-iterator
      :items="items"
      :items-per-page.sync="itemsPerPage"
      :page.sync="page"
      :search="search"
      :sort-by="sortBy.toLowerCase()"
      :sort-desc="sortDesc"
      hide-default-footer
    >

      <template v-slot:default="props">
        <v-row>
          <v-col
            v-for="item in props.items"
            :key="item.name"
            cols="12"
          >
            <v-card>
              <v-card-title class="subheading font-weight-bold">
                {{ item.name }}
              </v-card-title>

              <v-divider></v-divider>

              <v-list dense>
                <v-list-item
                  v-for="(key, index) in filteredKeys"
                  :key="index"
                >
                  <v-list-item-content
                    class="align-end"
                    :class="{ 'blue--text': sortBy === key }"
                  >
                    {{ item[key.toLowerCase()] }}
                  </v-list-item-content>
                </v-list-item>
              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </template>

      <template v-slot:footer>
        <v-row
          class="mt-2"
          align="center"
          justify="center"
        >
          <v-spacer></v-spacer>

          <span
            class="mr-4
            grey--text"
          >
            Page {{ page }} of {{ numberOfPages }}
          </span>
          <v-btn
            fab
            dark
            color="blue darken-3"
            class="mr-1"
            @click="formerPage"
          >
            <v-icon>mdi-chevron-left</v-icon>
          </v-btn>
          <v-btn
            fab
            dark
            color="blue darken-3"
            class="ml-1"
            @click="nextPage"
          >
            <v-icon>mdi-chevron-right</v-icon>
          </v-btn>
        </v-row>
      </template>
    </v-data-iterator>
  </v-container>
</template>

<script>
  export default {
    data () {
      return {
        itemsPerPageArray: [4, 8, 12],
        search: '',
        filter: {},
        sortDesc: false,
        page: 1,
        itemsPerPage: 1,
        sortBy: 'name',
        keys: [
          'Name',
          'Judul1',
          'Text1',
          'Judul2',
          'Text2',
        ],
        items: [
          {
            name: 'Page 1',
            judul1: 'Pengertian, Struktur dan Contoh Teks Prosedur',
            text1: 'Teks prosedur adalah sebuah teks yang terdiri mengenai tahapan-tahapan atau langkah untuk melakukan suatu hal. Hal ini bisa menjadi apa saja, baik menyusun sesuatu yang nantinya akan disajikan secara urut atau bisa juga melakukan suatu aktivitas tertentu.Teks prosedur kompleks sebenarnya sering kali kita jumpai pada kehidupan sehari-hari namun mungkin kita yang belum menyadarinya. Oleh karena itu pada pertemuan kali ini mari kita bahas bersama-sama tentang kalimat prosedur kompleks agar sobat bisa lebih memahaminya lagi.',
            judul2: 'Pengertian Teks Prosedur Kompleks ',
            text2: 'Teks prosedur kompleks adalah teks yang berisi tentang tahap-tahap atau proses-proses dari kegiatan untuk menyelesaikan suatu hal. Dengan kata lain, teks prosedur teks adalah teks yang memberikan penjelasan tentang langkah-langkah atau serangkaian proses untuk melakukan hal-hal yang mungkin belum diketahui orang banyak. Pada teks prosedur kompleks penjelasan akan proses-prosesnya dijelaskan secara berurutan dari awal hingga akhir proses tersebut.'
          },
          {
            name: 'Page 2',
            judul1: 'Struktur Teks Prosedur Kompleks ',
            text1: 'Semua bentuk teks pada umumnya pasti memiliki struktur pembangunnya karena tanpa struktur, teks tak akan terbentuk dengan baik dan sulit dipahami. Adapun struktur pada teks prosedur kompleks antara lain adalah sebagai berikut. 1.	Bagian Tujuan: Pada bagian tujuan berisi tentang tujuan dari pembuatan teks tersebut serta hasil yang akan dicapai nantinya. Bagian tujuan dapat berupa judul. 2.	Bagian Material: Pada bagian ini penulis memberikan informasi mengenai alat dan bahan yang akan digunakan dan harus dipersiapkan. Namun tidak semua teks prosedur terdapat bagian material. 3.	Bagian Langkah-langkah Pada bagian ini berisi tentang langkah-langkah atau cara-cara yang harus ditempuh untuk mencapai hasil yang diinginkan. Cara-cara tersebut dijelaskan secara berurutan dari awal hingga akhir.',
            judul2: 'Ciri dan Kaidah Kebahasaan Teks Prosedur Kompleks ',
            text2: '1.	Konjungsi: Konjungsi merupakan kata penghubung yang digunakan untuk menghubungkan antar kalimat agar menjadi satu kesatuan yang baik dan mudah dipahami. Konjungsi yang sering digunakan pada teks prosedur kompleks antara lain lalu, selanjutnya, pertama-tama, dan lain-lain yang penting merupakan konjungsi waktu. 2.	Kata Kerja Imperatif: Di dalam teks prosedur sangat banyak dikunjungi kata kerja imperatif atau perinta yaitu kata-kata yang menyatakan perintah yang harus dilakukan. 3.	Verba Material dan Tingkah Laku: Verba material adalah verba yang mengacu pada tindakan fisik. Seddangkan verba  tingkah laku adalah verba yang menyatakan tindakan yang dilakukan dengan pernyataan. 4.	Partisipan Manusia: Pada aspek ini secara umum kita cukup mengoreksi apabila pada teks yang disunting terdapat partisipan manusia dan partisipan manusia itu bukan secara khusus. Adapun ciri-cirinya sebagai berikut. 1.	Disusun secara informatif, 2.	Teks berisikan langkah-langkah, 3.	Bersifat objektif, 4.	Penjelasannya secara rinci, 5.	Langkah berkelanjutan dengan penjelasan, 6.	Menggunakan syarat pilihan, 7.	bersifat aktual dan akurat, 8.	Teks mengandung unsur logis, 9.	Bersifat umum dan universal.',
          },
          {
            name: 'Page 3',
            judul1: 'Cara Membuat Nasi Goreng',
            text1: 'Membuat nasi goreng sebenarnya bukanlah hal yang sulit, hanya saja perlu kemampuan khusus serta pemahaman yang lebih agar nasi goreng yang dibuat memiliki rasa yang lezat. Untuk membuat nasi goreng yang nikmat diperlukan bahan-bahan yang tepat dengan takaran yang tepat. Maka dari itu mari sebelum membuat nasi goreng yang nikmat anda harus menyiapkan bahan-bahan berikut ini.Bahan-bahan: 1.	2 piring nasi putih jangan terlalu pulen, 2.	3 butir telur, 3.	3 siung bawang merah, 4.	Garam secukupnya, 5.	2 siung bawang putih, 6.	5-6 buah cabai rawit, 7.	1 batang daun bawang, 8.	1 sdm merica, 9.	2 sendok mentega, 10.	Saus tomat secukupnya, 11.	bahan pelengkap: sosis, daging ayam, udang, bakso, sesuai selera, dll.',
            judul2: 'Cara Membuat: 1.	Siapkan penggorengan dan masukan mentega, setelah itu panaskan mentega dengan api sedang. 2.	Setelah mentega mencair dan telah panas lalu masukan bawang putih, bawang merah, dan cabai hingga matang dan mengeluarkan aroma harum. 3.	Kemudian masukan bahan pelengkap yang telah disiapkan dengan takaran sesuai selera anda, aduk terus hingga merata dan matang. 4.	Selanjutnya masukan telur dan aduk terus agar telur menjadi orak arik. 5.	Setelah itu masukan nasi putih dan aduk terus sampai merata tercampur dengan semua bahan. 6.	Selanjutnya tambahkan garam, saus tomat dan mentega lalu aduk kembali hingga merata. 7.	Apabila nasi telah terlihat merata dan mengeluarkan aroma harum, angkat nasi lalu sajikan atas piring. 8.	Nasi goreng pun siap untuk untuk disantap pada keadaan hangat.',
            text2: '',
          },
          {
            name: 'Page 4',
            judul1: 'Cara Mematikan Laptop',
            text1: 'Mematikan laptop adalah kewajiban setiap orang yang telah menghidupkan laptop. Namun saat ini masih banyak yang kebingungan tentang cara mematikan laptop padahal caranya cukup mudah sekali. Prosedur dalam mematikan laptop harus diikuti agar laptop dapat awet dan tak mudah rusak. Oleh  karena itu mari ikuti langkah-langkah dibawah ini.',
            judul2: '1.	Tutup semua aplikasi yang sedang dibuka. 2.	Arahkan kursor ke arah tombol Start lalu klik. 3.	Setelah itu klik turn off computer. 4.	Setelah itu akan muncul perintah, lalu klik shut down. 5.	Tunggu sebentar lalu laptop akan mati dengan sendirinya. 6.	Selanjutnya tutup laptop dan letakan pada tempat yang aman.',
            text2: '',
          },
          {
            name: 'Page 5',
            judul1: 'Cara Membuat Teks Prosedur  ',
            text1: 'Berikut ini langkah penulisan dalam membuat teks prosedur kompleks yang baik dan benar: 1.	Menentukan topik apa yang akan dibuat. 2.	Mengumpulkan sumber informasi dan menulis kerangka karangan. 3.	Mengembangkan informasi yang telah didapat dan memikirkan langkah-langkahnya. 4.	Menentukan judul. 5.	Menyusun teks prosedur kompleks secara utuh',
            judul2: 'Adapun hal yang harus kamu perhatikan ketika membuat teks prosedur kompleks: 1.	Kalimat yang digunakan sesuai dengan karakteristik teks prosedur kompleks. 2.	Langkah-langkah atau instruksi yang diberikan kepada pembaca harus jelas. 3.	Bahasa yang digunakan pas dengan karakteristik pembaca. 4.	Urutan langkah-langkah harus sistematis.',
            text2: '',
          }
        ],
      }
    },
    computed: {
      numberOfPages () {
        return Math.ceil(this.items.length / this.itemsPerPage)
      },
      filteredKeys () {
        return this.keys.filter(key => key !== 'Name')
      },
    },
    methods: {
      nextPage () {
        if (this.page + 1 <= this.numberOfPages) this.page += 1
      },
      formerPage () {
        if (this.page - 1 >= 1) this.page -= 1
      },
      updateItemsPerPage (number) {
        this.itemsPerPage = number
      },
    },
  }
</script>