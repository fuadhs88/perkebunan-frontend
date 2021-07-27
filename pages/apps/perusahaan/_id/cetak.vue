<template>
    <div>
        <Head 
			title="Cetak" 
			subtitle="Overview sebelum dicetak"
            color="text--black"
			>
			<div>
				<v-btn 
					v-on:click="handelCetak"
					small>
					<v-icon left>mdi-printer-check</v-icon>
					Cetak Sekarang
				</v-btn>
			</div>
		</Head>
        <vue-html2pdf
            options
            :show-layout="true"
            :float-layout="false"
            :enable-download="false"
            :preview-modal="true"
            :html-to-pdf-options="{margin:[10, 0, 10,0]}"
            filename="print perusahaan"
            :paginate-elements-by-height="1500"
            :pdf-quality="2"
            pdf-format="a4"
            pdf-orientation="portrait"
            pdf-content-width="800px"
            :manual-pagination="false"
            ref="html2Pdf">
            <section slot="pdf-content" style="padding:30px;font-family: 'Times New Roman';">
                <!-- start -->
                <!-- <div class="html2pdf__page-break"/> -->
                <h4 class="text-center">
                    LAPORAN KEMAJUAN KEGIATAN PERUSAHAAN PERKEBUNAN PERIODE LAPORAN: TRIWULAN {{ this.triwulan.substr(0,4) }}-{{ this.triwulan.substr(4,1) }}
                </h4>
                <br/>
                <p>
                    <strong>Data Perusahaan :</strong>
                </p>
                <table style="border-collapse: collapse; ">
                    <tbody>
                        <tr>
                            <td width="30px">1. </td>
                            <td width="200px">Nama Perusahaan</td>
                            <td>: {{ perusahaan.nama }}</td>
                        </tr>
                        <tr v-html="templatePerusahaan('2.', 'NPWP','npwp')"/>
                        <tr v-html="templatePerusahaan('3.', 'Status Perusahaan','status_perusahaan')"/>
                        <tr v-html="templatePerusahaan('4.', 'Alamat')"/>
                        <tr v-html="templatePerusahaan('', 'a. &nbsp; Kantor Pusat', 'alamat_kantor_pusat')"/>
                        <tr v-html="templatePerusahaan('', 'b. &nbsp; Kantor Cabang', 'alamat_kantor_cabang')"/>
                        <tr v-html="templatePerusahaan('5.', 'Nama Kebun/ Estate', 'nama_kebun')"/>
                        <tr v-html="templatePerusahaan('6.', 'Lokasi Kebun/ Pabrik')"/>
                        <tr v-html="templatePerusahaan('', 'a. &nbsp; Desa', 'lokasi_kebun_desa')"/>
                        <tr v-html="templatePerusahaan('', 'b. &nbsp; Kecamatan', 'lokasi_kebun_kecamatan')"/>
                        <tr v-html="templatePerusahaan('', 'c. &nbsp; Kabupaten', 'lokasi_kebun_kabupaten')"/>
                        <tr v-html="templatePerusahaan('', 'd. &nbsp; Provinsi', 'lokasi_kebun_provinsi')"/>
                    </tbody>
                </table>
                <br/>
                <p>
                    <strong>LEGALITAS YANG DIPEROLEH</strong>
                </p>
                <p>1. SuratPersetujuan/Perijinan yang diperoleh :</p>
                <div v-html="templateIjinLokasi('a. Ijin Lokasi', 
                                                'lokasi_nomor', 
                                                'lokasi_tanggal', 
                                                'lokasi_luas')"/> 
                <div v-html="templateIjinLokasi('b. Ijin Lokasi Perpanjangan Lokasi 1', 
                                                'lokasi_perpanjangan1_nomor', 
                                                'lokasi_perpanjangan1_tanggal', 
                                                'lokasi_perpanjangan1_luas')"/> 
                <div v-html="templateIjinLokasi('c. Ijin Lokasi Perpanjangan Lokasi 2', 
                                                'lokasi_perpanjangan2_nomor', 
                                                'lokasi_perpanjangan2_tanggal', 
                                                'lokasi_perpanjangan2_luas')"/> 
                <div v-html="templateIjinLokasi('d. Ijin Lokasi Perpanjangan Lokasi 3', 
                                                'lokasi_perpanjangan3_nomor', 
                                                'lokasi_perpanjangan3_tanggal', 
                                                'lokasi_perpanjangan3_luas')"/> 
                <div v-html="templateIjinLokasi('e. IUP/ PPUB', 
                                                'ppub_nomor', 
                                                'ppub_tanggal', 
                                                'ppub_luas')"/> 
                <div v-html="templateIjinLokasi('f. IPL', 
                                                'ipl_nomor', 
                                                'ipl_tanggal', 
                                                'ipl_luas')"/> 
                <div v-html="templateIjinLokasi('g. Perpanjangan IPL', 
                                                'ipl_perpanjangan_nomor', 
                                                'ipl_perpanjangan_tanggal', 
                                                'ipl_perpanjangan_luas')"/> 
                <div v-html="templateIjinLokasi('h. IPL tahap 2', 
                                                'ipl2_nomor', 
                                                'ipl2_tanggal', 
                                                'ipl2_luas')"/> 
                <div v-html="templateIjinLokasi('i. IPL tahap 3', 
                                                'ipl3_nomor', 
                                                'ipl3_tanggal', 
                                                'ipl3_luas')"/> 
                <div v-html="templateIjinLokasi('j. Izin Prinsip Pelepasan Hutan', 
                                                'izin_pelepasan_hutan_nomor', 
                                                'izin_pelepasan_hutan_tanggal')"/> 
                <div v-html="templateIjinLokasi('k. SK Pelepasan Hutan', 
                                                'sk_pelepasan_hutan_nomor', 
                                                'sk_pelepasan_hutan_tanggal')"/> 
                <div v-html="templateIjinLokasi('l. HGU', 
                                                'hgu_nomor', 
                                                'hgu_tanggal',
                                                'hgu_luas')"/> 
                <div v-html="templateIjinLokasi('m. HGB', 
                                                'hgb_nomor', 
                                                'hgb_tanggal',
                                                'hgb_luas')"/> 
                <div v-html="templateIjinLokasi('n. SK Amdal/UKL/UPL', 
                                                'sk_amdal_nomor', 
                                                'sk_amdal_tanggal')"/> 
                <div v-html="templateIjinLokasi('o. SK Ruang Plasma', 
                                                'sk_ruang_plasma_nomor', 
                                                'sk_ruang_plasma_tanggal')"/> 
                <div v-html="templateIjinLokasi('p. SK CPP', 
                                                'sk_cpp_nomor', 
                                                'sk_cpp_tanggal')"/> 
                <div class="html2pdf__page-break"/>
                <br/>
                <p>
                    <strong>1. Lahan Pembibitan</strong>
                </p>
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center">
                                No
                            </td>
                            <td width="186">
                                Kegiatan
                            </td>
                            <td width="83" align="center">
                                Luas ( HA )
                            </td>
                            <td width="96" align="center">
                                JumlahBibit (Btg)
                            </td>
                            <td width="115" align="center">
                                Umur ( Bln )
                            </td>
                            <td width="101">
                                Keterangan
                            </td>
                        </tr>
                        <tr 
                            v-for="(item, index) in pembibitan"
                            :key="index">
                            <td width="36" align="center">
                                {{ index+1 }}
                            </td>
                            <td width="186">
                                {{ item.tipe }} - {{ item.kegiatan }}
                            </td>
                            <td width="83" align="center">
                                {{ item.luas }}
                            </td>
                            <td width="96" align="center">
                                {{ item.jumlah_bibit }}
                            </td>
                            <td width="115" align="center">
                                {{ item.umur }}
                            </td>
                            <td width="115" align="center">
                                {{ item.keterangan || '-' }}
                            </td>
                        </tr>
                        <tr>
                            <td width="36" align="center">
                                
                            </td>
                            <td width="186" align="center">
                                Total
                            </td>
                            <td width="83" align="center">
                                {{ pembibitan.map((item)=>item.luas).reduce((a, b) => a + Number(b), 0)}}
                            </td>
                            <td width="96" align="center">
                                {{ pembibitan.map((item)=>item.jumlah_bibit).reduce((a, b) => a + Number(b), 0)}}
                            </td>
                            <td width="115" align="center">
                                {{ pembibitan.map((item)=>item.umur).reduce((a, b) => a + Number(b), 0)}}
                            </td>
                            <td width="115" align="center">
                                <p></p>
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                <p>
                    <strong>Perkembangan kegiatan</strong>
                </p>
                1. Penyelesaian Hak Atas Tanah
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center" rowspan="2">
                                No
                            </td>
                            <td width="186" rowspan="2">
                                Proses
                            </td>
                            <td width="83" align="center" colspan="3">
                                Perolehan
                            </td>
                            <td width="101" rowspan="2">
                                Keterangan
                            </td>
                        </tr>
                        <tr>
                            <td align="center">
                                Triwulan Lalu
                            </td>
                            <td align="center">
                                Triwulan Ini
                            </td>
                            <td align="center">
                                S/D Saat Ini
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in hat"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.proses }}
                            </td>
                            <td align="center">
                                {{ item.triwulan_lalu }}
                            </td>
                            <td align="center">
                                {{ item.triwulan_ini }}
                            </td>
                            <td align="center">
                                {{ item.sd_sekarang }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                2. Rencana Dan Realisasi Pembukaan Lahan
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center" rowspan="2">
                                No
                            </td>
                            <td width="186" rowspan="2" align="center">
                                Tahun LC
                            </td>
                            <td width="186" rowspan="2" align="center">
                                Rencana (HA)
                            </td>
                            <td width="83" align="center" colspan="2">
                                Realisasi (HA)
                            </td>
                            <td width="101" rowspan="2">
                                Keterangan
                            </td>
                        </tr>
                        <tr>
                            <td align="center">
                                Inti
                            </td>
                            <td align="center">
                                Plasma
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in pembukaan"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.tahun_lc }}
                            </td>
                            <td align="center">
                                {{ item.rencana }}
                            </td>
                            <td align="center">
                                {{ item.realisasi_inti }}
                            </td>
                            <td align="center">
                                {{ item.realisasi_plasma }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                3. Rencana Dan Realisasi Penanaman
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center" rowspan="2">
                                No
                            </td>
                            <td width="186" align="center">
                                Tahun Penanaman
                            </td>
                            <td width="186" rowspan="2" align="center">
                                Rencana (HA)
                            </td>
                            <td width="83" align="center" colspan="2">
                                Inti
                            </td>
                            <td width="101" align="center" colspan="2">
                                Plasma
                            </td>
                            <td width="101" rowspan="2">
                                Keterangan
                            </td>
                        </tr>
                        
                        <tr>
                            <td align="center">
                                Layak Tanam
                            </td>
                            <td align="center">
                                TBM
                            </td>
                            <td align="center">
                                TM
                            </td>
                            <td align="center">
                                TBM
                            </td>
                            <td align="center">
                                TM
                            </td>
                        </tr>
                        
                        <tr
                            v-for="(item, index) in penanaman"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.tahun_penanaman }}
                            </td>
                            <td align="center">
                                {{ item.rencana }}
                            </td>
                            <td align="center">
                                {{ item.inti_tbm }}
                            </td>
                            <td align="center">
                                {{ item.inti_tm }}
                            </td>
                            <td align="center">
                                {{ item.plasma_tbm }}
                            </td>
                            <td align="center">
                                {{ item.plasma_tm }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>

                <br/>
                4. ANKT
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center">
                                No
                            </td>
                            <td width="186" align="center">
                                ANKT
                            </td>
                            <td width="186" align="center">
                                Kondisi
                            </td>
                            <td width="83" align="center">
                                Luasan
                            </td>
                            <td width="101" align="center">
                                Koordinat
                            </td>
                            <td width="101">
                                Keterangan
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in ankt"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.ankt }}
                            </td>
                            <td align="center">
                                {{ item.kondisi }}
                            </td>
                            <td align="center">
                                {{ item.luasan }}
                            </td>
                            <td align="center">
                                {{ item.koordinat }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                5. Lahan Gambut
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center">
                                No
                            </td>
                            <td width="186" align="center">
                                Lahan Gambut
                            </td>
                            <td width="186" align="center">
                                Kondisi
                            </td>
                            <td width="83" align="center">
                                Luasan
                            </td>
                            <td width="101" align="center">
                                Koordinat
                            </td>
                            <td width="101">
                                Keterangan
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in lahangambut"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.lahan_gambut }}
                            </td>
                            <td align="center">
                                {{ item.kondisi }}
                            </td>
                            <td align="center">
                                {{ item.luasan }}
                            </td>
                            <td align="center">
                                {{ item.koordinat }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>

                <br/>
                6. Embung
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center">
                                No
                            </td>
                            <td width="186" align="center">
                                Embung
                            </td>
                            <td width="186" align="center">
                                Kondisi
                            </td>
                            <td width="83" align="center">
                                Luasan
                            </td>
                            <td width="101" align="center">
                                Koordinat
                            </td>
                            <td width="101">
                                Keterangan
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in embung"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.embung }}
                            </td>
                            <td align="center">
                                {{ item.kondisi }}
                            </td>
                            <td align="center">
                                {{ item.luasan }}
                            </td>
                            <td align="center">
                                {{ item.koordinat }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>

                <br/>
                7. Tenaga Kerja
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center" rowspan="3">
                                No
                            </td>
                            <td width="372" align="center" rowspan="3">
                                Uraian
                            </td>
                            <td width="186" align="center" colspan="2">
                                Kewarganegaraan (orang)
                            </td>
                            <td width="186" align="center" colspan="3">
                                Staff & Karyawan (orang)
                            </td>
                            <td align="center" colspan="2">
                                Jenis Kelamin
                            </td>
                        </tr>
                        <tr>
                            <td rowspan="2">
                                Asing
                            </td>
                            <td rowspan="2">
                                Indonesia
                            </td>
                            <td rowspan="2">
                                Bulanan
                            </td>
                            <td colspan="2" align="center">
                                Harian
                            </td>
                            <td rowspan="2" align="center">
                                L
                            </td>
                            <td rowspan="2" align="center">
                                P
                            </td>
                        </tr>
                        <tr>
                            <td>
                                Tetap
                            </td>
                            <td>
                                Lepas
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in tenagakerja"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.tipe }} - {{item.uraian}}
                            </td>
                            <td align="center">
                                {{ item.kewarganegaraan_asing }}
                            </td>
                            <td align="center">
                                {{ item.kewarganegaraan_indonesia }}
                            </td>
                            <td align="center">
                                {{ item.sk_bulanan }}
                            </td>
                            <td align="center">
                                {{ item.sk_harian_tetap }}
                            </td>
                            <td align="center">
                                {{ item.sk_harian_lepas }}
                            </td>
                            <td align="center">
                                {{ item.jenis_kelamin_p }}
                            </td>
                            <td align="center">
                                {{ item.jenis_kelamin_w }}
                            </td>
                            
                        </tr>
                    </tbody>
                </table>
                <br/>
                8. Rencana Dan Realisasi Pembangunan Pabrik
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center">
                                No
                            </td>
                            <td width="372" align="center">
                                Uraian
                            </td>
                            <td width="186" align="center">
                                Rencana
                            </td>
                            <td width="83" align="center">
                                Realisasi
                            </td>
                            <td width="101">
                                Keterangan
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in pembangunan"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.tipe }} - {{ item.uraian }}
                            </td>
                            <td align="center">
                                {{ item.rencana }}
                            </td>
                            <td align="center">
                                {{ item.realisasi }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                9. Kepemilikian Sarana Prasarana Sistem Cegah Dan Kendali Kebakaran
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center">
                                No
                            </td>
                            <td width="372" align="center">
                                Jenis Sarana Prasarana dan Sistem Yang dimiliki
                            </td>
                            <td width="83" align="center">
                                Jumlah
                            </td>
                            <td width="101">
                                Keterangan
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in kebakaran"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.tipe }} - {{ item.jenis_sarana }}
                            </td>
                            <td align="center">
                                {{ item.jumlah }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                10. Kepemilikan Sarana Prasarana Sistem Cegah dan Kendali OPT
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center">
                                No
                            </td>
                            <td width="372" align="center">
                                Jenis Sarana Prasarana dan Sistem Yang dimiliki
                            </td>
                            <td width="83" align="center">
                                Jumlah
                            </td>
                            <td width="101">
                                Keterangan
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in opt"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.tipe }} - {{ item.jenis_sarana }}
                            </td>
                            <td align="center">
                                {{ item.jumlah }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                11. Sarana Produksi
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center">
                                No
                            </td>
                            <td width="186" align="center">
                                Jenis
                            </td>
                            <td width="83" align="center">
                                Satuan
                            </td>
                            <td width="83" align="center">
                                Jumlah
                            </td>
                            <td width="101">
                                Ket.Perincian
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in saranaproduksi"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.jenis }}
                            </td>
                            <td align="center">
                                {{ item.satuan }}
                            </td>
                            <td align="center">
                                {{ item.jumlah }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                12. Jumlah & Jenis Alat Berat Yang Digunakan
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center">
                                No
                            </td>
                            <td width="186" align="center">
                                Jenis
                            </td>
                            <td width="83" align="center">
                                Jumlah (Unit)
                            </td>
                            <td width="101">
                                Keterangan
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in alatberat"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.jenis }}
                            </td>
                            <td align="center">
                                {{ item.jumlah }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                13. Sarana dan Prasarana Sosial Kemasyarakatan
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center">
                                No
                            </td>
                            <td width="186" align="center">
                                Sarana / Prasarana
                            </td>
                            <td width="83" align="center">
                                Jumlah (Unit)
                            </td>
                            <td width="101">
                                Keterangan
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in saranasosial"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.nama_sarana }}
                            </td>
                            <td align="center">
                                {{ item.jumlah }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                14. Produksi Dan Pemasaran<br/>
                a. Produksi
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center" rowspan="3">
                                No
                            </td>
                            <td width="186" align="center" rowspan="3">
                                Triwulan
                            </td>
                            <td width="558" align="center" colspan="10">
                                Produksi (Ton)
                            </td>
                        </tr>
                        <tr>
                            <td colspan="5" align="center">
                                Inti
                            </td>
                            <td colspan="5" align="center">
                                Plasma
                            </td>
                        </tr>
                        <tr>
                            <td>TBS</td>
                            <td>Kernel</td>
                            <td>CPO</td>
                            <td>PKO</td>
                            <td>PKE</td>
                            <td>TBS</td>
                            <td>Kernel</td>
                            <td>CPO</td>
                            <td>PKO</td>
                            <td>PKE</td>
                        </tr>
                        <tr
                            v-for="(item, index) in produksi"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td align="center">
                                {{ item.tahun }}
                            </td>
                            <td align="center">
                                {{ item.inti_tbs }}
                            </td>
                            <td align="center">
                                {{ item.inti_kernel }}
                            </td>
                            <td align="center">
                                {{ item.inti_cpo }}
                            </td>
                            <td align="center">
                                {{ item.inti_pko }}
                            </td>
                            <td align="center">
                                {{ item.inti_pke }}
                            </td>
                            
                            <td align="center">
                                {{ item.plasma_tbs }}
                            </td>
                            <td align="center">
                                {{ item.plasma_kernel }}
                            </td>
                            <td align="center">
                                {{ item.plasma_cpo }}
                            </td>
                            <td align="center">
                                {{ item.plasma_pko }}
                            </td>
                            <td align="center">
                                {{ item.plasma_pke }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                b. Pemasaran
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center" rowspan="2">
                                No
                            </td>
                            <td width="186" align="center" rowspan="2">
                                Jenis Produksi
                            </td>
                            <td width="100" align="center" rowspan="2">
                                Satuan
                            </td>
                            <td width="372" align="center" colspan="2">
                                Dalam Negeri
                            </td>
                            <td width="372" align="center" colspan="2">
                                Ekspor
                            </td>
                        </tr>
                        <tr>
                            <td align="center">
                                Volume
                            </td>
                            <td align="center">
                                Nilai (Rp)
                            </td>
                            <td align="center">
                                Volume
                            </td>
                            <td align="center">
                                Nilai (Rp)
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in pemasaran"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td align="center">
                                {{ item.jenis }}
                            </td>
                            <td align="center">
                                {{ item.satuan }}
                            </td>
                            <td align="center">
                                {{ item.dn_volume }}
                            </td>
                            <td align="center">
                                {{ item.dn_nilai }}
                            </td>
                            <td align="center">
                                {{ item.ekspor_volume }}
                            </td>
                            <td align="center">
                                {{ item.ekspor_nilai }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                c. Kerjasama Kemitraan
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center" rowspan="3">
                                No
                            </td>
                            <td width="186" align="center" rowspan="3">
                                Nama Koperasi
                            </td>
                            <td width="186" align="center" rowspan="3">
                                No dan tgl MOU
                            </td>
                            <td width="186" align="center" colspan="2">
                                Target
                            </td>
                            <td width="186" align="center" colspan="3">
                                Realisasi
                            </td>
                            <td width="100" align="center" rowspan="3">
                                Tahun Tanam
                            </td>
                        </tr>
                        <tr>
                            <td align="center" rowspan="2">
                                KK
                            </td>
                            <td align="center" rowspan="2">
                                Luas (Ha)
                            </td>
                            <td align="center" rowspan="2">
                                KK
                            </td>
                            <td align="center" colspan="2">
                                Luas (Ha)
                            </td>
                        </tr>
                        <tr>
                            <td align="center">TBM</td>
                            <td align="center">TM</td>
                        </tr>
                        <tr
                            v-for="(item, index) in mitra"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td align="center">
                                {{ item.nama_koperasi }}
                            </td>
                            <td align="center">
                                {{ item.no_mou }}/{{ item.tanggal_mou }}
                            </td>
                            <td align="center">
                                {{ item.target_kk }}
                            </td>
                            <td align="center">
                                {{ item.target_luas }}
                            </td>
                            <td align="center">
                                {{ item.realisasi_kk }}
                            </td>
                            <td align="center">
                                {{ item.realisasi_luas_tbm }}
                            </td>
                            <td align="center">
                                {{ item.realisasi_luas_tm }}
                            </td>
                            <td align="center">
                                {{ item.tahun_tanam }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                d. Kemitraan Lainnya
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="36" align="center">
                                No
                            </td>
                            <td width="186" align="center">
                                Jenis Koperasi
                            </td>
                            <td width="186" align="center">
                                Jenis Kegiatan
                            </td>
                            <td width="186" align="center">
                                Volume Kegiatan
                            </td>
                            <td>
                                Keterangan
                            </td>
                        </tr>
                        <tr
                            v-for="(item, index) in mitralainnya"
                            :key="index">
                            <td align="center">
                                {{ index+1 }}
                            </td>
                            <td>
                                {{ item.jenis_koperasi }}
                            </td>
                            <td>
                                {{ item.jenis_kegiatan }}
                            </td>
                            <td align="center">
                                {{ item.volume_kegiatan }}
                            </td>
                            <td>
                                {{ item.keterangan|| "-" }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="100%">
                                PROGRAM COMMUNITY DEVELOPMENT/CORPORATE SOCIAL RESPONSIBILITY (CSR):
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <ul style="list-style:auto">
                                    <li        
                                        v-for="(item, index) in csr"
                                        :key="index">{{ item.deskripsi }}</li>
                                </ul>
                            </td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                
                <table style="border-collapse: collapse; width: 100%;" class="tabel-border">
                    <tbody>
                        <tr>
                            <td width="100%">
                                PERMASALAHAN
                            </td>
                        </tr>
                        <tr>
                            <td>
                                <ul style="list-style:auto">
                                    <li        
                                        v-for="(item, index) in permasalahan"
                                        :key="index">{{ item.deskripsi }}</li>
                                </ul>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </section>
            
        </vue-html2pdf>
    </div>
</template>
<script>
import VueHtml2pdf from 'vue-html2pdf'
export default {
    props: ['id_perusahaan', 'triwulan'],
    mounted: function(){
        this.handleUpdateData()
    },
    watch:{
        triwulan: function(){
            this.handleUpdateData()
        }
    },
    components: {
        VueHtml2pdf
    },
    async asyncData({ params, $api }){
        const perusahaan    = (await $api.$get(`/v1/api/detil/perusahaan/${params.id}`)).data || {}
        
		return {
            perusahaan,
            legalitas       : {},
            pembibitan      : [],
            hat             : [],
            pembukaan       : [],
            penanaman       : [],
            ankt            : [],
            lahangambut     : [],
            embung          : [],
            tenagakerja     : [],
            pembangunan     : [],
            kebakaran       : [],
            opt             : [],
            saranaproduksi  : [],
            alatberat       : [],
            saranasosial    : [],
            produksi        : [],
            pemasaran       : [],
            mitra           : [],
            mitralainnya    : [],
            csr             : [],
            permasalahan    : [],
		}
	},
    data: () => ({
    }),
    methods:{
		handelCetak: function(){
			this.$refs.html2Pdf.generatePdf()
		},
        handleUpdateData: async function(){
            this.legalitas      = (await this.$api.$get(`/v1/api/detil/perusahaan_legalitas/${this.id_perusahaan}/id_perusahaan?field1=triwulan&value1=${this.triwulan}`)).data || {}
            this.pembibitan     = (await this.$api.$get(`/v1/api/data/perusahaan_lahan_pembibitan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.hat            = (await this.$api.$get(`/v1/api/data/perusahaan_penyelesaian_hat/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.pembukaan      = (await this.$api.$get(`/v1/api/data/perusahaan_pembukaan_lahan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.penanaman      = (await this.$api.$get(`/v1/api/data/perusahaan_penanaman_lahan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.ankt           = (await this.$api.$get(`/v1/api/data/perusahaan_ankt/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.lahangambut    = (await this.$api.$get(`/v1/api/data/perusahaan_lahan_gambut/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.embung         = (await this.$api.$get(`/v1/api/data/perusahaan_embung/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.tenagakerja    = (await this.$api.$get(`/v1/api/data/perusahaan_tenaga_kerja/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.pembangunan    = (await this.$api.$get(`/v1/api/data/perusahaan_pembangunan_pabrik/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.kebakaran      = (await this.$api.$get(`/v1/api/data/perusahaan_kendali_kebakaran/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.opt            = (await this.$api.$get(`/v1/api/data/perusahaan_kendali_opt/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.saranaproduksi = (await this.$api.$get(`/v1/api/data/perusahaan_sarana_produksi/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.alatberat      = (await this.$api.$get(`/v1/api/data/perusahaan_alat_berat/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.saranasosial   = (await this.$api.$get(`/v1/api/data/perusahaan_prasarana_sosial/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.produksi       = (await this.$api.$get(`/v1/api/data/perusahaan_produksi/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.pemasaran      = (await this.$api.$get(`/v1/api/data/perusahaan_pemasaran/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.mitra          = (await this.$api.$get(`/v1/api/data/perusahaan_kerjasama_kemitraan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.mitralainnya   = (await this.$api.$get(`/v1/api/data/perusahaan_kemitraan_lainnya/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.csr            = (await this.$api.$get(`/v1/api/data/perusahaan_csr/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
            this.permasalahan   = (await this.$api.$get(`/v1/api/data/perusahaan_permasalahan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`)).data || []
        },
        templatePerusahaan: function(no, field, value){
            let templateValue   = `<td></td>`
            if(value){
                templateValue   = `<td>: ${this.perusahaan[value]}</td>`
            }
            return `<tr>
                        <td>${no} </td>
                        <td>${field}</td>
                        ${templateValue}
                    </tr>`
        },
        templateIjinLokasi: function(item, nomor, tanggal, luas){
            let templateLuas    = ''
            if(luas){
                templateLuas    = `<tr>
                        <td>Luas </td>
                        <td>: ${this.legalitas[luas]} ha</td>
                    </tr>`
            }
            return `
            <p>${item}</p>
            <table style="border-collapse: collapse; margin-left:32px">
                <tbody>
                    <tr>
                        <td width="147">Nomor </td>
                        <td>: ${this.legalitas[nomor]} </td>
                    </tr>
                    <tr>
                        <td>Tanggal </td>
                        <td>: ${this.legalitas[tanggal]} </td>
                    </tr>
                    ${templateLuas}
                </tbody>
            </table>
            <br/>
            `
        }
    }
}
</script>
<style scoped>
.text-center{
    text-align:center
}
p{
    margin-bottom:8px;
}
.tabel-border tr td{
    border:1px solid black;
    padding-left:4px;
    padding-right:4px;
}
</style>