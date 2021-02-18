<template>
    <div class="posts">
        <div class="container mt-5">
            <div class="row justify-content-center">
                <div class="col-md-12">
                    <div class="card">
                        <div class="card-header" v-for="(post) in weddings" :key="post.id">
                            <h1>{{ post.nama_lengkap_pria }}</h1>
                        </div>
                        <div class="card-body">
                            <router-link :class="['btn btn-md btn-success mb-2']" to="/create">TAMBAH DATA WEDDING</router-link>
                            <hr>

                            <div class="table-responsive mt-2">
                                <table class="table table-hover table-bordered">
                                    <thead>
                                    <tr>
                                        <th>Nama Pria</th>
                                        <th>Panggilan Pria</th>
                                        <th>Asal Pria</th>
                                        <th>Orang tua Pria</th>
                                        <th>Nama Wanita</th>
                                        <th>Panggilan Wanita</th>
                                        <th>Asal Wanita</th>
                                        <th>Orang tua Wanita</th>
                                        <th>Ket. Akad</th>
                                        <th>Waktu Akad</th>
                                        <th>Ket. Resepsi</th>
                                        <th>Waktu Resepsi</th>
                                        <th>H. Pernikahan</th>
                                        <th>Tgl Pernikahan</th>
                                        <th>ket. Tempat</th>
                                        <th>Alamat Lengkap</th>
                                        <th>Google Maps</th>
                                        <th>Google Maps Direction</th>
                                        <th>Google Calendar</th>
                                        <th>Judul Undangan</th>
                                        <th>Kalimat Undangan</th>
                                        <th>Text Undangan</th>
                                        <th>doa Pernikahan</th>
                                        <th>Video Pernikahan</th>
                                    </tr>
                                    </thead>
                                    <tbody>
                                    <tr v-for="(post, index) in weddings" :key="post.id">
                                        <td>{{ post.nama_lengkap_pria }}</td>
                                        <td>{{ post.nama_panggilan_pria }}</td>
                                        <td>{{ post.asal_pria }}</td>
                                        <td>{{ post.orangtua_pria }}</td>
                                        <td>{{ post.nama_lengkap_wanita }}</td>
                                        <td>{{ post.nama_panggilan_wanita }}</td>
                                        <td>{{ post.asal_wanita }}</td>
                                        <td>{{ post.orangtua_wanita }}</td>
                                        <td>{{ post.ket_akad }}</td>
                                        <td>{{ post.waktu_akad }}</td>
                                        <td>{{ post.ket_resepsi }}</td>
                                        <td>{{ post.waktu_resepsi }}</td>
                                        <td>{{ post.hari_pernikahan }}</td>
                                        <td>{{ post.tgl_pernikahan }}</td>
                                        <td>{{ post.ket_tempat }}</td>
                                        <td>{{ post.alamat_lengkap }}</td>
                                        <td>{{ post.google_maps }}</td>
                                        <td>{{ post.google_maps_direction }}</td>
                                        <td>{{ post.google_calendar }}</td>
                                        <td>{{ post.judul_undangan }}</td>
                                        <td>{{ post.kalimat_udangan }}</td>
                                        <td>{{ post.text_undangan }}</td>
                                        <td>{{ post.doa_pernikahan }}</td>
                                        <td>{{ post.video_pernikahan }}</td>
                                        <td class="text-center">
                                            <router-link :to="{name: 'edit', params: { id: post.id }}" class="btn btn-sm btn-primary mr-2">EDIT</router-link>
                                            <button @click.prevent="PostDelete(post.id, index)" class="btn btn-sm btn-danger">HAPUS</button>
                                        </td>
                                    </tr>
                                    </tbody>
                                </table>
                            </div>

                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'

    export default {

        data() {
            return {
                weddings: []
            }
        },
        created() {
            axios.get('http://localhost:8080/api/wedding').then(response => {
                this.weddings = response.data.data;
            });
        },
        methods: {
            PostDelete(id, index)
            {
                axios.delete(`http://localhost:8080/api/wedding/${id}`)
                    .then(response => {
                        this.weddings.splice(index, 1);
                        console.log(response);
                    }).catch(error => {
                    console.log(error.response);
                });
            }
        }
    }
</script>