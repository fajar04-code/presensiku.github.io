<!DOCTYPE html>
<html lang="id" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Presensi Kehadiran SMAN 2 Nusa</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: { 50: '#eef2ff', 500: '#6366f1', 600: '#4f46e5', 700: '#4338ca' }
                    },
                    fontFamily: {
                        sans: ['Inter', 'ui-sans-serif', 'system-ui', '-apple-system', 'BlinkMacSystemFont', 'Segoe UI', 'Roboto', 'Helvetica Neue', 'Arial', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body { font-family: 'Inter', sans-serif; }
        /* Custom Scrollbar for better UI */
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 10px; }
        .dark ::-webkit-scrollbar-thumb { background: #475569; }
        ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
    </style>
</head>
<body class="bg-gray-50 dark:bg-gray-900 text-gray-800 dark:text-gray-100 h-full flex flex-col transition-colors duration-300">

    <!-- Header -->
    <header class="bg-white dark:bg-gray-800 border-b border-gray-200 dark:border-gray-700 shadow-sm py-4 px-4 sm:px-6 flex flex-col md:flex-row justify-between items-center gap-4 sticky top-0 z-40">
        <div class="flex items-center space-x-3 w-full md:w-auto">
            <div class="bg-indigo-600 text-white p-2.5 rounded-xl shadow-md flex-shrink-0">
                <i class="fa-solid fa-school text-xl"></i>
            </div>
            <div>
                <h1 class="text-xl font-bold tracking-tight text-gray-900 dark:text-white leading-tight">Presensi Kehadiran</h1>
                <p class="text-xs text-gray-500 dark:text-gray-400">SMAN 2 Nusa - Kelola Data & Tautan Otomatis</p>
            </div>
        </div>
        
        <div class="flex items-center flex-wrap gap-2 w-full md:w-auto justify-start md:justify-end">
            <button onclick="openAddStudentModal()" class="px-3 py-2 text-xs font-semibold rounded-xl bg-indigo-600 text-white hover:bg-indigo-700 shadow-sm transition flex items-center gap-1.5">
                <i class="fa-solid fa-user-plus"></i><span class="hidden sm:inline">Siswa</span>
            </button>
            <button onclick="openBulkStudentModal()" class="px-3 py-2 text-xs font-semibold rounded-xl bg-violet-600 text-white hover:bg-violet-700 shadow-sm transition flex items-center gap-1.5">
                <i class="fa-solid fa-users"></i><span class="hidden sm:inline">Massal</span>
            </button>
            <button onclick="openAddClassModal()" class="px-3 py-2 text-xs font-semibold rounded-xl bg-emerald-600 text-white hover:bg-emerald-700 shadow-sm transition flex items-center gap-1.5">
                <i class="fa-solid fa-folder-plus"></i><span class="hidden sm:inline">Kelas</span>
            </button>
            <div class="w-px h-6 bg-gray-300 dark:bg-gray-600 mx-1"></div>
            <button onclick="exportDataJSON()" class="p-2.5 text-xs font-medium rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition text-gray-600 dark:text-gray-300" title="Ekspor Data (Backup JSON)">
                <i class="fa-solid fa-download"></i>
            </button>
            <label class="p-2.5 text-xs font-medium rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 cursor-pointer transition text-gray-600 dark:text-gray-300" title="Impor Data (Upload JSON)">
                <i class="fa-solid fa-upload"></i>
                <input type="file" id="importJsonInput" accept=".json" onchange="importDataJSON(event)" class="hidden">
            </label>
            <button onclick="toggleDarkMode()" class="p-2.5 rounded-xl bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 transition text-gray-600 dark:text-gray-300" title="Ganti Tema">
                <i class="fa-solid fa-moon dark:hidden"></i>
                <i class="fa-solid fa-sun hidden dark:block text-yellow-400"></i>
            </button>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-1 w-full max-w-[1400px] mx-auto p-4 md:p-6 grid grid-cols-1 lg:grid-cols-12 gap-6 overflow-y-auto">

        <!-- Notification Banner -->
        <div id="alertBox" class="col-span-1 lg:col-span-12 hidden bg-indigo-50 dark:bg-indigo-900/40 border border-indigo-200 dark:border-indigo-800 text-indigo-800 dark:text-indigo-200 px-4 py-3 rounded-xl items-center justify-between text-sm shadow-sm transition-all">
            <div class="flex items-center space-x-3">
                <i class="fa-solid fa-circle-info text-indigo-500 text-lg"></i>
                <span id="alertText" class="font-medium">Pesan peringatan.</span>
            </div>
            <button onclick="hideAlert()" class="text-indigo-600 hover:text-indigo-800 dark:text-indigo-400 font-bold p-1">&times;</button>
        </div>

        <!-- Kolom Kiri: Daftar Siswa Berdasarkan Kelas & Pengaturan Tautan -->
        <div class="lg:col-span-7 flex flex-col gap-6">
            
            <!-- Konfigurasi Tautan / Format Link per Kelas -->
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl shadow-sm border border-gray-200 dark:border-gray-700 flex flex-col gap-3 transition-colors duration-300">
                <div class="flex justify-between items-center">
                    <h2 class="font-semibold text-sm flex items-center gap-2 text-gray-800 dark:text-gray-200">
                        <i class="fa-solid fa-link text-indigo-500"></i> Pola Tautan Presensi Hadir
                    </h2>
                    <button onclick="resetToDefaultData()" class="text-[11px] text-red-500 hover:text-red-700 hover:underline flex items-center gap-1 transition">
                        <i class="fa-solid fa-rotate-left"></i> Reset Data Awal
                    </button>
                </div>
                <p class="text-xs text-gray-500 dark:text-gray-400">Masukkan tautan Google Forms utama. Gunakan <code class="bg-gray-100 dark:bg-gray-700 px-1 py-0.5 rounded text-indigo-600 dark:text-indigo-400 font-mono">{nama}</code> atau <code class="bg-gray-100 dark:bg-gray-700 px-1 py-0.5 rounded text-indigo-600 dark:text-indigo-400 font-mono">{nis}</code> untuk kustomisasi per siswa.</p>
                
                <div class="flex flex-col sm:flex-row gap-2 mt-1">
                    <input type="text" id="globalLinkInput" placeholder="https://docs.google.com/forms/.../entry.123={nama}&entry.456={nis}" class="flex-1 p-2.5 text-xs rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 focus:outline-none transition-all dark:text-white">
                    <button onclick="applyGlobalLink()" class="px-4 py-2 text-xs font-semibold rounded-xl bg-indigo-600 text-white hover:bg-indigo-700 shadow-sm transition whitespace-nowrap active:scale-95">Terapkan ke Kelas Ini</button>
                </div>
            </div>

            <!-- Bagian Pemilihan Siswa Per Kelas -->
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl shadow-sm border border-gray-200 dark:border-gray-700 flex flex-col gap-4 flex-1 transition-colors duration-300 min-h-[500px]">
                
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-3 border-b border-gray-100 dark:border-gray-700 pb-3">
                    <h2 class="font-semibold text-sm flex items-center gap-2 text-gray-800 dark:text-gray-200">
                        <i class="fa-solid fa-users-viewfinder text-indigo-500"></i> Direktori Siswa
                    </h2>
                    <div class="flex items-center gap-2 w-full sm:w-auto">
                        <button onclick="selectAll(true)" class="flex-1 sm:flex-none px-3 py-1.5 text-xs font-medium rounded-lg bg-indigo-50 dark:bg-indigo-900/30 text-indigo-600 dark:text-indigo-400 hover:bg-indigo-100 dark:hover:bg-indigo-900/50 transition">Pilih Semua</button>
                        <button onclick="selectAll(false)" class="flex-1 sm:flex-none px-3 py-1.5 text-xs font-medium rounded-lg bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-300 hover:bg-gray-200 dark:hover:bg-gray-600 transition">Batalkan</button>
                    </div>
                </div>

                <!-- Tab Kelas Selector -->
                <div id="classTabs" class="flex flex-wrap gap-2 items-center">
                    <!-- Dinamis via JS -->
                </div>

                <!-- Filter & Search Bar -->
                <div class="relative mt-2">
                    <i class="fa-solid fa-magnifying-glass absolute left-3 top-3 text-xs text-gray-400"></i>
                    <input type="text" id="searchInput" oninput="renderStudentList()" placeholder="Cari berdasarkan nama, NIS, atau NISN..." class="w-full pl-8 pr-3 py-2.5 text-xs rounded-xl border border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-900 focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 focus:outline-none transition-all dark:text-white shadow-inner">
                </div>

                <!-- Kontainer Info Daftar Siswa -->
                <div class="flex justify-between items-center text-xs text-gray-500 dark:text-gray-400 px-1 mt-1">
                    <span id="activeClassTitle" class="font-bold text-gray-700 dark:text-gray-300 bg-gray-100 dark:bg-gray-700 px-2 py-1 rounded-md">Pilih Kelas</span>
                    <span id="classSelectedCount" class="font-medium">0 terpilih di kelas ini</span>
                </div>

                <!-- Scrollable Student List -->
                <div id="studentListContainer" class="flex-1 overflow-y-auto border border-gray-100 dark:border-gray-700 rounded-xl p-3 bg-gray-50/50 dark:bg-gray-900/30 flex flex-col gap-2">
                    <!-- Dinamis via JS -->
                </div>
            </div>

        </div>

        <!-- Kolom Kanan: Menu Presensi Khusus & Hasil Tautan -->
        <div class="lg:col-span-5 flex flex-col gap-6">
            
            <!-- Integrasi Kartu: Menu Presensi Khusus -->
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl shadow-sm border border-gray-200 dark:border-gray-700 flex flex-col gap-4 transition-colors duration-300">
                <div class="flex flex-col border-b border-gray-100 dark:border-gray-700 pb-3">
                    <h2 class="font-semibold text-sm flex items-center gap-2 text-gray-800 dark:text-gray-200">
                        <i class="fa-solid fa-circle-exclamation text-amber-500"></i> Menu Presensi Khusus
                    </h2>
                    <span class="text-[11px] text-gray-500 dark:text-gray-400 mt-1">Gunakan tautan di bawah ini untuk menginput presensi siswa yang tidak hadir secara langsung.</span>
                </div>
                
                <div class="grid grid-cols-2 gap-3">
                    <!-- Tombol SAKIT -->
                    <a href="https://forms.gle/c4dMAXtYNpahjm4F8" target="_blank" rel="noopener noreferrer" class="group flex flex-col items-center justify-center gap-2 p-3 bg-blue-50 hover:bg-blue-500 text-blue-600 hover:text-white dark:bg-blue-900/20 dark:hover:bg-blue-600 dark:text-blue-400 dark:hover:text-white border border-blue-200 dark:border-blue-800 rounded-xl transition-all duration-300 shadow-sm hover:shadow-md">
                        <div class="bg-white dark:bg-gray-800 p-2 rounded-full group-hover:bg-blue-400 dark:group-hover:bg-blue-500 transition-colors">
                            <i class="fa-solid fa-bed-pulse text-lg"></i>
                        </div>
                        <span class="text-xs font-bold tracking-wide">SAKIT</span>
                    </a>
                    
                    <!-- Tombol IZIN -->
                    <a href="https://forms.gle/sQYzvpgkqvaqeY1q6" target="_blank" rel="noopener noreferrer" class="group flex flex-col items-center justify-center gap-2 p-3 bg-yellow-50 hover:bg-yellow-500 text-yellow-600 hover:text-white dark:bg-yellow-900/20 dark:hover:bg-yellow-600 dark:text-yellow-400 dark:hover:text-white border border-yellow-200 dark:border-yellow-800 rounded-xl transition-all duration-300 shadow-sm hover:shadow-md">
                        <div class="bg-white dark:bg-gray-800 p-2 rounded-full group-hover:bg-yellow-400 dark:group-hover:bg-yellow-500 transition-colors">
                            <i class="fa-solid fa-envelope-open-text text-lg"></i>
                        </div>
                        <span class="text-xs font-bold tracking-wide">IZIN</span>
                    </a>
                    
                    <!-- Tombol TERLAMBAT -->
                    <a href="https://forms.gle/AGDTUVeq7MmFkSV38" target="_blank" rel="noopener noreferrer" class="group flex flex-col items-center justify-center gap-2 p-3 bg-orange-50 hover:bg-orange-500 text-orange-600 hover:text-white dark:bg-orange-900/20 dark:hover:bg-orange-600 dark:text-orange-400 dark:hover:text-white border border-orange-200 dark:border-orange-800 rounded-xl transition-all duration-300 shadow-sm hover:shadow-md">
                        <div class="bg-white dark:bg-gray-800 p-2 rounded-full group-hover:bg-orange-400 dark:group-hover:bg-orange-500 transition-colors">
                            <i class="fa-solid fa-person-running text-lg"></i>
                        </div>
                        <span class="text-xs font-bold tracking-wide">TERLAMBAT</span>
                    </a>
                    
                    <!-- Tombol BOLOS -->
                    <a href="https://forms.gle/XHoob5yMRTac19y9A" target="_blank" rel="noopener noreferrer" class="group flex flex-col items-center justify-center gap-2 p-3 bg-red-50 hover:bg-red-500 text-red-600 hover:text-white dark:bg-red-900/20 dark:hover:bg-red-600 dark:text-red-400 dark:hover:text-white border border-red-200 dark:border-red-800 rounded-xl transition-all duration-300 shadow-sm hover:shadow-md">
                        <div class="bg-white dark:bg-gray-800 p-2 rounded-full group-hover:bg-red-400 dark:group-hover:bg-red-500 transition-colors">
                            <i class="fa-solid fa-user-xmark text-lg"></i>
                        </div>
                        <span class="text-xs font-bold tracking-wide">BOLOS</span>
                    </a>
                </div>
            </div>

            <!-- Kartu Hasil Tautan -->
            <div class="bg-white dark:bg-gray-800 p-5 rounded-2xl shadow-sm border border-gray-200 dark:border-gray-700 flex flex-col gap-4 flex-1 transition-colors duration-300">
                <div class="flex-1 flex flex-col">
                    <div class="flex justify-between items-center border-b border-gray-100 dark:border-gray-700 pb-3">
                        <h2 class="font-semibold text-sm flex items-center gap-2 text-gray-800 dark:text-gray-200">
                            <i class="fa-solid fa-clipboard-list text-indigo-500"></i> Hasil Tautan Terkumpul
                        </h2>
                        <span id="totalSelectedBadge" class="bg-indigo-100 dark:bg-indigo-900/50 text-indigo-700 dark:text-indigo-300 px-3 py-1 rounded-full text-xs font-bold shadow-inner">0 Tautan</span>
                    </div>

                    <p class="text-[11px] text-gray-500 dark:text-gray-400 mt-3 mb-2">Tautan presensi dari siswa yang dicentang di semua kelas akan tergabung secara otomatis di sini:</p>

                    <!-- Output Textarea -->
                    <textarea id="outputLinkArea" readonly rows="12" placeholder="Pilih siswa pada direktori sebelah kiri untuk memunculkan tautannya di sini..." class="w-full flex-1 min-h-[200px] p-3.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs text-gray-700 dark:text-gray-300 focus:outline-none focus:ring-2 focus:ring-indigo-500 font-mono transition resize-none shadow-inner"></textarea>
                </div>

                <!-- Statistik Ringkas -->
                <div class="grid grid-cols-2 gap-3 p-3 bg-gray-50 dark:bg-gray-900/60 rounded-xl border border-gray-100 dark:border-gray-800 text-xs mt-auto">
                    <div class="flex flex-col">
                        <span class="text-gray-400 dark:text-gray-500 text-[10px] uppercase font-bold tracking-wider">Total Siswa</span>
                        <span id="statTotalStudents" class="font-bold text-gray-700 dark:text-gray-200 text-lg">0</span>
                    </div>
                    <div class="flex flex-col border-l border-gray-200 dark:border-gray-700 pl-3">
                        <span class="text-gray-400 dark:text-gray-500 text-[10px] uppercase font-bold tracking-wider">Total Kelas</span>
                        <span id="statTotalClasses" class="font-bold text-gray-700 dark:text-gray-200 text-lg">0</span>
                    </div>
                </div>

                <!-- Action Buttons -->
                <div class="flex flex-col gap-2 pt-1">
                    <button onclick="processAndOpen()" class="w-full py-3 text-sm font-semibold rounded-xl bg-indigo-600 text-white hover:bg-indigo-700 shadow-md shadow-indigo-500/20 transition-all flex items-center justify-center gap-2 active:scale-[0.98]">
                        <i class="fa-solid fa-rocket"></i> Buka Semua Tautan (Tab Baru)
                    </button>
                    <button onclick="copyAllOutputLinks()" class="w-full py-2.5 text-sm font-medium rounded-xl bg-gray-100 dark:bg-gray-700 text-gray-700 dark:text-gray-200 hover:bg-gray-200 dark:hover:bg-gray-600 transition-all flex items-center justify-center gap-2 active:scale-[0.98]">
                        <i class="fa-regular fa-copy"></i> Salin Semua Tautan
                    </button>
                </div>
            </div>

        </div>

    </main>

    <!-- Modal Tambah / Edit Siswa -->
    <div id="studentModal" class="fixed inset-0 bg-gray-900/60 backdrop-blur-sm z-50 hidden items-center justify-center p-4 opacity-0 transition-opacity duration-300">
        <div class="bg-white dark:bg-gray-800 rounded-2xl max-w-md w-full p-6 shadow-2xl border border-gray-100 dark:border-gray-700 flex flex-col gap-4 transform scale-95 transition-transform duration-300">
            <div class="flex justify-between items-center border-b border-gray-100 dark:border-gray-700 pb-3">
                <h3 id="studentModalTitle" class="font-bold text-base text-gray-800 dark:text-gray-100">Tambah Siswa Baru</h3>
                <button onclick="closeModal('studentModal')" class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-200 text-lg transition-colors p-1"><i class="fa-solid fa-xmark"></i></button>
            </div>

            <form id="studentForm" onsubmit="handleSaveStudent(event)" class="flex flex-col gap-3 text-xs">
                <input type="hidden" id="editOriginalClass">
                <input type="hidden" id="editOriginalId">

                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Kelas Target <span class="text-red-500">*</span></label>
                    <select id="modalStudentClass" required class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none dark:text-white"></select>
                </div>

                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">NIS (ID Unik) <span class="text-red-500">*</span></label>
                        <input type="text" id="modalStudentId" required placeholder="Contoh: 260120" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none dark:text-white">
                    </div>
                    <div>
                        <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">NISN</label>
                        <input type="text" id="modalStudentNisn" placeholder="Opsional: 0105432109" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none dark:text-white">
                    </div>
                </div>

                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Nama Lengkap Siswa <span class="text-red-500">*</span></label>
                    <input type="text" id="modalStudentName" required placeholder="Contoh: AHMAD FAUZI" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none dark:text-white">
                </div>

                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Jenis Kelamin</label>
                    <select id="modalStudentGender" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none dark:text-white">
                        <option value="LAKI-LAKI">LAKI-LAKI</option>
                        <option value="PEREMPUAN">PEREMPUAN</option>
                    </select>
                </div>

                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Tautan Presensi Khusus (Opsional)</label>
                    <input type="url" id="modalStudentLink" placeholder="Kosongkan agar memakai template kelas" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-indigo-500 focus:outline-none dark:text-white">
                </div>

                <div class="flex justify-end gap-2 pt-3 border-t border-gray-100 dark:border-gray-700 mt-2">
                    <button type="button" onclick="closeModal('studentModal')" class="px-4 py-2 rounded-xl bg-gray-100 dark:bg-gray-700 text-gray-700 dark:text-gray-200 hover:bg-gray-200 dark:hover:bg-gray-600 transition font-medium">Batal</button>
                    <button type="submit" class="px-5 py-2 rounded-xl bg-indigo-600 text-white hover:bg-indigo-700 font-semibold transition shadow-sm shadow-indigo-500/30">Simpan Data</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Input Siswa Massal -->
    <div id="bulkStudentModal" class="fixed inset-0 bg-gray-900/60 backdrop-blur-sm z-50 hidden items-center justify-center p-4 opacity-0 transition-opacity duration-300">
        <div class="bg-white dark:bg-gray-800 rounded-2xl max-w-3xl w-full p-6 shadow-2xl border border-gray-100 dark:border-gray-700 flex flex-col gap-4 transform scale-95 transition-transform duration-300">
            <div class="flex justify-between items-center border-b border-gray-100 dark:border-gray-700 pb-3">
                <div>
                    <h3 class="font-bold text-base text-gray-800 dark:text-gray-100">Input Data Siswa Massal</h3>
                    <p class="text-[11px] text-gray-400 mt-1">Masukkan banyak siswa sekaligus dengan format tabular.</p>
                </div>
                <button onclick="closeModal('bulkStudentModal')" class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-200 text-lg transition p-1"><i class="fa-solid fa-xmark"></i></button>
            </div>

            <div class="flex flex-col gap-3 text-xs">
                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1">Target Kelas</label>
                    <select id="bulkStudentClass" class="w-full p-2.5 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs focus:ring-2 focus:ring-violet-500 focus:outline-none dark:text-white"></select>
                </div>

                <div class="bg-violet-50 dark:bg-violet-900/30 border border-violet-100 dark:border-violet-800 rounded-xl p-3 text-[11px] text-violet-800 dark:text-violet-200 shadow-inner">
                    <b>Format:</b> satu siswa per baris. Gunakan pemisah Tab, Koma (,) atau Titik Koma (;). Urutan Kolom:<br>
                    <code class="font-mono bg-white dark:bg-gray-900 px-1 py-0.5 rounded border border-violet-100 dark:border-violet-700 inline-block mt-1">NIS [TAB] NISN [TAB] NAMA LENGKAP [TAB] JENIS KELAMIN</code><br>
                    <span class="text-violet-600 dark:text-violet-300 mt-1 block">*Bisa langsung copy-paste dari Excel atau Google Sheets.</span>
                </div>

                <textarea id="bulkStudentData" rows="10" spellcheck="false" placeholder="Contoh Data:&#10;260120&#9;0101234567&#9;AHMAD FAUZI&#9;LAKI-LAKI&#10;260121&#9;0101234568&#9;SITI AISYAH&#9;PEREMPUAN" class="w-full p-3 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-xs font-mono focus:ring-2 focus:ring-violet-500 focus:outline-none resize-y dark:text-white shadow-inner"></textarea>

                <div class="flex items-center justify-between gap-2 mt-2">
                    <button type="button" onclick="fillBulkExample()" class="px-3 py-2 rounded-xl bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-300 hover:bg-gray-200 dark:hover:bg-gray-600 transition font-medium flex items-center gap-1">
                        <i class="fa-solid fa-wand-magic-sparkles"></i> Contoh Format
                    </button>
                    <div class="flex gap-2">
                        <button type="button" onclick="closeModal('bulkStudentModal')" class="px-4 py-2 rounded-xl bg-gray-100 dark:bg-gray-700 text-gray-700 dark:text-gray-200 hover:bg-gray-200 dark:hover:bg-gray-600 transition font-medium">Batal</button>
                        <button type="button" onclick="handleBulkSaveStudents()" class="px-5 py-2 rounded-xl bg-violet-600 text-white hover:bg-violet-700 font-semibold transition shadow-sm shadow-violet-500/30">
                            Simpan Massal
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal Tambah Kelas -->
    <div id="classModal" class="fixed inset-0 bg-gray-900/60 backdrop-blur-sm z-50 hidden items-center justify-center p-4 opacity-0 transition-opacity duration-300">
        <div class="bg-white dark:bg-gray-800 rounded-2xl max-w-sm w-full p-6 shadow-2xl border border-gray-100 dark:border-gray-700 flex flex-col gap-4 transform scale-95 transition-transform duration-300">
            <div class="flex justify-between items-center border-b border-gray-100 dark:border-gray-700 pb-3">
                <h3 class="font-bold text-base text-gray-800 dark:text-gray-100">Buat Kelas Baru</h3>
                <button onclick="closeModal('classModal')" class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-200 text-lg transition p-1"><i class="fa-solid fa-xmark"></i></button>
            </div>

            <form onsubmit="handleSaveClass(event)" class="flex flex-col gap-4 text-xs mt-1">
                <div>
                    <label class="font-medium text-gray-600 dark:text-gray-400 block mb-1.5">Nama Kelas (Wajib Unik) <span class="text-red-500">*</span></label>
                    <input type="text" id="newClassNameInput" required placeholder="Contoh: Kelas XII-MIPA 1" class="w-full p-3 rounded-xl border border-gray-300 dark:border-gray-600 bg-gray-50 dark:bg-gray-900 text-sm focus:ring-2 focus:ring-emerald-500 focus:outline-none dark:text-white">
                </div>

                <div class="flex justify-end gap-2 pt-2">
                    <button type="button" onclick="closeModal('classModal')" class="px-4 py-2.5 rounded-xl bg-gray-100 dark:bg-gray-700 text-gray-700 dark:text-gray-200 hover:bg-gray-200 dark:hover:bg-gray-600 transition font-medium">Batal</button>
                    <button type="submit" class="px-5 py-2.5 rounded-xl bg-emerald-600 text-white hover:bg-emerald-700 font-semibold transition shadow-sm shadow-emerald-500/30">Tambah Kelas</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Modal Konfirmasi Hapus -->
    <div id="confirmModal" class="fixed inset-0 bg-gray-900/60 backdrop-blur-sm z-50 hidden items-center justify-center p-4 opacity-0 transition-opacity duration-300">
        <div class="bg-white dark:bg-gray-800 rounded-2xl max-w-sm w-full p-6 shadow-2xl border border-gray-100 dark:border-gray-700 flex flex-col gap-4 text-center transform scale-95 transition-transform duration-300">
            <div class="w-14 h-14 bg-red-100 dark:bg-red-900/30 text-red-600 dark:text-red-400 rounded-full flex items-center justify-center mx-auto text-2xl mb-1 shadow-inner">
                <i class="fa-solid fa-triangle-exclamation"></i>
            </div>
            <h3 id="confirmTitle" class="font-bold text-lg text-gray-800 dark:text-gray-100">Konfirmasi Hapus</h3>
            <p id="confirmMessage" class="text-sm text-gray-500 dark:text-gray-400 px-2">Apakah Anda yakin ingin menghapus data ini? Aksi ini tidak dapat dikembalikan.</p>

            <div class="flex justify-center gap-3 pt-4 border-t border-gray-100 dark:border-gray-700 mt-2">
                <button onclick="closeModal('confirmModal')" class="px-5 py-2.5 text-sm rounded-xl bg-gray-100 dark:bg-gray-700 text-gray-700 dark:text-gray-200 hover:bg-gray-200 dark:hover:bg-gray-600 transition font-medium">Batal</button>
                <button id="confirmExecuteBtn" class="px-5 py-2.5 text-sm rounded-xl bg-red-600 text-white hover:bg-red-700 font-bold transition shadow-sm shadow-red-500/30">Ya, Hapus Permanen</button>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="text-center py-5 text-[11px] font-medium tracking-wide text-gray-400 dark:text-gray-500 border-t border-gray-200 dark:border-gray-700">
        &copy; 2026 Sistem Pengelola Data & Tautan SMAN 2 Nusa &bull; Semua Hak Dilindungi
    </footer>

    <script>
        // State Management
        let appData = {};
        let activeClass = '';
        let searchQuery = '';

        // Default Seed Data
        const initialSchoolData = {
            "Kelas XA": [
                { id: "260004", nisn: "0106148762", name: "ABDUL WAHIP", gender: "LAKI-LAKI", link: "https://docs.google.com/forms/d/e/1FAIpQLSdnsta25s_bhWUMKMcf86QdHcAT1zAOFqKdB6GkKlLyaFErcw/formResponse?usp=pp_url&entry.1687779044=ABDUL+WAHIP", selected: false },
                { id: "260010", nisn: "0107923109", name: "ALFON AQUINO SAKA", gender: "LAKI-LAKI", link: "", selected: false },
                { id: "260012", nisn: "0105052057", name: "AMANDA PUTRI", gender: "PEREMPUAN", link: "", selected: false },
                { id: "260017", nisn: "0118971241", name: "ARAYYA NUR ZAHIRA", gender: "PEREMPUAN", link: "", selected: false }
            ],
            "Kelas XB": [
                { id: "260005", nisn: "0102094669", name: "ADAM ALIF RAHMAN", gender: "LAKI-LAKI", link: "", selected: false },
                { id: "260014", nisn: "0109930277", name: "ANDI NURHALIZAH", gender: "PEREMPUAN", link: "", selected: false },
                { id: "260021", nisn: "0117889037", name: "DINDA KIRANA", gender: "PEREMPUAN", link: "", selected: false }
            ]
        };

        // Initialize App
        document.addEventListener('DOMContentLoaded', () => {
            initDarkMode();
            loadData();
            updateUI();
        });

        function loadData() {
            try {
                const stored = localStorage.getItem('presensiAppData');
                if (stored) {
                    appData = JSON.parse(stored);
                } else {
                    appData = JSON.parse(JSON.stringify(initialSchoolData)); // Deep copy
                }
                const classes = Object.keys(appData);
                if (classes.length > 0) {
                    activeClass = classes[0];
                }
            } catch (e) {
                console.error("Error loading data", e);
                appData = JSON.parse(JSON.stringify(initialSchoolData));
            }
        }

        function saveData() {
            localStorage.setItem('presensiAppData', JSON.stringify(appData));
            updateStats();
        }

        function resetToDefaultData() {
            showConfirm("Reset Data Awal", "Apakah Anda yakin ingin menghapus semua perubahan dan mengembalikan ke data awal bawaan aplikasi?", () => {
                appData = JSON.parse(JSON.stringify(initialSchoolData));
                activeClass = Object.keys(appData)[0] || '';
                saveData();
                updateUI();
                showAlert("Data berhasil direset ke pengaturan awal.");
            });
        }

        function updateUI() {
            renderClassTabs();
            renderStudentList();
            generateLinks();
            updateStats();
        }

        function renderClassTabs() {
            const container = document.getElementById('classTabs');
            container.innerHTML = '';
            const classes = Object.keys(appData);
            
            if (classes.length === 0) {
                container.innerHTML = `<span class="text-xs text-gray-500 italic">Tidak ada kelas. Silakan tambah kelas.</span>`;
                return;
            }

            classes.forEach(cls => {
                const isActive = cls === activeClass;
                const btn = document.createElement('button');
                btn.className = `px-3.5 py-1.5 text-xs font-semibold rounded-lg transition-all duration-200 shadow-sm ${isActive ? 'bg-indigo-600 text-white shadow-indigo-500/30' : 'bg-white dark:bg-gray-800 text-gray-600 dark:text-gray-300 border border-gray-200 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-700'}`;
                btn.innerHTML = `
                    ${cls}
                    ${isActive ? `<span onclick="deleteClass(event, '${cls}')" class="ml-2 text-indigo-200 hover:text-white transition cursor-pointer px-1">&times;</span>` : ''}
                `;
                btn.onclick = () => {
                    activeClass = cls;
                    document.getElementById('searchInput').value = '';
                    searchQuery = '';
                    updateUI();
                };
                container.appendChild(btn);
            });
        }

        function renderStudentList() {
            const container = document.getElementById('studentListContainer');
            const titleEl = document.getElementById('activeClassTitle');
            const countEl = document.getElementById('classSelectedCount');
            
            searchQuery = document.getElementById('searchInput').value.toLowerCase();
            
            if (!activeClass || !appData[activeClass]) {
                container.innerHTML = `<div class="text-center text-gray-400 text-xs py-8">Pilih atau buat kelas terlebih dahulu.</div>`;
                titleEl.textContent = "Belum Ada Kelas";
                countEl.textContent = "";
                return;
            }

            titleEl.textContent = activeClass;
            container.innerHTML = '';

            let students = appData[activeClass];
            
            if (searchQuery) {
                students = students.filter(s => 
                    s.name.toLowerCase().includes(searchQuery) || 
                    s.id.toLowerCase().includes(searchQuery) || 
                    (s.nisn && s.nisn.toLowerCase().includes(searchQuery))
                );
            }

            if (students.length === 0) {
                container.innerHTML = `<div class="text-center text-gray-400 text-xs py-8">Tidak ada siswa ditemukan.</div>`;
            }

            let selectedInClass = 0;

            students.forEach((s, index) => {
                if (s.selected) selectedInClass++;
                
                const item = document.createElement('div');
                item.className = `flex flex-col sm:flex-row justify-between sm:items-center p-3 rounded-xl border transition-all duration-200 ${s.selected ? 'bg-indigo-50 dark:bg-indigo-900/30 border-indigo-200 dark:border-indigo-700 shadow-sm' : 'bg-white dark:bg-gray-800 border-gray-100 dark:border-gray-700 hover:border-gray-300 dark:hover:border-gray-600'}`;
                
                item.innerHTML = `
                    <div class="flex items-center gap-3 overflow-hidden cursor-pointer w-full sm:w-auto" onclick="toggleStudentSelection('${s.id}')">
                        <div class="relative flex items-center">
                            <input type="checkbox" ${s.selected ? 'checked' : ''} class="w-4 h-4 text-indigo-600 bg-gray-100 border-gray-300 rounded focus:ring-indigo-500 dark:focus:ring-indigo-600 dark:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600 pointer-events-none">
                        </div>
                        <div class="flex flex-col min-w-0">
                            <span class="font-semibold text-xs text-gray-800 dark:text-gray-200 truncate ${s.selected ? 'text-indigo-700 dark:text-indigo-300' : ''}">${s.name}</span>
                            <span class="text-[10px] text-gray-500 flex items-center gap-1.5 mt-0.5">
                                <span class="bg-gray-100 dark:bg-gray-700 px-1.5 py-0.5 rounded text-gray-600 dark:text-gray-400">${s.id}</span>
                                ${s.gender === 'LAKI-LAKI' ? '<i class="fa-solid fa-mars text-blue-400" title="Laki-laki"></i>' : '<i class="fa-solid fa-venus text-pink-400" title="Perempuan"></i>'}
                                ${s.link ? '<i class="fa-solid fa-link text-indigo-400 ml-1" title="Tautan kustom aktif"></i>' : ''}
                            </span>
                        </div>
                    </div>
                    <div class="flex items-center gap-2 mt-2 sm:mt-0 justify-end w-full sm:w-auto pl-7 sm:pl-0 border-t sm:border-t-0 border-gray-100 dark:border-gray-700 pt-2 sm:pt-0">
                        <button onclick="editStudent('${s.id}')" class="p-1.5 text-gray-400 hover:text-indigo-500 transition" title="Edit Siswa"><i class="fa-solid fa-pen text-xs"></i></button>
                        <button onclick="deleteStudent('${s.id}')" class="p-1.5 text-gray-400 hover:text-red-500 transition" title="Hapus Siswa"><i class="fa-solid fa-trash text-xs"></i></button>
                    </div>
                `;
                container.appendChild(item);
            });

            countEl.textContent = `${selectedInClass} terpilih dari ${appData[activeClass].length}`;
            
            // Generate Links automatically when rendering updates selections
            generateLinks();
        }

        function toggleStudentSelection(studentId) {
            if(!appData[activeClass]) return;
            const student = appData[activeClass].find(s => s.id === studentId);
            if (student) {
                student.selected = !student.selected;
                saveData();
                renderStudentList();
            }
        }

        function selectAll(check) {
            if(!appData[activeClass]) return;
            
            // Only select/deselect visible students if searching
            let targetStudents = appData[activeClass];
            if (searchQuery) {
                targetStudents = targetStudents.filter(s => 
                    s.name.toLowerCase().includes(searchQuery) || 
                    s.id.toLowerCase().includes(searchQuery)
                );
            }

            targetStudents.forEach(s => s.selected = check);
            saveData();
            renderStudentList();
        }

        function getStudentLink(student) {
            // Use custom link if exists, otherwise try to generate from global config
            if (student.link && student.link.trim() !== '') {
                return student.link;
            }
            
            const globalLink = document.getElementById('globalLinkInput').value.trim();
            if (globalLink) {
                let generatedLink = globalLink
                    .replace(/{nama}/g, encodeURIComponent(student.name))
                    .replace(/{nis}/g, encodeURIComponent(student.id));
                return generatedLink;
            }
            
            return `[Tautan Belum Diatur] - ${student.name}`;
        }

        function applyGlobalLink() {
            const input = document.getElementById('globalLinkInput').value;
            if (!input) {
                showAlert("Masukkan format tautan terlebih dahulu!");
                return;
            }
            if(!appData[activeClass]) return;
            
            // Overwrite all custom links in active class with empty to force using global link logic
            // or we could embed the generated link directly. Let's embed directly for portability.
            appData[activeClass].forEach(s => {
                s.link = input
                    .replace(/{nama}/g, encodeURIComponent(s.name))
                    .replace(/{nis}/g, encodeURIComponent(s.id));
            });
            
            saveData();
            renderStudentList();
            showAlert(`Tautan global berhasil diterapkan ke seluruh siswa di ${activeClass}.`);
        }

        function generateLinks() {
            const area = document.getElementById('outputLinkArea');
            const badge = document.getElementById('totalSelectedBadge');
            
            let links = [];
            
            // Gather selected students across ALL classes (or just active? Usually all classes for bulk generation)
            for (const cls in appData) {
                appData[cls].forEach(s => {
                    if (s.selected) {
                        links.push(getStudentLink(s));
                    }
                });
            }

            if (links.length > 0) {
                area.value = links.join('\n');
            } else {
                area.value = '';
            }
            
            badge.textContent = `${links.length} Tautan`;
        }

        function processAndOpen() {
            const area = document.getElementById('outputLinkArea');
            const links = area.value.split('\n').filter(l => l.trim() !== '' && l.startsWith('http'));
            
            if (links.length === 0) {
                showAlert("Tidak ada tautan valid yang dipilih untuk dibuka.");
                return;
            }
            if (links.length > 20) {
                showConfirm("Buka Banyak Tab", `Anda akan membuka ${links.length} tab sekaligus. Ini bisa membuat peramban berat/terblokir pop-up blocker. Lanjutkan?`, () => {
                    links.forEach(l => window.open(l.trim(), '_blank'));
                });
                return;
            }
            
            links.forEach(l => window.open(l.trim(), '_blank'));
        }

        function copyAllOutputLinks() {
            const area = document.getElementById('outputLinkArea');
            if (!area.value.trim()) {
                showAlert("Tidak ada tautan untuk disalin.");
                return;
            }
            area.select();
            document.execCommand('copy');
            showAlert("Semua tautan berhasil disalin ke clipboard!");
        }

        function updateStats() {
            let totalStu = 0;
            let totalCls = Object.keys(appData).length;
            
            for(const cls in appData){
                totalStu += appData[cls].length;
            }
            
            document.getElementById('statTotalStudents').textContent = totalStu;
            document.getElementById('statTotalClasses').textContent = totalCls;
        }

        // Helper Modals
        function openModal(id) {
            const m = document.getElementById(id);
            m.classList.remove('hidden');
            m.classList.add('flex');
            // Small timeout to allow display:flex to apply before opacity transition
            setTimeout(() => {
                m.classList.remove('opacity-0');
                m.querySelector('div').classList.remove('scale-95');
            }, 10);
        }

        function closeModal(id) {
            const m = document.getElementById(id);
            m.classList.add('opacity-0');
            m.querySelector('div').classList.add('scale-95');
            setTimeout(() => {
                m.classList.add('hidden');
                m.classList.remove('flex');
            }, 300); // match duration-300
        }

        function populateClassDropdown(selectId) {
            const select = document.getElementById(selectId);
            select.innerHTML = '';
            Object.keys(appData).forEach(cls => {
                const opt = document.createElement('option');
                opt.value = cls;
                opt.textContent = cls;
                if(cls === activeClass) opt.selected = true;
                select.appendChild(opt);
            });
        }

        // Class Actions
        function openAddClassModal() {
            document.getElementById('newClassNameInput').value = '';
            openModal('classModal');
            setTimeout(() => document.getElementById('newClassNameInput').focus(), 100);
        }

        function handleSaveClass(e) {
            e.preventDefault();
            const name = document.getElementById('newClassNameInput').value.trim();
            if(!name) return;
            
            if(appData[name]) {
                showAlert("Kelas dengan nama tersebut sudah ada!");
                return;
            }
            
            appData[name] = [];
            activeClass = name;
            saveData();
            updateUI();
            closeModal('classModal');
            showAlert(`Kelas ${name} berhasil ditambahkan.`);
        }

        function deleteClass(e, className) {
            e.stopPropagation();
            showConfirm("Hapus Kelas", `Anda yakin ingin menghapus kelas <b>${className}</b> beserta seluruh siswa di dalamnya?`, () => {
                delete appData[className];
                const remaining = Object.keys(appData);
                if (remaining.length > 0) activeClass = remaining[0];
                else activeClass = '';
                
                saveData();
                updateUI();
            });
        }

        // Student Actions
        function openAddStudentModal() {
            if(Object.keys(appData).length === 0){
                showAlert("Buat kelas terlebih dahulu sebelum menambah siswa.");
                return;
            }
            document.getElementById('studentModalTitle').textContent = "Tambah Siswa Baru";
            document.getElementById('studentForm').reset();
            document.getElementById('editOriginalClass').value = '';
            document.getElementById('editOriginalId').value = '';
            populateClassDropdown('modalStudentClass');
            openModal('studentModal');
        }

        function editStudent(studentId) {
            if(!appData[activeClass]) return;
            const student = appData[activeClass].find(s => s.id === studentId);
            if(!student) return;

            document.getElementById('studentModalTitle').textContent = "Edit Data Siswa";
            populateClassDropdown('modalStudentClass');
            
            document.getElementById('modalStudentClass').value = activeClass;
            document.getElementById('modalStudentId').value = student.id;
            document.getElementById('modalStudentNisn').value = student.nisn || '';
            document.getElementById('modalStudentName').value = student.name;
            document.getElementById('modalStudentGender').value = student.gender;
            document.getElementById('modalStudentLink').value = student.link || '';
            
            document.getElementById('editOriginalClass').value = activeClass;
            document.getElementById('editOriginalId').value = student.id;
            
            openModal('studentModal');
        }

        function handleSaveStudent(e) {
            e.preventDefault();
            const targetCls = document.getElementById('modalStudentClass').value;
            const sId = document.getElementById('modalStudentId').value.trim();
            const sNisn = document.getElementById('modalStudentNisn').value.trim();
            const sName = document.getElementById('modalStudentName').value.trim().toUpperCase();
            const sGender = document.getElementById('modalStudentGender').value;
            const sLink = document.getElementById('modalStudentLink').value.trim();
            
            const origCls = document.getElementById('editOriginalClass').value;
            const origId = document.getElementById('editOriginalId').value;

            // Validation ID exist
            if(origId !== sId || origCls !== targetCls) {
               if(appData[targetCls] && appData[targetCls].some(s => s.id === sId)){
                   showAlert(`Siswa dengan NIS ${sId} sudah ada di kelas ${targetCls}!`);
                   return;
               }
            }

            const newStudentObj = {
                id: sId, nisn: sNisn, name: sName, gender: sGender, link: sLink, selected: false
            };

            if (origId && origCls) {
                // Editing existing
                const idx = appData[origCls].findIndex(s => s.id === origId);
                if(idx > -1) {
                    newStudentObj.selected = appData[origCls][idx].selected; // preserve selection
                    if (origCls === targetCls) {
                        appData[origCls][idx] = newStudentObj;
                    } else {
                        appData[origCls].splice(idx, 1);
                        if(!appData[targetCls]) appData[targetCls] = [];
                        appData[targetCls].push(newStudentObj);
                    }
                }
            } else {
                // Adding new
                if(!appData[targetCls]) appData[targetCls] = [];
                appData[targetCls].push(newStudentObj);
            }

            // Sort by name
            appData[targetCls].sort((a,b) => a.name.localeCompare(b.name));
            
            activeClass = targetCls;
            saveData();
            updateUI();
            closeModal('studentModal');
        }

        function deleteStudent(studentId) {
            showConfirm("Hapus Siswa", `Yakin ingin menghapus siswa dengan ID ${studentId}?`, () => {
                if(appData[activeClass]){
                    appData[activeClass] = appData[activeClass].filter(s => s.id !== studentId);
                    saveData();
                    renderStudentList();
                }
            });
        }

        function openBulkStudentModal() {
            if(Object.keys(appData).length === 0){
                showAlert("Buat kelas terlebih dahulu sebelum menambah siswa massal.");
                return;
            }
            populateClassDropdown('bulkStudentClass');
            document.getElementById('bulkStudentData').value = '';
            openModal('bulkStudentModal');
        }

        function fillBulkExample() {
            document.getElementById('bulkStudentData').value = 
`260201\t0109988771\tJOHN DOE\tLAKI-LAKI
260202\t0109988772\tJANE ROE\tPEREMPUAN
260203\t0109988773\tBUDI SANTOSO\tLAKI-LAKI`;
        }

        function handleBulkSaveStudents() {
            const targetCls = document.getElementById('bulkStudentClass').value;
            const rawData = document.getElementById('bulkStudentData').value.trim();
            if(!rawData) return;
            
            const lines = rawData.split('\n');
            let addedCount = 0;
            
            if(!appData[targetCls]) appData[targetCls] = [];

            lines.forEach(line => {
                // Split by tab, semicolon, or comma
                let parts = line.split(/\t|;|,/).map(p => p.trim()).filter(p => p !== '');
                if (parts.length >= 3) {
                    const id = parts[0];
                    const nisn = parts[1];
                    const name = parts[2].toUpperCase();
                    let gender = parts[3] ? parts[3].toUpperCase() : 'LAKI-LAKI';
                    if (!gender.includes('PEREMPUAN') && !gender.includes('P')) { gender = 'LAKI-LAKI'; } 
                    else { gender = 'PEREMPUAN'; }

                    // Check duplicate ID
                    if(!appData[targetCls].some(s => s.id === id)){
                        appData[targetCls].push({
                            id: id, nisn: nisn, name: name, gender: gender, link: "", selected: false
                        });
                        addedCount++;
                    }
                }
            });

            appData[targetCls].sort((a,b) => a.name.localeCompare(b.name));
            activeClass = targetCls;
            saveData();
            updateUI();
            closeModal('bulkStudentModal');
            showAlert(`${addedCount} siswa baru berhasil ditambahkan ke ${targetCls}.`);
        }

        // Dark Mode
        function initDarkMode() {
            if (localStorage.theme === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
                document.documentElement.classList.add('dark');
            } else {
                document.documentElement.classList.remove('dark');
            }
        }
        function toggleDarkMode() {
            document.documentElement.classList.toggle('dark');
            localStorage.theme = document.documentElement.classList.contains('dark') ? 'dark' : 'light';
        }

        // Export/Import JSON
        function exportDataJSON() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(appData, null, 2));
            const dlAnchorElem = document.createElement('a');
            dlAnchorElem.setAttribute("href", dataStr);
            dlAnchorElem.setAttribute("download", `Backup_Presensi_SMAN2Nusa_${new Date().toISOString().slice(0,10)}.json`);
            dlAnchorElem.click();
        }

        function importDataJSON(event) {
            const file = event.target.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const parsed = JSON.parse(e.target.result);
                    if(typeof parsed === 'object') {
                        appData = parsed;
                        activeClass = Object.keys(appData)[0] || '';
                        saveData();
                        updateUI();
                        showAlert("Data berhasil diimpor.");
                    }
                } catch (err) {
                    showAlert("Format JSON tidak valid.");
                }
            };
            reader.readAsText(file);
            event.target.value = ''; // reset
        }

        // Notifications
        let alertTimeout;
        function showAlert(msg) {
            const box = document.getElementById('alertBox');
            document.getElementById('alertText').textContent = msg;
            box.classList.remove('hidden');
            box.classList.add('flex');
            
            clearTimeout(alertTimeout);
            alertTimeout = setTimeout(() => hideAlert(), 5000);
        }
        function hideAlert() {
            const box = document.getElementById('alertBox');
            box.classList.add('hidden');
            box.classList.remove('flex');
        }

        // Confirm Dialog
        let confirmActionCallback = null;
        function showConfirm(title, message, callback) {
            document.getElementById('confirmTitle').innerHTML = title;
            document.getElementById('confirmMessage').innerHTML = message;
            confirmActionCallback = callback;
            openModal('confirmModal');
        }
        document.getElementById('confirmExecuteBtn').onclick = () => {
            if (confirmActionCallback) confirmActionCallback();
            closeModal('confirmModal');
        };

    </script>
</body>
</html>
