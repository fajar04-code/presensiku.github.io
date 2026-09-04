<!DOCTYPE html>
<html lang="id" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Presensi Kehadiran SMAN 2 Nusa - Kelola Data & Tautan</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: { 50: '#eef2ff', 500: '#6366f1', 600: '#4f46e5', 700: '#4338ca' }
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body class="bg-gray-50 dark:bg-gray-900 text-gray-800 dark:text-gray-100 h-full flex flex-col transition-colors duration-200">

    <!-- Header -->
    <header class="bg-white dark:bg-gray-800 border-b border-gray-200 dark:border-gray-700 shadow-sm py-4 px-4 sm:px-6 flex flex-wrap justify-between items-center gap-4">
        <div class="flex items-center space-x-3">
            <div class="bg-indigo-600 text-white p-2.5 rounded-xl shadow-md">
                <i class="fa-solid fa-school text-xl"></i>
            </div>
            <div>
                <h1 class="text-xl font-bold tracking-tight text-gray-900 dark:text-white">Presensi Kehadiran SMAN 2 Nusa</h1>
                <p class="text-xs text-gray-500 dark:text-gray-400">Pilih siswa per kelas, tambah/edit data, dan kelola tautan otomatis</p>
            </div>
        </div>
        
        <div class="flex items-center flex-wrap gap-2">
            <button onclick="openAddStudentModal()" class="px-3 py-2 text-xs font-semibold rounded-xl bg-indigo-600 text-white hover:bg-indigo-700 shadow-sm transition flex items-center gap-1.5">
                <i class="fa-solid fa-user-plus"></i>
                <span>+ Siswa</span>
            </button>
            <button onclick="openAddClassModal()" class="px-3 py-2 text-xs font-semibold rounded-xl bg-emerald-600 text-white hover:bg-emerald-700 shadow-sm transition flex items-center gap-1.5">
                <i class="fa-solid fa-folder-plus"></i>
                <span>+ Kelas</span>
            </button>
            <button onclick="exportDataJSON()" class="p-2.5 text-xs font-medium rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition" title="Ekspor Data (Backup JSON)">
                <i class="fa-solid fa-download"></i>
            </button>
            <label class="p-2.5 text-xs font-medium rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 cursor-pointer transition" title="Impor Data (Upload JSON)">
                <i class="fa-solid fa-upload"></i>
                <input type="file" id="importJsonInput" accept=".json" onchange="importDataJSON(event)" class="hidden">
            </label>
            <button onclick="toggleDarkMode()" class="p-2.5 rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition" title="Ganti Tema">
                <i class="fa-solid fa-moon dark:hidden"></i>
                <i class="fa-solid fa-sun hidden dark:block text-yellow-400"></i>
            </button>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-1 max-w-7xl w-full mx-auto p-4 md:p-6 grid grid-cols-1 lg:grid-cols-12 gap-6 overflow-y-auto">

        <!-- Notification Banner -->
        <div id="alertBox" class="col-span-12 hidden bg-indigo-50 dark:bg-indigo-950/60 border border-indigo-200 dark:border-indigo-800 text-indigo-800 dark:text-indigo-200 px-4 py-3 rounded-xl flex items-center justify-between text-sm shadow-sm transition-all">
            <div class="flex items-center space-x-2">
                <i class="fa-solid fa-circle-info text-indigo-500"></i>
                <span id="alertText">Pesan peringatan.</span>
            </div>
            <button onclick="hideAlert()" class="text-indigo-600 hover:text-indigo-800 dark:text-indigo-400 font-bold">&times;</button>
        </div>

        <!-- Kolom Kiri: Daftar Siswa Berdasarkan Kelas & Pengaturan Tautan -->
        <div class="lg:col-span-7 flex flex-col gap-6">
            
            <!-- Konfigurasi Tautan / Format Link per Kelas -->
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl shadow-sm border border-gray-200 dark:border-gray-700 flex flex-col gap-3">
                <div class="flex justify-between items-center">
                    <h2 class="font-semibold text-sm flex items-center gap-2 text-gray-800 dark:text-gray-200">
                        <i class="fa-solid fa-link text-indigo-500"></i> Pola Tautan Presensi / Kelas
                    </h2>
                    <button onclick="resetToDefaultData()" class="text-[11px] text-red-500 hover:underline flex items-center gap-1">
                        <i class="fa-solid fa-rotate-left"></i> Reset Data Awal
                    </button>
                </div>
                <p class="text-xs text-gray-400">Masukkan tautan Google Forms/format umum. Gunakan placeholder <code class="bg-gray-100 dark:bg-gray-700 px-1 py-0.5 rounded text-indigo-500">{nama}</code> atau <code class="bg-gray-100 dark:bg-gray-700 px-1 py-0.5 rounded text-indigo-500">{nis}</code> untuk kustomisasi dinamis.</p>
                
                <div class="flex flex-col sm:flex-row gap-2">
                    <input type="text" id="globalLinkInput" placeholder="Contoh: https://docs.google.com/forms/.../entry.123={nama}&entry.456={nis}" class="flex-1 p-2.5 text-xs rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 focus:ring-2 focus:ring-indigo-500 focus:outline-none transition">
                    <button onclick="applyGlobalLink()" class="px-4 py-2 text-xs font-semibold rounded-xl bg-indigo-600 text-white hover:bg-indigo-700 transition whitespace-nowrap">Terapkan Kelas Ini</button>
                </div>
            </div>

            <!-- Bagian Pemilihan Siswa Per Kelas -->
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl shadow-sm border border-gray-200 dark:border-gray-700 flex flex-col gap-4 flex-1">
                
                <div class="flex flex-wrap justify-between items-center gap-2 border-b border-gray-100 dark:border-gray-700 pb-3">
                    <h2 class="font-semibold text-sm flex items-center gap-2">
                        <i class="fa-solid fa-users text-indigo-500"></i> Direktori Siswa & Klasifikasi Kelas
                    </h2>
                    <div class="flex items-center gap-2">
                        <button onclick="selectAll(true)" class="px-3 py-1.5 text-xs font-medium rounded-lg bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition">Pilih Semua</button>
                        <button onclick="selectAll(false)" class="px-3 py-1.5 text-xs font-medium rounded-lg bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition">Batalkan</button>
                    </div>
                </div>

                <!-- Tab Kelas Selector -->
                <div id="classTabs" class="flex flex-wrap gap-2 items-center">
                    <!-- Dinamis via JS -->
                </div>

                <!-- Filter & Search Bar -->
                <div class="relative">
                    <i class="fa-solid fa-magnifying-glass absolute left-3 top-3 text-xs text-gray-400"></i>
                    <input type="text" id="searchInput" oninput="renderStudentList()" placeholder="Cari nama, NIS, atau NISN siswa..." class="w-full pl-8 pr-3 py-2 text-xs rounded-xl border border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-900 focus:ring-2 focus:ring-indigo-500 focus:outline-none transition">
                </div>

                <!-- Kontainer Info Daftar Siswa -->
                <div class="flex justify-between items-center text-xs text-gray-500 px-1">
                    <span id="activeClassTitle" class="font-bold text-gray-700 dark:text-gray-300">Kelas XA</span>
                    <span id="classSelectedCount">0 terpilih di kelas ini</span>
                </div>

                <!-- Scrollable Student List -->
                <div id="studentListContainer" class="min-h-[260px] max-h-[380px] overflow-y-auto border border-gray-100 dark:border-gray-700 rounded-xl p-3 bg-gray-50/50 dark:bg-gray-900/50 flex flex-col gap-2">
                    <!-- Dinamis via JS -->
                </div>
            </div>

        </div>

        <!-- Kolom Kanan: Hasil Kumpulan Tautan & Aksi Massal -->
        <div class="lg:col-span-5 flex flex-col gap-6">
            
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl shadow-sm border border-gray-200 dark:border-gray-700 flex flex-col gap-4 flex-1 justify-between">
                <div>
                    <div class="flex justify-between items-center border-b border-gray-100 dark:border-gray-700 pb-3">
                        <h2 class="font-semibold text-sm flex items-center gap-2">
                            <i class="fa-solid fa-clipboard-list text-indigo-500"></i> Hasil Kumpulan Tautan
                        </h2>
                        <span id="totalSelectedBadge" class="bg-indigo-100 dark:bg-indigo-900/50 text-indigo-700 dark:text-indigo-300 px-2.5 py-1 rounded-full text-xs font-bold">0 Tautan</span>
                    </div>

                    <p class="text-xs text-gray-400 my-3">Tautan presensi dari siswa yang dicentang akan terkumpul secara otomatis di bawah ini:</p>

                    <!-- Output Textarea / List Preview -->
                    <textarea id="outputLinkArea" readonly rows="10" placeholder="Daftar tautan terkumpul akan muncul di sini..." class="w-full p-3.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:outline-none font-mono transition resize-none"></textarea>
                </div>

                <!-- Statistik Ringkas -->
                <div class="grid grid-cols-2 gap-3 p-3 bg-gray-50 dark:bg-gray-900/60 rounded-xl border border-gray-100 dark:border-gray-800 text-xs">
                    <div>
                        <span class="text-gray-400 block text-[10px]">Total Siswa Terdaftar:</span>
                        <span id="statTotalStudents" class="font-bold text-gray-700 dark:text-gray-200">0</span>
                    </div>
                    <div>
                        <span class="text-gray-400 block text-[10px]">Total Kelas:</span>
                        <span id="statTotalClasses" class="font-bold text-gray-700 dark:text-gray-200">0</span>
                    </div>
                </div>

                <div class="flex flex-col gap-2 pt-2">
                    <button onclick="processAndOpen()" class="w-full py-3 text-sm font-semibold rounded-xl bg-indigo-600 text-white hover:bg-indigo-700 shadow-md shadow-indigo-500/20 transition flex items-center justify-center gap-2">
                        <i class="fa-solid fa-rocket"></i> Buka Semua Tautan Terpilih
                    </button>
                    <button onclick="copyAllOutputLinks()" class="w-full py-2.5 text-sm font-medium rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition flex items-center justify-center gap-2">
                        <i class="fa-regular fa-copy"></i> Salin Semua Tautan
                    </button>
                </div>
            </div>

        </div>

    </main>

    <!-- Modal Tambah / Edit Siswa -->
    <div id="studentModal" class="fixed inset-0 bg-black/50 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white dark:bg-gray-800 rounded-2xl max-w-md w-full p-6 shadow-2xl border border-gray-100 dark:border-gray-700 flex flex-col gap-4">
            <div class="flex justify-between items-center border-b border-gray-100 dark:border-gray-700 pb-3">
                <h3 id="studentModalTitle" class="font-bold text-base text-gray-800 dark:text-gray-100">Tambah Siswa Baru</h3>
                <button onclick="closeStudentModal()" class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-200 text-lg">&times;</button>
            </div>

            <form id="studentForm" onsubmit="handleSaveStudent(event)" class="flex flex-col gap-3 text-xs">
                <input type="hidden" id="editOriginalClass">
                <input type="hidden" id="editOriginalId">

                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Kelas Target</label>
                    <select id="modalStudentClass" required class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                        <!-- Populated dynamically -->
                    </select>
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">NIS (ID Unik)</label>
                        <input type="text" id="modalStudentId" required placeholder="Contoh: 260120" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                    </div>
                    <div>
                        <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">NISN</label>
                        <input type="text" id="modalStudentNisn" required placeholder="Contoh: 0105432109" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                    </div>
                </div>

                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Nama Lengkap Siswa</label>
                    <input type="text" id="modalStudentName" required placeholder="Contoh: AHMAD FAUZI" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                </div>

                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Jenis Kelamin</label>
                    <select id="modalStudentGender" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                        <option value="LAKI-LAKI">LAKI-LAKI</option>
                        <option value="PEREMPUAN">PEREMPUAN</option>
                    </select>
                </div>

                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Tautan Presensi (Opsional)</label>
                    <input type="url" id="modalStudentLink" placeholder="Biarkan kosong untuk menggunakan tautan default kelas" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                </div>

                <div class="flex justify-end gap-2 pt-3 border-t border-gray-100 dark:border-gray-700">
                    <button type="button" onclick="closeStudentModal()" class="px-4 py-2 rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition">Batal</button>
                    <button type="submit" class="px-4 py-2 rounded-xl bg-indigo-600 text-white hover:bg-indigo-700 font-semibold transition">Simpan Data</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Tambah Kelas -->
    <div id="classModal" class="fixed inset-0 bg-black/50 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white dark:bg-gray-800 rounded-2xl max-w-sm w-full p-6 shadow-2xl border border-gray-100 dark:border-gray-700 flex flex-col gap-4">
            <div class="flex justify-between items-center border-b border-gray-100 dark:border-gray-700 pb-3">
                <h3 class="font-bold text-base text-gray-800 dark:text-gray-100">Tambah Kelas Baru</h3>
                <button onclick="closeClassModal()" class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-200 text-lg">&times;</button>
            </div>

            <form onsubmit="handleSaveClass(event)" class="flex flex-col gap-3 text-xs">
                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Nama Kelas Baru</label>
                    <input type="text" id="newClassNameInput" required placeholder="Contoh: Kelas XE atau Kelas XI-IPA 1" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none">
                </div>

                <div class="flex justify-end gap-2 pt-3 border-t border-gray-100 dark:border-gray-700">
                    <button type="button" onclick="closeClassModal()" class="px-4 py-2 rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition">Batal</button>
                    <button type="submit" class="px-4 py-2 rounded-xl bg-emerald-600 text-white hover:bg-emerald-700 font-semibold transition">Tambah Kelas</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Konfirmasi Hapus -->
    <div id="confirmModal" class="fixed inset-0 bg-black/50 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white dark:bg-gray-800 rounded-2xl max-w-sm w-full p-6 shadow-2xl border border-gray-100 dark:border-gray-700 flex flex-col gap-4 text-center">
            <div class="w-12 h-12 bg-red-100 dark:bg-red-900/30 text-red-600 dark:text-red-400 rounded-full flex items-center justify-center mx-auto text-xl">
                <i class="fa-solid fa-triangle-exclamation"></i>
            </div>
            <h3 id="confirmTitle" class="font-bold text-base text-gray-800 dark:text-gray-100">Konfirmasi Hapus</h3>
            <p id="confirmMessage" class="text-xs text-gray-500 dark:text-gray-400">Apakah Anda yakin ingin menghapus data ini?</p>

            <div class="flex justify-center gap-3 pt-2">
                <button onclick="closeConfirmModal()" class="px-4 py-2 text-xs rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition">Batal</button>
                <button id="confirmExecuteBtn" class="px-4 py-2 text-xs rounded-xl bg-red-600 text-white hover:bg-red-700 font-semibold transition">Ya, Hapus</button>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="text-center py-4 text-xs text-gray-400 dark:text-gray-500 border-t border-gray-200 dark:border-gray-700">
        Presensi Kehadiran SMAN 2 Nusa &bull; Sistem Pengelola Data & Tautan Siswa
    </footer>

    <!-- Script Logika Aplikasi -->
    <script>
        const initialSchoolData = {
            "Kelas XA": [
                { id: "260004", nisn: "0106148762", name: "ABDUL WAHIP", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ABDUL+WAHIP&entry.201529640=HS", selected: true },
                { id: "260010", nisn: "0107923109", name: "ALFON AQUINO SAKA", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ALFON+AQUINO+SAKA&entry.201529640=HS", selected: false },
                { id: "260012", nisn: "0105052057", name: "AMANDA PUTRI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AMANDA+PUTRI&entry.201529640=HS", selected: false },
                { id: "260017", nisn: "0118971241", name: "ARAYYA NUR ZAHIRA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ARAYYA+NUR+ZAHIRA&entry.201529640=HS", selected: true },
                { id: "260019", nisn: "0105469341", name: "ARIL SAHRUL RAMADANI", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ARIL+SAHRUL+RAMADANI&entry.201529640=HS", selected: false },
                { id: "260024", nisn: "097712728", name: "ELSYA APRILIA ANTHONY", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ELSYA+APRILIA+ANTHONY&entry.201529640=HS", selected: false },
                { id: "260030", nisn: "0111628831", name: "FITRIANI XA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FITRIANI+XA&entry.201529640=HS", selected: false },
                { id: "260031", nisn: "0112035176", name: "HADIR JUMANSA PUTRA", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HADIR+JUMANSA+PUTRA&entry.201529640=HS", selected: false },
                { id: "260037", nisn: "0101869333", name: "IMAM AMROSI", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=IMAM+AMROSI&entry.201529640=HS", selected: false },
                { id: "260039", nisn: "0115027428", name: "INDIAN ILYANDA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=INDIAN+ILYANDA&entry.201529640=HS", selected: false },
                { id: "260046", nisn: "0117832504", name: "KIRANA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=KIRANA&entry.201529640=HS", selected: false },
                { id: "260049", nisn: "0101496080", name: "MHD. ISWANDI", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MHD.+ISWANDI&entry.201529640=HS", selected: false },
                { id: "260053", nisn: "0103877484", name: "MUH. ALBAR", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH.+ALBAR&entry.201529640=HS", selected: true },
                { id: "260057", nisn: "0102802885", name: "MUHAMMAD FADLI ADRIANO", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+FADLI+ADRIANO&entry.201529640=HS", selected: false },
                { id: "260061", nisn: "0118519658", name: "MUHAMMAD ISRA SYAHPUTRA", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ISRA+SYAHPUTRA&entry.201529640=HS", selected: false },
                { id: "260065", nisn: "0101834198", name: "MUHAMMAD RESA SAPUTRA", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+RESA+SAPUTRA&entry.201529640=HS", selected: false },
                { id: "260069", nisn: "0105715277", name: "MUHAMMAD WILDAN", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+WILDAN&entry.201529640=HS", selected: false },
                { id: "260072", nisn: "0098401328", name: "NADA KAMELIA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NADA+KAMELIA&entry.201529640=HS", selected: true },
                { id: "260076", nisn: "0108527238", name: "NOVIANA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NOVIANA&entry.201529640=HS", selected: true },
                { id: "260080", nisn: "0111176983", name: "NUR VEBRIANI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+VEBRIANI&entry.201529640=HS", selected: false },
                { id: "260084", nisn: "0107839346", name: "NURHIKMAH ABDI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURHIKMAH+ABDI&entry.201529640=HS", selected: true },
                { id: "260090", nisn: "0104278399", name: "RASTI PRITA ANDINI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RASTI+PRITA+ANDINI&entry.201529640=HS", selected: true },
                { id: "260092", nisn: "0107010100", name: "REFAN", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REFAN&entry.201529640=HS", selected: true },
                { id: "260098", nisn: "0111191658", name: "REZKY AFANDY", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REZKY+AFANDY&entry.201529640=HS", selected: false },
                { id: "260101", nisn: "0109392495", name: "SAMSINAR", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SAMSINAR&entry.201529640=HS", selected: true },
                { id: "260105", nisn: "0123968886", name: "SITI SAILAH SAPUTRI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SITI+SAILAH+SAPUTRI&entry.201529640=HS", selected: true },
                { id: "260109", nisn: "0104154107", name: "SYAHRUL RAMADHANI", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SYAHRUL+RAMADHANI&entry.201529640=HS", selected: false },
                { id: "260110", nisn: "0116564777", name: "WA ODE NURTADALIA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=WA+ODE+NURTADAHLIA&entry.201529640=HS", selected: false },
                { id: "260114", nisn: "0101000649", name: "YAFFA ALENA FAAIZA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=YAFFA+ALENA+FAAIZA&entry.201529640=HS", selected: false },
                { id: "260116", nisn: "0104888082", name: "YUNITA HALIMATUN SYA'DIAH", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=YUNITA+HALIMATUN+SYA'DIAH&entry.201529640=HS", selected: false }
            ],
            "Kelas XB": [
                { id: "260005", nisn: "0102094669", name: "ADAM ALIF RAHMAN", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ADAM+ALIF+RAHMAN&entry.201529640=HS", selected: true },
                { id: "260011", nisn: "0116883035", name: "ALI IRSAN", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ALI+IRSAN&entry.201529640=HS", selected: true },
                { id: "260014", nisn: "0109930277", name: "ANDI NURHALIZAH", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDI+NURHALIZAH&entry.201529640=HS", selected: true },
                { id: "260020", nisn: "0119525847", name: "BADAR IBADIN", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=BADAR+IBADIN&entry.201529640=HS", selected: true },
                { id: "260021", nisn: "0117889037", name: "DINDA KIRANA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=DINDA+KIRANA&entry.201529640=HS", selected: true },
                { id: "260025", nisn: "0109248575", name: "ERNI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ERNI&entry.201529640=HS", selected: true },
                { id: "260032", nisn: "0116390313", name: "HAJRIYANA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HAJRIYANA&entry.201529640=HS", selected: false },
                { id: "260033", nisn: "0103097316", name: "HERUL AGUSTIAN", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HERUL+AGUSTIAN&entry.201529640=HS", selected: false },
                { id: "260040", nisn: "0112728658", name: "INTAN BATRISYIA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=INTAN+BATRISYIA&entry.201529640=HS", selected: true },
                { id: "260041", nisn: "0107422875", name: "IQBAL IRFANSA", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=IQBAL+IRFANSA&entry.201529640=HS", selected: true },
                { id: "260047", nisn: "0106837618", name: "MARWAH SYAFITRI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MARWAH+SYAFITRI&entry.201529640=HS", selected: true },
                { id: "260054", nisn: "0101515411", name: "MUH. UMARSYAM", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH.+UMARSYAM&entry.201529640=HS", selected: false },
                { id: "2600503", nisn: "100506286", name: "MOHAMMAD IRWAN", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MOHAMMAD+IRWAN&entry.201529640=HS", selected: false },
                { id: "260058", nisn: "0111136908", name: "MUHAMMAD FHAYSAL SYUKUR AHMAD", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+FHAYSAL+SYUKUR+AHMAD&entry.201529640=HS", selected: false },
                { id: "260062", nisn: "0106705459", name: "MUHAMMAD KARIM", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+KARIM&entry.201529640=HS", selected: true },
                { id: "260066", nisn: "0104922371", name: "MUHAMMAD RIFQI", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+RIFQI&entry.201529640=HS", selected: true },
                { id: "260073", nisn: "0106033650", name: "NANDA ERISKA LIHU", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NANDA+ERISKA+LIHU&entry.201529640=HS", selected: true },
                { id: "260070", nisn: "0104388826", name: "MULTAZAM NISYAM", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MULTAZAM+NISYAM&entry.201529640=HS", selected: true },
                { id: "260077", nisn: "0109625541", name: "NUR ANISA RAMADAN", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+ANISA+RAMADAN&entry.201529640=HS", selected: false },
                { id: "260081", nisn: "0116968436", name: "NURAIRAH", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURAIRAH&entry.201529640=HS", selected: true },
                { id: "260085", nisn: "0113740296", name: "NURUL SAFIKAH", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURUL+SAFIKAH&entry.201529640=HS", selected: true },
                { id: "260091", nisn: "0117058653", name: "RATU RAMAYANA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RATU+RAMAYANA&entry.201529640=HS", selected: true },
                { id: "260093", nisn: "0104116976", name: "REIVAN ARADILA", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REIVAN+ARADILA&entry.201529640=HS", selected: true },
                { id: "260099", nisn: "0104428616", name: "RIFALDI", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RIFALDI&entry.201529640=HS", selected: false },
                { id: "2601023", nisn: "114740852", name: "SASKIA AMANDA WULANDARI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SASKIA+AMANDA+WULANDARI&entry.201529640=HS", selected: true },
                { id: "260106", nisn: "0119225802", name: "SITY NUR CAHYA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SITY+NUR+CAHYA&entry.201529640=HS", selected: true },
                { id: "2601113", nisn: "112662330", name: "WAFRI THALITA ZAINUN", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=WAFRI+THALITA+ZAINUN&entry.201529640=HS", selected: false },
                { id: "260115", nisn: "0103410698", name: "YOFARNO YOSAFAI RATU LUBUR", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=YOFARNO+YOSAFAI+RATU+LUBUR&entry.201529640=HS", selected: false }
            ],
            "Kelas XC": [
                { id: "260003", nisn: "0116790414", name: "A. NURFARIDAH", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=A.+NURFARIDAH&entry.201529640=HS", selected: true },
                { id: "260006", nisn: "3111658883", name: "AFIKA ADELIA SIREGAR", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AFIKA+ADELIA+SIREGAR&entry.201529640=HS", selected: true },
                { id: "260008", nisn: "0115123543", name: "AHMAD ANGGA", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AHMAD+ANGGA&entry.201529640=HS", selected: true },
                { id: "260013", nisn: "0119993291", name: "AMMAR FAIQ HAWRIEL ADNAN", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AMMAR+FAIQ+HAWRIEL+ADNAN&entry.201529640=HS", selected: true },
                { id: "260015", nisn: "0113593653", name: "ANDI NURUL SHAZIRAWATI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANDI+NURUL+SHAZIRAWATI&entry.201529640=HS", selected: true },
                { id: "260022", nisn: "0115190109", name: "EGY DESTRI AMALIA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=EGY+DESTRI+AMALIA&entry.201529640=HS", selected: true },
                { id: "260026", nisn: "0107565355", name: "FALDIANZAH TAUFIK NUR HIDAYAH", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FALDIANZAH+TAUFIK+NUR+HIDAYAH&entry.201529640=HS", selected: true },
                { id: "260027", nisn: "0107224310", name: "FAUZIAH", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FAUZIAH&entry.201529640=HS", selected: true },
                { id: "260034", nisn: "0115714284", name: "HIJRIYANI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HIJRIYANI&entry.201529640=HS", selected: true },
                { id: "260035", nisn: "0118616933", name: "HIKMAL MARUDDANI", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=HIKMAL+MARUDDANI&entry.201529640=HS", selected: true },
                { id: "260042", nisn: "0111180220", name: "IZMI AULIA ARHAM", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=IZMI+AULIA+ARHAM&entry.201529640=HS", selected: true },
                { id: "260043", nisn: "0102119722", name: "KAKA ARBI GILARDI", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=KAKA+ARBI+GILARDI&entry.201529640=HS", selected: true },
                { id: "260048", nisn: "0105220301", name: "MARWANI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MARWANI&entry.201529640=HS", selected: true },
                { id: "260051", nisn: "0101797683", name: "MOHAMMAD REZA R. LIHU", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MOHAMMAD+REZA+R.+LIHU&entry.201529640=HS", selected: true },
                { id: "260055", nisn: "0105499299", name: "MUHAMMAD AIDIL", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+AIDIL&entry.201529640=HS", selected: true },
                { id: "260059", nisn: "0107742019", name: "MUHAMMAD FIKRAM", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+FIKRAM&entry.201529640=HS", selected: true },
                { id: "260063", nisn: "0107664477", name: "MUHAMMAD RAMADHAN", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+RAMADHAN&entry.201529640=HS", selected: true },
                { id: "260067", nisn: "0109751609", name: "MUHAMMAD SYAFIAN MONE", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+SYAFIAN+MONE&entry.201529640=HS", selected: true },
                { id: "260074", nisn: "0111950492", name: "NIDHIFAH NAYLAH SAPUTRY", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NIDHIFAH+NAYLAH+SAPUTRY&entry.201529640=HS", selected: true },
                { id: "260078", nisn: "0111695633", name: "NUR HAFIZA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+HAFIZA&entry.201529640=HS", selected: true },
                { id: "260082", nisn: "0103516333", name: "NURFADILA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURFADILA&entry.201529640=HS", selected: true },
                { id: "260086", nisn: "095554229", name: "PUTRI ANGRENI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PUTRI+ANGRENI&entry.201529640=HS", selected: true },
                { id: "260088", nisn: "0105946200", name: "RAHMAT REZKY HIDAYAT", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RAHMAT+REZKY+HIDAYAT&entry.201529640=HS", selected: true },
                { id: "2600943", nisn: "112122465", name: "REIZA HAMZAH", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REIZA+HAMZAH&entry.201529640=HS", selected: true },
                { id: "260095", nisn: "0102337788", name: "RENITA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RENITA&entry.201529640=HS", selected: true },
                { id: "260107", nisn: "0119619702", name: "ST.RAHMAH", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ST.RAHMAH&entry.201529640=HS", selected: true },
                { id: "260103", nisn: "0104451032", name: "SEKAR WANGI RAHMADINI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SEKAR+WANGI+RAHMADINI&entry.201529640=HS", selected: true },
                { id: "260112", nisn: "0107736381", name: "WANDA NOVI AULIA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=WANDA+NOVI+AULIA&entry.201529640=HS", selected: true }
            ],
            "Kelas XD": [
                { id: "260007", nisn: "0108884814", name: "AFRAH FATHANIA PRABA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AFRAH+FATHANIA+PRABA&entry.201529640=HS", selected: true },
                { id: "260009", nisn: "0109166563", name: "AKBAR MAULANA", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=AKBAR+MAULANA&entry.201529640=HS", selected: true },
                { id: "260016", nisn: "0111791555", name: "ANISA PUTRI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ANISA+PUTRI&entry.201529640=HS", selected: true },
                { id: "260018", nisn: "0108722663", name: "ARHAM NURWAHID", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ARHAM+NURWAHID&entry.201529640=HS", selected: true },
                { id: "260023", nisn: "0106033839", name: "ELSA HANDAYANI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ELSA+HANDAYANI&entry.201529640=HS", selected: true },
                { id: "260028", nisn: "0116745293", name: "FEBRIANSYAH", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FEBRIANSYAH&entry.201529640=HS", selected: true },
                { id: "260029", nisn: "0108662406", name: "FITRIANI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=FITRIANI+X-D&entry.201529640=HS", selected: true },
                { id: "260036", nisn: "0112586711", name: "ILMANSYAH", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ILMANSYAH&entry.201529640=HS", selected: true },
                { id: "260038", nisn: "0107462839", name: "INDAYANI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=INDAYANI&entry.201529640=HS", selected: true },
                { id: "260044", nisn: "0106940038", name: "KAKA IBRA GILARDI", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=KAKA+IBRA+GILARDI&entry.201529640=HS", selected: true },
                { id: "2600453", nisn: "101143313", name: "KARMILA SYAHRINA SAPUTRI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=KARMILA+SYAHRINA+SAPUTRI&entry.201529640=HS", selected: false },
                { id: "260052", nisn: "0105410277", name: "MUH AIDIN ROIHAN AL FURQAN", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUH+AIDIN+ROIHAN+AL+FURQAN&entry.201529640=HS", selected: true },
                { id: "260056", nisn: "0111414121", name: "MUHAMMAD ARDIANSYAH", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+ARDIANSYAH&entry.201529640=HS", selected: true },
                { id: "260060", nisn: "0118399845", name: "MUHAMMAD IQBAL MULIYADI", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+IQBAL+MULIYADI&entry.201529640=HS", selected: false },
                { id: "260064", nisn: "0119799802", name: "MUHAMMAD REEFAN BASTIAN", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+REEFAN+BASTIAN&entry.201529640=HS", selected: true },
                { id: "260068", nisn: "0108012631", name: "MUHAMMAD SYAFIQ", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUHAMMAD+SYAFIQ&entry.201529640=HS", selected: true },
                { id: "260071", nisn: "0107544031", name: "MUSFIRA RAMADANI MARMAN", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=MUSFIRA+RAMADANI+MARMAN&entry.201529640=HS", selected: true },
                { id: "260075", nisn: "0108546784", name: "NOVI AMELIA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NOVI+AMELIA&entry.201529640=HS", selected: true },
                { id: "260079", nisn: "0105691485", name: "NUR HAISA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NUR+HAISA&entry.201529640=HS", selected: true },
                { id: "260083", nisn: "0103802830", name: "NURHAFIZA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=NURHAFIZA&entry.201529640=HS", selected: true },
                { id: "260087", nisn: "0101679788", name: "PUTRI NABILA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=PUTRI+NABILA&entry.201529640=HS", selected: true },
                { id: "2600893", nisn: "084790876", name: "RASMAN RAM", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RASMAN+RAM&entry.201529640=HS", selected: true },
                { id: "260096", nisn: "0107266947", name: "REVARINDI TINDA", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REVARINDI+TINDA&entry.201529640=HS", selected: true },
                { id: "260097", nisn: "0109887410", name: "REZA AGUNGTAMA", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=REZA+AGUNGTAMA&entry.201529640=HS", selected: true },
                { id: "2601003", nisn: "110853510", name: "RIZKI", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=RIZKI&entry.201529640=HS", selected: true },
                { id: "260104", nisn: "0105182137", name: "SELVIA RAHMADANI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SELVIA+RAHMADANI&entry.201529640=HS", selected: true },
                { id: "260108", nisn: "0111290947", name: "SYAHRINI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=SYAHRINI&entry.201529640=HS", selected: true },
                { id: "260113", nisn: "0106354045", name: "WULAN SAFITRI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=WULAN+SAFITRI&entry.201529640=HS", selected: true },
                { id: "260117", nisn: "0104920937", name: "ZASKIA SULISTYAWATI", gender: "PEREMPUAN", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ZASKIA+SULISTYAWATI&entry.201529640=HS", selected: true }
            ]
        };

        let schoolData = {};
        let selectedStudents = {};
        let currentActiveClassName = '';
        let pendingConfirmCallback = null;

        // Dark Mode Toggle
        function toggleDarkMode() {
            document.documentElement.classList.toggle('dark');
        }

        // Inisialisasi Data dari LocalStorage atau Data Bawaan
        window.addEventListener('DOMContentLoaded', () => {
            loadSchoolData();
            renderClassTabs();
            renderStudentList();
            updateOutputLinks();
            updateStatistics();
        });

        function loadSchoolData() {
            const savedData = localStorage.getItem('sman2_presensi_data_v2');
            if (savedData) {
                try {
                    schoolData = JSON.parse(savedData);
                } catch (e) {
                    schoolData = JSON.parse(JSON.stringify(initialSchoolData));
                }
            } else {
                schoolData = JSON.parse(JSON.stringify(initialSchoolData));
            }

            const classKeys = Object.keys(schoolData);
            if (classKeys.length > 0) {
                if (!currentActiveClassName || !schoolData[currentActiveClassName]) {
                    currentActiveClassName = classKeys[0];
                }
            } else {
                currentActiveClassName = '';
            }

            // Sync selections
            selectedStudents = {};
            Object.keys(schoolData).forEach(className => {
                schoolData[className].forEach(student => {
                    if (student.selected) {
                        selectedStudents[student.id] = true;
                    }
                });
            });
        }

        function saveSchoolData() {
            // Keep student.selected synced with selectedStudents map
            Object.keys(schoolData).forEach(className => {
                schoolData[className].forEach(student => {
                    student.selected = !!selectedStudents[student.id];
                });
            });
            localStorage.setItem('sman2_presensi_data_v2', JSON.stringify(schoolData));
            updateStatistics();
        }

        function resetToDefaultData() {
            showConfirmModal(
                'Reset Data Bawaan',
                'Apakah Anda yakin ingin mengembalikan seluruh data siswa dan kelas ke data awal? Perubahan kustom Anda akan terhapus.',
                () => {
                    localStorage.removeItem('sman2_presensi_data_v2');
                    loadSchoolData();
                    renderClassTabs();
                    renderStudentList();
                    updateOutputLinks();
                    showAlert('Data berhasil dikembalikan ke format awal.');
                }
            );
        }

        function renderClassTabs() {
            const container = document.getElementById('classTabs');
            let html = '';
            
            const classKeys = Object.keys(schoolData);
            classKeys.forEach(className => {
                const isActive = className === currentActiveClassName;
                const btnClass = isActive 
                    ? 'bg-indigo-600 text-white shadow-sm shadow-indigo-500/20' 
                    : 'bg-gray-100 dark:bg-gray-700 text-gray-700 dark:text-gray-300 hover:bg-gray-200 dark:hover:bg-gray-600';
                
                html += `
                    <div class="inline-flex items-center rounded-xl overflow-hidden shadow-sm transition">
                        <button onclick="switchClass('${className}')" class="px-3.5 py-1.5 text-xs font-semibold ${btnClass}">
                            ${className} (${schoolData[className].length})
                        </button>
                        ${classKeys.length > 1 ? `
                            <button onclick="askDeleteClass('${className}')" title="Hapus Kelas ${className}" class="px-2 py-1.5 text-xs ${isActive ? 'bg-indigo-700 text-white hover:bg-indigo-800' : 'bg-gray-200 dark:bg-gray-600 text-gray-500 dark:text-gray-300 hover:bg-red-500 hover:text-white'}">
                                <i class="fa-solid fa-xmark"></i>
                            </button>
                        ` : ''}
                    </div>
                `;
            });

            container.innerHTML = html || '<span class="text-xs text-gray-400">Belum ada kelas. Silakan tambah kelas baru.</span>';
        }

        function switchClass(className) {
            currentActiveClassName = className;
            document.getElementById('activeClassTitle').textContent = `Kelas ${className}`;
            renderClassTabs();
            renderStudentList();
        }

        function renderStudentList() {
            const container = document.getElementById('studentListContainer');
            const searchKeyword = (document.getElementById('searchInput')?.value || '').toLowerCase().trim();
            const students = schoolData[currentActiveClassName] || [];
            
            let html = '';
            let countSelectedInClass = 0;

            const filteredStudents = students.filter(student => {
                if (!searchKeyword) return true;
                return student.name.toLowerCase().includes(searchKeyword) || 
                       student.id.toLowerCase().includes(searchKeyword) ||
                       student.nisn.toLowerCase().includes(searchKeyword);
            });

            if (filteredStudents.length === 0) {
                container.innerHTML = `
                    <div class="flex flex-col items-center justify-center p-8 text-center text-gray-400">
                        <i class="fa-solid fa-folder-open text-3xl mb-2 text-gray-300 dark:text-gray-600"></i>
                        <p class="text-xs font-medium">Tidak ada siswa ditemukan.</p>
                        <button onclick="openAddStudentModal()" class="mt-2 text-xs text-indigo-600 dark:text-indigo-400 font-semibold hover:underline">+ Tambah Siswa Ke Kelas Ini</button>
                    </div>
                `;
                document.getElementById('classSelectedCount').textContent = `0 terpilih di kelas ini`;
                return;
            }

            filteredStudents.forEach(student => {
                const isChecked = selectedStudents[student.id] || false;
                if (isChecked) countSelectedInClass++;

                html += `
                    <div class="flex items-center justify-between p-2.5 rounded-xl border border-gray-100 dark:border-gray-800 bg-white dark:bg-gray-800 hover:bg-indigo-50/50 dark:hover:bg-indigo-900/10 cursor-pointer transition gap-2">
                        <label class="flex items-center space-x-3 flex-1 cursor-pointer min-w-0">
                            <input type="checkbox" value="${student.id}" ${isChecked ? 'checked' : ''} onchange="toggleStudent('${student.id}')" class="w-4 h-4 text-indigo-600 rounded border-gray-300 focus:ring-indigo-500 flex-shrink-0">
                            <div class="truncate">
                                <p class="text-xs font-bold text-gray-800 dark:text-gray-200 truncate">
                                    ${student.name} 
                                    <span class="font-normal text-[10px] text-gray-400">(${student.gender})</span>
                                </p>
                                <p class="text-[10px] text-gray-400 font-mono">NIS: ${student.id} &bull; NISN: ${student.nisn}</p>
                            </div>
                        </label>
                        <div class="flex items-center space-x-1 flex-shrink-0">
                            <span class="text-[10px] px-2 py-0.5 rounded-full ${isChecked ? 'bg-green-100 text-green-700 dark:bg-green-900/40 dark:text-green-300 font-semibold' : 'bg-gray-100 text-gray-400 dark:bg-gray-700 dark:text-gray-400'}">
                                ${isChecked ? 'Dipilih' : 'Tidak'}
                            </span>
                            <button onclick="openEditStudentModal('${currentActiveClassName}', '${student.id}')" class="p-1.5 text-gray-400 hover:text-indigo-600 dark:hover:text-indigo-400 text-xs transition" title="Edit Data Siswa">
                                <i class="fa-solid fa-pen-to-square"></i>
                            </button>
                            <button onclick="askDeleteStudent('${currentActiveClassName}', '${student.id}', '${student.name}')" class="p-1.5 text-gray-400 hover:text-red-600 dark:hover:text-red-400 text-xs transition" title="Hapus Siswa">
                                <i class="fa-solid fa-trash-can"></i>
                            </button>
                        </div>
                    </div>
                `;
            });

            container.innerHTML = html;
            document.getElementById('classSelectedCount').textContent = `${countSelectedInClass} terpilih di kelas ini`;
        }

        function toggleStudent(studentId) {
            selectedStudents[studentId] = !selectedStudents[studentId];
            saveSchoolData();
            renderStudentList();
            updateOutputLinks();
        }

        function selectAll(status) {
            const students = schoolData[currentActiveClassName] || [];
            students.forEach(student => {
                selectedStudents[student.id] = status;
            });
            saveSchoolData();
            renderStudentList();
            updateOutputLinks();
        }

        function applyGlobalLink() {
            const customUrl = document.getElementById('globalLinkInput').value.trim();
            if (!customUrl) {
                showAlert('Masukkan tautan terlebih dahulu pada kotak konfigurasi.');
                return;
            }

            const students = schoolData[currentActiveClassName] || [];
            students.forEach(student => {
                let formatted = customUrl;
                if (formatted.includes('{nama}')) {
                    formatted = formatted.replace(/{nama}/g, encodeURIComponent(student.name));
                }
                if (formatted.includes('{nis}')) {
                    formatted = formatted.replace(/{nis}/g, student.id);
                }
                student.link = formatted;
            });

            saveSchoolData();
            renderStudentList();
            updateOutputLinks();
            showAlert(`Tautan untuk ${currentActiveClassName} berhasil diperbarui!`);
        }

        function updateOutputLinks() {
            let collectedLinks = [];

            Object.keys(schoolData).forEach(className => {
                schoolData[className].forEach(student => {
                    if (selectedStudents[student.id]) {
                        collectedLinks.push(student.link || generateDefaultStudentLink(student.name));
                    }
                });
            });

            document.getElementById('outputLinkArea').value = collectedLinks.join('\n');
            document.getElementById('totalSelectedBadge').textContent = `${collectedLinks.length} Tautan`;
        }

        function generateDefaultStudentLink(name) {
            const baseUrl = "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url";
            return `${baseUrl}&entry.1687779044=${encodeURIComponent(name)}&entry.201529640=HS`;
        }

        function updateStatistics() {
            let totalStudents = 0;
            const classKeys = Object.keys(schoolData);
            
            classKeys.forEach(c => {
                totalStudents += schoolData[c].length;
            });

            document.getElementById('statTotalStudents').textContent = totalStudents;
            document.getElementById('statTotalClasses').textContent = classKeys.length;
        }

        function populateClassDropdown(selectedClass) {
            const select = document.getElementById('modalStudentClass');
            select.innerHTML = '';
            Object.keys(schoolData).forEach(c => {
                const opt = document.createElement('option');
                opt.value = c;
                opt.textContent = c;
                if (c === selectedClass) opt.selected = true;
                select.appendChild(opt);
            });
        }

        function openAddStudentModal() {
            if (Object.keys(schoolData).length === 0) {
                showAlert('Silakan buat kelas terlebih dahulu sebelum menambah siswa!');
                return;
            }
            document.getElementById('studentModalTitle').textContent = 'Tambah Siswa Baru';
            document.getElementById('editOriginalClass').value = '';
            document.getElementById('editOriginalId').value = '';
            document.getElementById('studentForm').reset();
            
            populateClassDropdown(currentActiveClassName);
            document.getElementById('studentModal').classList.remove('hidden');
        }

        function openEditStudentModal(className, studentId) {
            const student = (schoolData[className] || []).find(s => s.id === studentId);
            if (!student) return;

            document.getElementById('studentModalTitle').textContent = 'Edit Data Siswa';
            document.getElementById('editOriginalClass').value = className;
            document.getElementById('editOriginalId').value = studentId;

            populateClassDropdown(className);
            document.getElementById('modalStudentId').value = student.id;
            document.getElementById('modalStudentNisn').value = student.nisn;
            document.getElementById('modalStudentName').value = student.name;
            document.getElementById('modalStudentGender').value = student.gender;
            document.getElementById('modalStudentLink').value = student.link || '';

            document.getElementById('studentModal').classList.remove('hidden');
        }

        function closeStudentModal() {
            document.getElementById('studentModal').classList.add('hidden');
        }

        function handleSaveStudent(e) {
            e.preventDefault();

            const origClass = document.getElementById('editOriginalClass').value;
            const origId = document.getElementById('editOriginalId').value;

            const targetClass = document.getElementById('modalStudentClass').value;
            const newId = document.getElementById('modalStudentId').value.trim();
            const newNisn = document.getElementById('modalStudentNisn').value.trim();
            const newName = document.getElementById('modalStudentName').value.trim().toUpperCase();
            const newGender = document.getElementById('modalStudentGender').value;
            let newLink = document.getElementById('modalStudentLink').value.trim();

            if (!newLink) {
                newLink = generateDefaultStudentLink(newName);
            }

            // Check duplicate ID if new or ID changed
            let isDuplicate = false;
            Object.keys(schoolData).forEach(c => {
                schoolData[c].forEach(s => {
                    if (s.id === newId && !(c === origClass && s.id === origId)) {
                        isDuplicate = true;
                    }
                });
            });

            if (isDuplicate) {
                showAlert('NIS/ID Siswa sudah digunakan oleh siswa lain! Gunakan NIS unik.');
                return;
            }

            // If edit, remove old record
            if (origClass && origId) {
                const isSelectedPrev = selectedStudents[origId];
                delete selectedStudents[origId];

                schoolData[origClass] = schoolData[origClass].filter(s => s.id !== origId);
                selectedStudents[newId] = isSelectedPrev !== undefined ? isSelectedPrev : true;
            } else {
                selectedStudents[newId] = true;
            }

            // Add new or updated student
            const studentObj = {
                id: newId,
                nisn: newNisn,
                name: newName,
                gender: newGender,
                link: newLink,
                selected: selectedStudents[newId]
            };

            if (!schoolData[targetClass]) {
                schoolData[targetClass] = [];
            }
            schoolData[targetClass].push(studentObj);

            saveSchoolData();
            currentActiveClassName = targetClass;
            renderClassTabs();
            renderStudentList();
            updateOutputLinks();
            closeStudentModal();
            showAlert(`Data siswa "${newName}" berhasil disimpan.`);
        }

        function openAddClassModal() {
            document.getElementById('newClassNameInput').value = '';
            document.getElementById('classModal').classList.remove('hidden');
        }

        function closeClassModal() {
            document.getElementById('classModal').classList.add('hidden');
        }

        function handleSaveClass(e) {
            e.preventDefault();
            const nameInput = document.getElementById('newClassNameInput').value.trim();
            if (!nameInput) return;

            let formattedClassName = nameInput.startsWith('Kelas') ? nameInput : `Kelas ${nameInput}`;

            if (schoolData[formattedClassName]) {
                showAlert(`Kelas dengan nama "${formattedClassName}" sudah ada!`);
                return;
            }

            schoolData[formattedClassName] = [];
            saveSchoolData();
            currentActiveClassName = formattedClassName;
            renderClassTabs();
            renderStudentList();
            closeClassModal();
            showAlert(`Kelas "${formattedClassName}" berhasil ditambahkan.`);
        }

        function askDeleteStudent(className, studentId, studentName) {
            showConfirmModal(
                'Hapus Data Siswa',
                `Apakah Anda yakin ingin menghapus data siswa "${studentName}" dari ${className}?`,
                () => {
                    schoolData[className] = schoolData[className].filter(s => s.id !== studentId);
                    delete selectedStudents[studentId];
                    saveSchoolData();
                    renderStudentList();
                    updateOutputLinks();
                    showAlert(`Siswa "${studentName}" telah dihapus.`);
                }
            );
        }

        function askDeleteClass(className) {
            showConfirmModal(
                'Hapus Kelas',
                `Apakah Anda yakin ingin menghapus seluruh ${className} beserta data seluruh siswanya?`,
                () => {
                    (schoolData[className] || []).forEach(s => delete selectedStudents[s.id]);
                    delete schoolData[className];
                    saveSchoolData();

                    const remainingClasses = Object.keys(schoolData);
                    currentActiveClassName = remainingClasses.length > 0 ? remainingClasses[0] : '';
                    renderClassTabs();
                    renderStudentList();
                    updateOutputLinks();
                    showAlert(`"${className}" telah dihapus.`);
                }
            );
        }

        function processAndOpen() {
            const outputText = document.getElementById('outputLinkArea').value.trim();
            if (!outputText) {
                showAlert('Belum ada siswa yang dicentang atau tautan kosong!');
                return;
            }

            const links = outputText.split('\n').filter(l => l.trim().length > 0);
            
            let index = 0;
            function openNext() {
                if (index < links.length) {
                    let formattedUrl = links[index];
                    if (!/^https?:\/\//i.test(formattedUrl)) {
                        formattedUrl = 'https://' + formattedUrl;
                    }
                    window.open(formattedUrl, '_blank');
                    index++;
                    setTimeout(openNext, 300);
                }
            }
            openNext();
        }

        function copyAllOutputLinks() {
            const outputText = document.getElementById('outputLinkArea').value;
            if (!outputText) {
                showAlert('Tidak ada tautan untuk disalin.');
                return;
            }

            copyLegacy(outputText);
        }

        function copyLegacy(text) {
            const textarea = document.createElement('textarea');
            textarea.value = text;
            document.body.appendChild(textarea);
            textarea.select();
            try {
                document.execCommand('copy');
                showAlert('Semua tautan terkumpul berhasil disalin ke papan klip!');
            } catch (err) {
                showAlert('Gagal menyalin tautan.');
            }
            document.body.removeChild(textarea);
        }

        function exportDataJSON() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(schoolData, null, 2));
            const downloadAnchor = document.createElement('a');
            downloadAnchor.setAttribute("href", dataStr);
            downloadAnchor.setAttribute("download", `presensi_sman2_nusa_${new Date().toISOString().slice(0,10)}.json`);
            document.body.appendChild(downloadAnchor);
            downloadAnchor.click();
            downloadAnchor.remove();
            showAlert('File JSON cadangan data siswa berhasil diunduh.');
        }

        function importDataJSON(event) {
            const file = event.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const importedObj = JSON.parse(e.target.result);
                    if (typeof importedObj === 'object' && importedObj !== null) {
                        schoolData = importedObj;
                        saveSchoolData();
                        loadSchoolData();
                        renderClassTabs();
                        renderStudentList();
                        updateOutputLinks();
                        showAlert('Data presensi berhasil diimpor!');
                    } else {
                        showAlert('Format file JSON tidak valid.');
                    }
                } catch (err) {
                    showAlert('Gagal membaca file JSON.');
                }
            };
            reader.readAsText(file);
        }

        function showConfirmModal(title, message, callback) {
            document.getElementById('confirmTitle').textContent = title;
            document.getElementById('confirmMessage').textContent = message;
            pendingConfirmCallback = callback;
            
            const btn = document.getElementById('confirmExecuteBtn');
            btn.onclick = function() {
                if (pendingConfirmCallback) pendingConfirmCallback();
                closeConfirmModal();
            };

            document.getElementById('confirmModal').classList.remove('hidden');
        }

        function closeConfirmModal() {
            document.getElementById('confirmModal').classList.add('hidden');
            pendingConfirmCallback = null;
        }

        function showAlert(msg) {
            const alertBox = document.getElementById('alertBox');
            const alertText = document.getElementById('alertText');
            alertText.textContent = msg;
            alertBox.classList.remove('hidden');
            setTimeout(() => {
                hideAlert();
            }, 4000);
        }

        function hideAlert() {
            document.getElementById('alertBox').classList.add('hidden');
        }
    </script>
</body>
</html>
