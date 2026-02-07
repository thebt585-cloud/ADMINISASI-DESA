<html lang="id" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sistem Administrasi Desa/Kelurahan</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <script src="/_sdk/data_sdk.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&amp;display=swap" rel="stylesheet">
  <style>
    body {
      box-sizing: border-box;
      font-family: 'Plus Jakarta Sans', sans-serif;
    }
    
    .sidebar-item {
      transition: all 0.2s ease;
    }
    
    .sidebar-item:hover {
      transform: translateX(4px);
    }
    
    .card-hover {
      transition: all 0.3s ease;
    }
    
    .card-hover:hover {
      transform: translateY(-2px);
      box-shadow: 0 10px 40px rgba(0,0,0,0.1);
    }
    
    .status-badge {
      animation: fadeIn 0.3s ease;
    }
    
    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.9); }
      to { opacity: 1; transform: scale(1); }
    }
    
    @keyframes slideIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    
    .slide-in {
      animation: slideIn 0.4s ease forwards;
    }
    
    .gradient-bg {
      background: linear-gradient(135deg, #0ea5e9 0%, #0284c7 50%, #0369a1 100%);
    }
    
    .glass-effect {
      backdrop-filter: blur(10px);
      background: rgba(255,255,255,0.95);
    }
    
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    
    ::-webkit-scrollbar-track {
      background: #f1f5f9;
    }
    
    ::-webkit-scrollbar-thumb {
      background: #cbd5e1;
      border-radius: 3px;
    }
    
    ::-webkit-scrollbar-thumb:hover {
      background: #94a3b8;
    }
    
    .print-area {
      background: white;
      padding: 40px;
      max-width: 210mm;
      margin: 0 auto;
    }
    
    @media print {
      body * {
        visibility: hidden;
      }
      .print-area, .print-area * {
        visibility: visible;
      }
      .print-area {
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
      }
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
 </head>
 <body class="h-full bg-gradient-to-br from-slate-50 via-sky-50 to-cyan-50">
  <div id="app" class="h-full w-full overflow-auto"><!-- Login Screen -->
   <div id="loginScreen" class="h-full flex items-center justify-center p-4">
    <div class="w-full max-w-md">
     <div class="text-center mb-8 slide-in">
      <div class="w-24 h-24 mx-auto mb-4 gradient-bg rounded-2xl flex items-center justify-center shadow-lg shadow-sky-200">
       <svg class="w-14 h-14 text-white" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
       </svg>
      </div>
      <h1 id="loginTitle" class="text-2xl font-bold text-slate-800">Sistem Administrasi Desa</h1>
      <p id="loginSubtitle" class="text-slate-500 mt-1">Desa Sukamaju, Kec. Cilandak</p>
     </div>
     <div class="bg-white rounded-2xl shadow-xl shadow-slate-200/50 p-8 slide-in" style="animation-delay: 0.1s">
      <div class="flex gap-2 mb-6 bg-slate-100 p-1 rounded-xl"><button onclick="setLoginMode('admin')" id="btnLoginAdmin" class="flex-1 py-2.5 rounded-lg text-sm font-semibold transition-all bg-white text-sky-600 shadow"> 🔐 Admin Desa </button> <button onclick="setLoginMode('warga')" id="btnLoginWarga" class="flex-1 py-2.5 rounded-lg text-sm font-semibold transition-all text-slate-500"> 👤 Warga </button>
      </div><!-- Admin Login Form -->
      <div id="adminLoginForm">
       <div class="space-y-4">
        <div><label class="block text-sm font-medium text-slate-700 mb-1.5">Username</label> <input type="text" id="adminUsername" placeholder="Masukkan username" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none transition-all">
        </div>
        <div><label class="block text-sm font-medium text-slate-700 mb-1.5">PIN</label> <input type="password" id="adminPin" placeholder="Masukkan PIN" maxlength="6" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none transition-all">
        </div><button onclick="loginAdmin()" class="w-full py-3.5 gradient-bg text-white rounded-xl font-semibold hover:opacity-90 transition-all shadow-lg shadow-sky-200"> Masuk sebagai Admin </button>
       </div>
       <p class="text-center text-xs text-slate-400 mt-4">Demo: admin / 123456</p>
      </div><!-- Warga Form -->
      <div id="wargaLoginForm" class="hidden">
       <div class="space-y-4">
        <div><label class="block text-sm font-medium text-slate-700 mb-1.5">NIK (16 digit)</label> <input type="text" id="wargaNik" placeholder="Masukkan NIK Anda" maxlength="16" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none transition-all">
        </div><button onclick="loginWarga()" class="w-full py-3.5 gradient-bg text-white rounded-xl font-semibold hover:opacity-90 transition-all shadow-lg shadow-sky-200"> Ajukan Surat </button> <button onclick="cekTracking()" class="w-full py-3 border-2 border-sky-500 text-sky-600 rounded-xl font-semibold hover:bg-sky-50 transition-all"> 📋 Cek Status Pengajuan </button>
       </div>
      </div>
     </div>
     <p class="text-center text-xs text-slate-400 mt-6">© 2024 Sistem Administrasi Desa Digital</p>
    </div>
   </div><!-- Admin Dashboard -->
   <div id="adminDashboard" class="hidden h-full flex"><!-- Sidebar -->
    <aside class="w-64 gradient-bg text-white flex-shrink-0 flex flex-col">
     <div class="p-5 border-b border-white/10">
      <div class="flex items-center gap-3">
       <div class="w-10 h-10 bg-white/20 rounded-xl flex items-center justify-center">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
        </svg>
       </div>
       <div>
        <h2 id="sidebarTitle" class="font-bold text-sm">Admin Desa</h2>
        <p class="text-xs text-white/70">Panel Kontrol</p>
       </div>
      </div>
     </div>
     <nav class="flex-1 p-4 space-y-1 overflow-y-auto"><button onclick="showSection('dashboard')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 rounded-xl bg-white/20 text-white font-medium" data-section="dashboard"> <span class="text-lg">📊</span> Dashboard </button> <button onclick="showSection('penduduk')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 rounded-xl hover:bg-white/10 text-white/80 font-medium" data-section="penduduk"> <span class="text-lg">👥</span> Data Penduduk </button> <button onclick="showSection('pengajuan')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 rounded-xl hover:bg-white/10 text-white/80 font-medium" data-section="pengajuan"> <span class="text-lg">📄</span> Pengajuan Surat </button> <button onclick="showSection('arsip')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 rounded-xl hover:bg-white/10 text-white/80 font-medium" data-section="arsip"> <span class="text-lg">📁</span> Arsip Surat </button> <button onclick="showSection('pengaturan')" class="sidebar-item w-full flex items-center gap-3 px-4 py-3 rounded-xl hover:bg-white/10 text-white/80 font-medium" data-section="pengaturan"> <span class="text-lg">⚙️</span> Pengaturan </button>
     </nav>
     <div class="p-4 border-t border-white/10"><button onclick="logout()" class="w-full flex items-center justify-center gap-2 px-4 py-3 rounded-xl bg-white/10 hover:bg-white/20 text-white font-medium transition-all">
       <svg class="w-5 h-5" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
       </svg> Keluar </button>
     </div>
    </aside><!-- Main Content -->
    <main class="flex-1 overflow-y-auto"><!-- Header -->
     <header class="bg-white/80 glass-effect sticky top-0 z-10 px-6 py-4 border-b border-slate-200">
      <div class="flex items-center justify-between">
       <div>
        <h1 id="pageTitle" class="text-xl font-bold text-slate-800">Dashboard</h1>
        <p id="pageSubtitle" class="text-sm text-slate-500">Selamat datang di panel administrasi</p>
       </div>
       <div class="flex items-center gap-4"><button id="notifBtn" onclick="toggleNotif()" class="relative p-2 rounded-xl bg-slate-100 hover:bg-slate-200 transition-all">
         <svg class="w-6 h-6 text-slate-600" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
         </svg><span id="notifBadge" class="hidden absolute -top-1 -right-1 w-5 h-5 bg-red-500 text-white text-xs rounded-full flex items-center justify-center font-bold">0</span> </button>
        <div class="flex items-center gap-3 pl-4 border-l border-slate-200">
         <div class="w-10 h-10 gradient-bg rounded-xl flex items-center justify-center text-white font-bold">
          A
         </div>
         <div>
          <p class="font-semibold text-slate-800 text-sm">Administrator</p>
          <p class="text-xs text-slate-500">Super Admin</p>
         </div>
        </div>
       </div>
      </div>
     </header>
     <div class="p-6"><!-- Dashboard Section -->
      <section id="sectionDashboard" class="space-y-6"><!-- Stats Cards -->
       <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
        <div class="card-hover bg-white rounded-2xl p-5 shadow-sm border border-slate-100">
         <div class="flex items-center justify-between">
          <div>
           <p class="text-sm text-slate-500">Total Pengajuan</p>
           <p id="statTotal" class="text-3xl font-bold text-slate-800 mt-1">0</p>
          </div>
          <div class="w-14 h-14 bg-sky-100 rounded-2xl flex items-center justify-center"><span class="text-2xl">📋</span>
          </div>
         </div>
         <p class="text-xs text-slate-400 mt-3">Semua pengajuan surat</p>
        </div>
        <div class="card-hover bg-white rounded-2xl p-5 shadow-sm border border-slate-100">
         <div class="flex items-center justify-between">
          <div>
           <p class="text-sm text-slate-500">Menunggu</p>
           <p id="statPending" class="text-3xl font-bold text-amber-500 mt-1">0</p>
          </div>
          <div class="w-14 h-14 bg-amber-100 rounded-2xl flex items-center justify-center"><span class="text-2xl">⏳</span>
          </div>
         </div>
         <p class="text-xs text-slate-400 mt-3">Perlu diproses</p>
        </div>
        <div class="card-hover bg-white rounded-2xl p-5 shadow-sm border border-slate-100">
         <div class="flex items-center justify-between">
          <div>
           <p class="text-sm text-slate-500">Diproses</p>
           <p id="statProcess" class="text-3xl font-bold text-sky-500 mt-1">0</p>
          </div>
          <div class="w-14 h-14 bg-sky-100 rounded-2xl flex items-center justify-center"><span class="text-2xl">🔄</span>
          </div>
         </div>
         <p class="text-xs text-slate-400 mt-3">Sedang diproses</p>
        </div>
        <div class="card-hover bg-white rounded-2xl p-5 shadow-sm border border-slate-100">
         <div class="flex items-center justify-between">
          <div>
           <p class="text-sm text-slate-500">Selesai</p>
           <p id="statDone" class="text-3xl font-bold text-emerald-500 mt-1">0</p>
          </div>
          <div class="w-14 h-14 bg-emerald-100 rounded-2xl flex items-center justify-center"><span class="text-2xl">✅</span>
          </div>
         </div>
         <p class="text-xs text-slate-400 mt-3">Surat selesai</p>
        </div>
       </div><!-- Chart & Recent -->
       <div class="grid grid-cols-1 lg:grid-cols-2 gap-6"><!-- Chart -->
        <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-100">
         <h3 class="font-bold text-slate-800 mb-4">📊 Statistik Jenis Surat</h3>
         <div id="chartContainer" class="space-y-3"><!-- Chart bars will be rendered here -->
         </div>
        </div><!-- Recent -->
        <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-100">
         <h3 class="font-bold text-slate-800 mb-4">🕐 Pengajuan Terbaru</h3>
         <div id="recentList" class="space-y-3 max-h-72 overflow-y-auto">
          <p class="text-center text-slate-400 py-8">Belum ada pengajuan</p>
         </div>
        </div>
       </div><!-- Quick Actions -->
       <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-100">
        <h3 class="font-bold text-slate-800 mb-4">⚡ Aksi Cepat</h3>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-3"><button onclick="showSection('penduduk'); showAddPenduduk()" class="p-4 rounded-xl bg-sky-50 hover:bg-sky-100 transition-all text-center"> <span class="text-2xl">➕</span> <p class="text-sm font-medium text-slate-700 mt-2">Tambah Penduduk</p></button> <button onclick="showSection('pengajuan')" class="p-4 rounded-xl bg-amber-50 hover:bg-amber-100 transition-all text-center"> <span class="text-2xl">📄</span> <p class="text-sm font-medium text-slate-700 mt-2">Kelola Pengajuan</p></button> <button onclick="exportData('excel')" class="p-4 rounded-xl bg-emerald-50 hover:bg-emerald-100 transition-all text-center"> <span class="text-2xl">📊</span> <p class="text-sm font-medium text-slate-700 mt-2">Export Excel</p></button> <button onclick="showSection('pengaturan')" class="p-4 rounded-xl bg-purple-50 hover:bg-purple-100 transition-all text-center"> <span class="text-2xl">⚙️</span> <p class="text-sm font-medium text-slate-700 mt-2">Pengaturan</p></button>
        </div>
       </div>
      </section><!-- Penduduk Section -->
      <section id="sectionPenduduk" class="hidden space-y-6">
       <div class="flex flex-col sm:flex-row gap-4 justify-between">
        <div class="relative flex-1 max-w-md"><input type="text" id="searchPenduduk" placeholder="Cari NIK atau nama..." class="w-full pl-10 pr-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
         <svg class="w-5 h-5 text-slate-400 absolute left-3 top-1/2 -translate-y-1/2" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
         </svg>
        </div><button onclick="showAddPenduduk()" class="px-6 py-3 gradient-bg text-white rounded-xl font-semibold hover:opacity-90 transition-all shadow-lg shadow-sky-200 flex items-center gap-2">
         <svg class="w-5 h-5" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4" />
         </svg> Tambah Penduduk </button>
       </div>
       <div class="bg-white rounded-2xl shadow-sm border border-slate-100 overflow-hidden">
        <div class="overflow-x-auto">
         <table class="w-full">
          <thead class="bg-slate-50 border-b border-slate-100">
           <tr>
            <th class="px-6 py-4 text-left text-xs font-semibold text-slate-500 uppercase tracking-wider">NIK</th>
            <th class="px-6 py-4 text-left text-xs font-semibold text-slate-500 uppercase tracking-wider">Nama</th>
            <th class="px-6 py-4 text-left text-xs font-semibold text-slate-500 uppercase tracking-wider">L/P</th>
            <th class="px-6 py-4 text-left text-xs font-semibold text-slate-500 uppercase tracking-wider">Alamat</th>
            <th class="px-6 py-4 text-left text-xs font-semibold text-slate-500 uppercase tracking-wider">Pekerjaan</th>
            <th class="px-6 py-4 text-center text-xs font-semibold text-slate-500 uppercase tracking-wider">Aksi</th>
           </tr>
          </thead>
          <tbody id="pendudukTable" class="divide-y divide-slate-100">
           <tr>
            <td colspan="6" class="px-6 py-12 text-center text-slate-400"><span class="text-4xl">👥</span> <p class="mt-2">Belum ada data penduduk</p></td>
           </tr>
          </tbody>
         </table>
        </div>
       </div>
      </section><!-- Pengajuan Section -->
      <section id="sectionPengajuan" class="hidden space-y-6">
       <div class="flex flex-col sm:flex-row gap-4 justify-between">
        <div class="flex gap-2 flex-wrap"><button onclick="filterPengajuan('all')" class="filter-btn px-4 py-2 rounded-xl bg-slate-800 text-white font-medium text-sm" data-filter="all"> Semua </button> <button onclick="filterPengajuan('pending')" class="filter-btn px-4 py-2 rounded-xl bg-slate-100 text-slate-600 font-medium text-sm" data-filter="pending"> ⏳ Menunggu </button> <button onclick="filterPengajuan('process')" class="filter-btn px-4 py-2 rounded-xl bg-slate-100 text-slate-600 font-medium text-sm" data-filter="process"> 🔄 Diproses </button> <button onclick="filterPengajuan('done')" class="filter-btn px-4 py-2 rounded-xl bg-slate-100 text-slate-600 font-medium text-sm" data-filter="done"> ✅ Selesai </button> <button onclick="filterPengajuan('rejected')" class="filter-btn px-4 py-2 rounded-xl bg-slate-100 text-slate-600 font-medium text-sm" data-filter="rejected"> ❌ Ditolak </button>
        </div>
       </div>
       <div id="pengajuanList" class="grid gap-4">
        <div class="bg-white rounded-2xl p-8 text-center shadow-sm border border-slate-100"><span class="text-4xl">📄</span>
         <p class="mt-2 text-slate-400">Belum ada pengajuan surat</p>
        </div>
       </div>
      </section><!-- Arsip Section -->
      <section id="sectionArsip" class="hidden space-y-6">
       <div class="flex flex-col sm:flex-row gap-4 justify-between">
        <div class="relative flex-1 max-w-md"><input type="text" id="searchArsip" placeholder="Cari no surat atau nama..." class="w-full pl-10 pr-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
         <svg class="w-5 h-5 text-slate-400 absolute left-3 top-1/2 -translate-y-1/2" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
         </svg>
        </div>
        <div class="flex gap-2"><button onclick="exportData('excel')" class="px-4 py-3 bg-emerald-500 text-white rounded-xl font-semibold hover:bg-emerald-600 transition-all flex items-center gap-2"> 📊 Export Excel </button>
        </div>
       </div>
       <div class="bg-white rounded-2xl shadow-sm border border-slate-100 overflow-hidden">
        <div class="overflow-x-auto">
         <table class="w-full">
          <thead class="bg-slate-50 border-b border-slate-100">
           <tr>
            <th class="px-6 py-4 text-left text-xs font-semibold text-slate-500 uppercase tracking-wider">No. Surat</th>
            <th class="px-6 py-4 text-left text-xs font-semibold text-slate-500 uppercase tracking-wider">Jenis</th>
            <th class="px-6 py-4 text-left text-xs font-semibold text-slate-500 uppercase tracking-wider">Nama</th>
            <th class="px-6 py-4 text-left text-xs font-semibold text-slate-500 uppercase tracking-wider">Tanggal</th>
            <th class="px-6 py-4 text-center text-xs font-semibold text-slate-500 uppercase tracking-wider">Status</th>
            <th class="px-6 py-4 text-center text-xs font-semibold text-slate-500 uppercase tracking-wider">Aksi</th>
           </tr>
          </thead>
          <tbody id="arsipTable" class="divide-y divide-slate-100">
           <tr>
            <td colspan="6" class="px-6 py-12 text-center text-slate-400"><span class="text-4xl">📁</span> <p class="mt-2">Belum ada arsip surat</p></td>
           </tr>
          </tbody>
         </table>
        </div>
       </div>
      </section><!-- Pengaturan Section -->
      <section id="sectionPengaturan" class="hidden space-y-6">
       <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-100">
         <h3 class="font-bold text-slate-800 mb-4 flex items-center gap-2"><span class="text-xl">🏛️</span> Identitas Instansi</h3>
         <div class="space-y-4">
          <div><label class="block text-sm font-medium text-slate-700 mb-1.5">Nama Desa/Kelurahan</label> <input type="text" id="settingDesa" placeholder="Nama Desa/Kelurahan" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
          </div>
          <div><label class="block text-sm font-medium text-slate-700 mb-1.5">Kecamatan</label> <input type="text" id="settingKecamatan" placeholder="Nama Kecamatan" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
          </div>
          <div><label class="block text-sm font-medium text-slate-700 mb-1.5">Kabupaten/Kota</label> <input type="text" id="settingKabupaten" placeholder="Nama Kabupaten/Kota" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
          </div>
          <div><label class="block text-sm font-medium text-slate-700 mb-1.5">Provinsi</label> <input type="text" id="settingProvinsi" placeholder="Nama Provinsi" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
          </div>
          <div><label class="block text-sm font-medium text-slate-700 mb-1.5">Nama Kepala Desa/Lurah</label> <input type="text" id="settingKepalaDesa" placeholder="Nama Kepala Desa" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
          </div><button onclick="saveSettings()" class="w-full py-3 gradient-bg text-white rounded-xl font-semibold hover:opacity-90 transition-all"> 💾 Simpan Pengaturan </button>
         </div>
        </div>
        <div class="space-y-6">
         <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-100">
          <h3 class="font-bold text-slate-800 mb-4 flex items-center gap-2"><span class="text-xl">📄</span> Template Surat Tersedia</h3>
          <div class="space-y-2">
           <div class="flex items-center gap-3 p-3 bg-slate-50 rounded-xl"><span class="text-lg">📝</span> <span class="text-sm text-slate-700">Surat Keterangan Domisili</span>
           </div>
           <div class="flex items-center gap-3 p-3 bg-slate-50 rounded-xl"><span class="text-lg">🏪</span> <span class="text-sm text-slate-700">Surat Keterangan Usaha</span>
           </div>
           <div class="flex items-center gap-3 p-3 bg-slate-50 rounded-xl"><span class="text-lg">💰</span> <span class="text-sm text-slate-700">Surat Keterangan Tidak Mampu</span>
           </div>
           <div class="flex items-center gap-3 p-3 bg-slate-50 rounded-xl"><span class="text-lg">⚰️</span> <span class="text-sm text-slate-700">Surat Keterangan Kematian</span>
           </div>
           <div class="flex items-center gap-3 p-3 bg-slate-50 rounded-xl"><span class="text-lg">👶</span> <span class="text-sm text-slate-700">Surat Keterangan Kelahiran</span>
           </div>
           <div class="flex items-center gap-3 p-3 bg-slate-50 rounded-xl"><span class="text-lg">📨</span> <span class="text-sm text-slate-700">Surat Pengantar</span>
           </div>
           <div class="flex items-center gap-3 p-3 bg-slate-50 rounded-xl"><span class="text-lg">🚚</span> <span class="text-sm text-slate-700">Surat Keterangan Pindah</span>
           </div>
          </div>
         </div>
         <div class="bg-gradient-to-br from-sky-500 to-cyan-600 rounded-2xl p-6 text-white">
          <h3 class="font-bold mb-2">💡 Tips</h3>
          <p class="text-sm text-white/90">Pastikan data instansi sudah lengkap agar template surat otomatis terisi dengan benar. Data ini akan muncul di kop surat dan footer dokumen.</p>
         </div>
        </div>
       </div>
      </section>
     </div>
    </main>
   </div><!-- Warga Dashboard -->
   <div id="wargaDashboard" class="hidden h-full overflow-y-auto">
    <div class="max-w-4xl mx-auto p-4 sm:p-6">
     <div class="flex items-center justify-between mb-6">
      <div>
       <h1 class="text-xl font-bold text-slate-800">Pengajuan Surat</h1>
       <p id="wargaGreeting" class="text-sm text-slate-500">Selamat datang</p>
      </div><button onclick="logout()" class="px-4 py-2 bg-slate-100 hover:bg-slate-200 rounded-xl text-sm font-medium text-slate-600 transition-all"> ← Kembali </button>
     </div>
     <div class="bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
      <h2 class="font-bold text-slate-800 mb-4">📝 Form Pengajuan Surat Baru</h2>
      <div class="space-y-4">
       <div><label class="block text-sm font-medium text-slate-700 mb-1.5">Jenis Surat</label> <select id="wargaJenisSurat" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none"> <option value="">-- Pilih Jenis Surat --</option> <option value="domisili">📝 Surat Keterangan Domisili</option> <option value="usaha">🏪 Surat Keterangan Usaha</option> <option value="tidak_mampu">💰 Surat Keterangan Tidak Mampu</option> <option value="kematian">⚰️ Surat Keterangan Kematian</option> <option value="kelahiran">👶 Surat Keterangan Kelahiran</option> <option value="pengantar">📨 Surat Pengantar</option> <option value="pindah">🚚 Surat Keterangan Pindah</option> </select>
       </div>
       <div><label class="block text-sm font-medium text-slate-700 mb-1.5">Keperluan</label> <input type="text" id="wargaKeperluan" placeholder="Contoh: Pembuatan KTP, Melamar Kerja, dll" class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
       </div>
       <div><label class="block text-sm font-medium text-slate-700 mb-1.5">Keterangan Tambahan</label> <textarea id="wargaKeterangan" rows="3" placeholder="Informasi tambahan jika diperlukan..." class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none resize-none"></textarea>
       </div><button onclick="submitPengajuan()" id="btnSubmitPengajuan" class="w-full py-3.5 gradient-bg text-white rounded-xl font-semibold hover:opacity-90 transition-all shadow-lg shadow-sky-200"> 📤 Kirim Pengajuan </button>
      </div>
     </div><!-- Riwayat Pengajuan Warga -->
     <div class="mt-6 bg-white rounded-2xl shadow-sm border border-slate-100 p-6">
      <h2 class="font-bold text-slate-800 mb-4">📋 Riwayat Pengajuan Anda</h2>
      <div id="wargaRiwayat" class="space-y-3">
       <p class="text-center text-slate-400 py-4">Belum ada riwayat pengajuan</p>
      </div>
     </div>
    </div>
   </div><!-- Modal Container -->
   <div id="modalContainer" class="hidden fixed inset-0 z-50 flex items-center justify-center p-4">
    <div class="absolute inset-0 bg-slate-900/50 backdrop-blur-sm" onclick="closeModal()"></div>
    <div id="modalContent" class="relative bg-white rounded-2xl shadow-2xl w-full max-w-2xl max-h-[90%] overflow-y-auto"><!-- Modal content will be injected here -->
    </div>
   </div><!-- Toast Notification -->
   <div id="toast" class="hidden fixed bottom-4 right-4 z-50 px-6 py-4 rounded-xl shadow-lg text-white font-medium slide-in"><span id="toastMessage"></span>
   </div><!-- Print Area (Hidden) -->
   <div id="printArea" class="hidden"><!-- Print content will be injected here -->
   </div>
  </div>
  <script>
    // ============================================
    // CONFIGURATION & STATE
    // ============================================
    
    const defaultConfig = {
      nama_desa: 'Kelurahan Medang',
      nama_kecamatan: 'Pagedangan',
      nama_kabupaten: 'Tangerang',
      nama_provinsi: 'Banten',
      nama_kepala_desa: 'M. Gilang Pratama Putra, S.Sos',
      primary_color: '#0ea5e9',
      secondary_color: '#0284c7',
      text_color: '#1e293b',
      bg_color: '#f8fafc',
      accent_color: '#06b6d4'
    };
    
    let config = { ...defaultConfig };
    let currentUser = null;
    let currentLoginMode = 'admin';
    let allData = [];
    let currentFilter = 'all';
    
    // Data types
    const DATA_TYPES = {
      PENDUDUK: 'penduduk',
      SURAT: 'surat'
    };
    
    const JENIS_SURAT = {
      domisili: 'Surat Keterangan Domisili',
      usaha: 'Surat Keterangan Usaha',
      tidak_mampu: 'Surat Keterangan Tidak Mampu',
      kematian: 'Surat Keterangan Kematian',
      kelahiran: 'Surat Keterangan Kelahiran',
      pengantar: 'Surat Pengantar',
      pindah: 'Surat Keterangan Pindah'
    };
    
    const STATUS_LABELS = {
      pending: { text: 'Menunggu', color: 'bg-amber-100 text-amber-700', icon: '⏳' },
      process: { text: 'Diproses', color: 'bg-sky-100 text-sky-700', icon: '🔄' },
      done: { text: 'Selesai', color: 'bg-emerald-100 text-emerald-700', icon: '✅' },
      rejected: { text: 'Ditolak', color: 'bg-red-100 text-red-700', icon: '❌' }
    };
    
    // ============================================
    // SDK INITIALIZATION
    // ============================================
    
    const dataHandler = {
      onDataChanged(data) {
        allData = data || [];
        updateUI();
      }
    };
    
    async function initApp() {
      // Initialize Element SDK
      if (window.elementSdk) {
        window.elementSdk.init({
          defaultConfig,
          onConfigChange: async (newConfig) => {
            config = { ...defaultConfig, ...newConfig };
            applyConfig();
          },
          mapToCapabilities: (cfg) => ({
            recolorables: [
              {
                get: () => cfg.primary_color || defaultConfig.primary_color,
                set: (v) => { cfg.primary_color = v; window.elementSdk.setConfig({ primary_color: v }); }
              },
              {
                get: () => cfg.secondary_color || defaultConfig.secondary_color,
                set: (v) => { cfg.secondary_color = v; window.elementSdk.setConfig({ secondary_color: v }); }
              },
              {
                get: () => cfg.text_color || defaultConfig.text_color,
                set: (v) => { cfg.text_color = v; window.elementSdk.setConfig({ text_color: v }); }
              },
              {
                get: () => cfg.bg_color || defaultConfig.bg_color,
                set: (v) => { cfg.bg_color = v; window.elementSdk.setConfig({ bg_color: v }); }
              },
              {
                get: () => cfg.accent_color || defaultConfig.accent_color,
                set: (v) => { cfg.accent_color = v; window.elementSdk.setConfig({ accent_color: v }); }
              }
            ],
            borderables: [],
            fontEditable: undefined,
            fontSizeable: undefined
          }),
          mapToEditPanelValues: (cfg) => new Map([
            ['nama_desa', cfg.nama_desa || defaultConfig.nama_desa],
            ['nama_kecamatan', cfg.nama_kecamatan || defaultConfig.nama_kecamatan],
            ['nama_kabupaten', cfg.nama_kabupaten || defaultConfig.nama_kabupaten],
            ['nama_provinsi', cfg.nama_provinsi || defaultConfig.nama_provinsi],
            ['nama_kepala_desa', cfg.nama_kepala_desa || defaultConfig.nama_kepala_desa]
          ])
        });
      }
      
      // Initialize Data SDK
      if (window.dataSdk) {
        const result = await window.dataSdk.init(dataHandler);
        if (!result.isOk) {
          console.error('Failed to initialize Data SDK');
        }
      }
      
      applyConfig();
    }
    
    function applyConfig() {
      const desa = config.nama_desa || defaultConfig.nama_desa;
      const kec = config.nama_kecamatan || defaultConfig.nama_kecamatan;
      
      document.getElementById('loginTitle').textContent = `Sistem Administrasi ${desa}`;
      document.getElementById('loginSubtitle').textContent = `${desa}, Kec. ${kec}`;
      document.getElementById('sidebarTitle').textContent = desa;
      
      // Apply settings fields
      document.getElementById('settingDesa').value = config.nama_desa || defaultConfig.nama_desa;
      document.getElementById('settingKecamatan').value = config.nama_kecamatan || defaultConfig.nama_kecamatan;
      document.getElementById('settingKabupaten').value = config.nama_kabupaten || defaultConfig.nama_kabupaten;
      document.getElementById('settingProvinsi').value = config.nama_provinsi || defaultConfig.nama_provinsi;
      document.getElementById('settingKepalaDesa').value = config.nama_kepala_desa || defaultConfig.nama_kepala_desa;
    }
    
    // ============================================
    // UI UPDATE FUNCTIONS
    // ============================================
    
    function updateUI() {
      const penduduk = allData.filter(d => d.type === DATA_TYPES.PENDUDUK);
      const surat = allData.filter(d => d.type === DATA_TYPES.SURAT);
      
      updateDashboardStats(surat);
      updateChart(surat);
      updateRecentList(surat);
      updatePendudukTable(penduduk);
      updatePengajuanList(surat);
      updateArsipTable(surat);
      updateNotifBadge(surat);
      
      if (currentUser && currentUser.type === 'warga') {
        updateWargaRiwayat(surat);
      }
    }
    
    function updateDashboardStats(surat) {
      const total = surat.length;
      const pending = surat.filter(s => s.status === 'pending').length;
      const process = surat.filter(s => s.status === 'process').length;
      const done = surat.filter(s => s.status === 'done').length;
      
      document.getElementById('statTotal').textContent = total;
      document.getElementById('statPending').textContent = pending;
      document.getElementById('statProcess').textContent = process;
      document.getElementById('statDone').textContent = done;
    }
    
    function updateChart(surat) {
      const container = document.getElementById('chartContainer');
      const counts = {};
      
      Object.keys(JENIS_SURAT).forEach(key => {
        counts[key] = surat.filter(s => s.jenis_surat === key).length;
      });
      
      const maxCount = Math.max(...Object.values(counts), 1);
      
      let html = '';
      Object.entries(JENIS_SURAT).forEach(([key, label]) => {
        const count = counts[key] || 0;
        const width = (count / maxCount) * 100;
        html += `
          <div class="flex items-center gap-3">
            <div class="w-32 text-xs text-slate-600 truncate">${label.replace('Surat Keterangan ', 'SK ')}</div>
            <div class="flex-1 bg-slate-100 rounded-full h-6 overflow-hidden">
              <div class="h-full gradient-bg rounded-full transition-all duration-500" style="width: ${width}%"></div>
            </div>
            <div class="w-8 text-sm font-semibold text-slate-700">${count}</div>
          </div>
        `;
      });
      
      container.innerHTML = html || '<p class="text-center text-slate-400 py-4">Belum ada data</p>';
    }
    
    function updateRecentList(surat) {
      const container = document.getElementById('recentList');
      const recent = [...surat].sort((a, b) => new Date(b.tanggal_pengajuan) - new Date(a.tanggal_pengajuan)).slice(0, 5);
      
      if (recent.length === 0) {
        container.innerHTML = '<p class="text-center text-slate-400 py-8">Belum ada pengajuan</p>';
        return;
      }
      
      container.innerHTML = recent.map(s => {
        const status = STATUS_LABELS[s.status] || STATUS_LABELS.pending;
        return `
          <div class="flex items-center gap-3 p-3 bg-slate-50 rounded-xl">
            <div class="w-10 h-10 bg-white rounded-lg flex items-center justify-center text-lg">${status.icon}</div>
            <div class="flex-1 min-w-0">
              <p class="font-medium text-slate-800 text-sm truncate">${s.nama || 'N/A'}</p>
              <p class="text-xs text-slate-500">${JENIS_SURAT[s.jenis_surat] || s.jenis_surat}</p>
            </div>
            <span class="px-2 py-1 rounded-lg text-xs font-medium ${status.color}">${status.text}</span>
          </div>
        `;
      }).join('');
    }
    
    function updatePendudukTable(penduduk) {
      const container = document.getElementById('pendudukTable');
      const searchTerm = document.getElementById('searchPenduduk')?.value?.toLowerCase() || '';
      
      let filtered = penduduk;
      if (searchTerm) {
        filtered = penduduk.filter(p => 
          p.nik?.toLowerCase().includes(searchTerm) || 
          p.nama?.toLowerCase().includes(searchTerm)
        );
      }
      
      if (filtered.length === 0) {
        container.innerHTML = `
          <tr>
            <td colspan="6" class="px-6 py-12 text-center text-slate-400">
              <span class="text-4xl">👥</span>
              <p class="mt-2">${searchTerm ? 'Tidak ditemukan' : 'Belum ada data penduduk'}</p>
            </td>
          </tr>
        `;
        return;
      }
      
      container.innerHTML = filtered.map(p => `
        <tr class="hover:bg-slate-50 transition-colors">
          <td class="px-6 py-4 text-sm font-mono text-slate-800">${p.nik || '-'}</td>
          <td class="px-6 py-4 text-sm font-medium text-slate-800">${p.nama || '-'}</td>
          <td class="px-6 py-4 text-sm text-slate-600">${p.jenis_kelamin === 'L' ? '👨 L' : '👩 P'}</td>
          <td class="px-6 py-4 text-sm text-slate-600 max-w-xs truncate">${p.alamat || '-'}</td>
          <td class="px-6 py-4 text-sm text-slate-600">${p.pekerjaan || '-'}</td>
          <td class="px-6 py-4 text-center">
            <div class="flex items-center justify-center gap-2">
              <button onclick="editPenduduk('${p.__backendId}')" class="p-2 text-sky-600 hover:bg-sky-50 rounded-lg transition-all" title="Edit">
                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"/>
                </svg>
              </button>
              <button onclick="confirmDeletePenduduk('${p.__backendId}')" class="p-2 text-red-600 hover:bg-red-50 rounded-lg transition-all" title="Hapus">
                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
                </svg>
              </button>
            </div>
          </td>
        </tr>
      `).join('');
    }
    
    function updatePengajuanList(surat) {
      const container = document.getElementById('pengajuanList');
      
      let filtered = surat;
      if (currentFilter !== 'all') {
        filtered = surat.filter(s => s.status === currentFilter);
      }
      
      filtered = [...filtered].sort((a, b) => new Date(b.tanggal_pengajuan) - new Date(a.tanggal_pengajuan));
      
      if (filtered.length === 0) {
        container.innerHTML = `
          <div class="bg-white rounded-2xl p-8 text-center shadow-sm border border-slate-100">
            <span class="text-4xl">📄</span>
            <p class="mt-2 text-slate-400">Tidak ada pengajuan${currentFilter !== 'all' ? ' dengan status ini' : ''}</p>
          </div>
        `;
        return;
      }
      
      container.innerHTML = filtered.map(s => {
        const status = STATUS_LABELS[s.status] || STATUS_LABELS.pending;
        return `
          <div class="bg-white rounded-2xl p-5 shadow-sm border border-slate-100 card-hover">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4">
              <div class="flex items-start gap-4">
                <div class="w-12 h-12 gradient-bg rounded-xl flex items-center justify-center text-white text-xl flex-shrink-0">
                  ${status.icon}
                </div>
                <div>
                  <div class="flex items-center gap-2 mb-1">
                    <h4 class="font-bold text-slate-800">${s.nama || 'N/A'}</h4>
                    <span class="status-badge px-2 py-0.5 rounded-lg text-xs font-medium ${status.color}">${status.text}</span>
                  </div>
                  <p class="text-sm text-slate-600">${JENIS_SURAT[s.jenis_surat] || s.jenis_surat}</p>
                  <p class="text-xs text-slate-400 mt-1">📅 ${formatDate(s.tanggal_pengajuan)} • 🔖 ${s.no_tracking || '-'}</p>
                </div>
              </div>
              <div class="flex items-center gap-2 flex-shrink-0">
                <select onchange="updateStatus('${s.__backendId}', this.value)" class="px-3 py-2 rounded-lg border border-slate-200 text-sm focus:border-sky-500 outline-none">
                  <option value="pending" ${s.status === 'pending' ? 'selected' : ''}>⏳ Menunggu</option>
                  <option value="process" ${s.status === 'process' ? 'selected' : ''}>🔄 Diproses</option>
                  <option value="done" ${s.status === 'done' ? 'selected' : ''}>✅ Selesai</option>
                  <option value="rejected" ${s.status === 'rejected' ? 'selected' : ''}>❌ Ditolak</option>
                </select>
                <button onclick="viewSurat('${s.__backendId}')" class="p-2 text-sky-600 hover:bg-sky-50 rounded-lg transition-all" title="Lihat">
                  <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"/>
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"/>
                  </svg>
                </button>
                <button onclick="printSurat('${s.__backendId}')" class="p-2 text-emerald-600 hover:bg-emerald-50 rounded-lg transition-all" title="Cetak">
                  <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 17h2a2 2 0 002-2v-4a2 2 0 00-2-2H5a2 2 0 00-2 2v4a2 2 0 002 2h2m2 4h6a2 2 0 002-2v-4a2 2 0 00-2-2H9a2 2 0 00-2 2v4a2 2 0 002 2zm8-12V5a2 2 0 00-2-2H9a2 2 0 00-2 2v4h10z"/>
                  </svg>
                </button>
              </div>
            </div>
          </div>
        `;
      }).join('');
    }
    
    function updateArsipTable(surat) {
      const container = document.getElementById('arsipTable');
      const searchTerm = document.getElementById('searchArsip')?.value?.toLowerCase() || '';
      
      let filtered = surat.filter(s => s.status === 'done');
      if (searchTerm) {
        filtered = filtered.filter(s => 
          s.no_tracking?.toLowerCase().includes(searchTerm) || 
          s.nama?.toLowerCase().includes(searchTerm)
        );
      }
      
      if (filtered.length === 0) {
        container.innerHTML = `
          <tr>
            <td colspan="6" class="px-6 py-12 text-center text-slate-400">
              <span class="text-4xl">📁</span>
              <p class="mt-2">${searchTerm ? 'Tidak ditemukan' : 'Belum ada arsip surat'}</p>
            </td>
          </tr>
        `;
        return;
      }
      
      container.innerHTML = filtered.map(s => {
        const status = STATUS_LABELS[s.status] || STATUS_LABELS.pending;
        return `
          <tr class="hover:bg-slate-50 transition-colors">
            <td class="px-6 py-4 text-sm font-mono text-slate-800">${s.no_tracking || '-'}</td>
            <td class="px-6 py-4 text-sm text-slate-600">${JENIS_SURAT[s.jenis_surat]?.replace('Surat Keterangan ', 'SK ') || s.jenis_surat}</td>
            <td class="px-6 py-4 text-sm font-medium text-slate-800">${s.nama || '-'}</td>
            <td class="px-6 py-4 text-sm text-slate-600">${formatDate(s.tanggal_selesai || s.tanggal_pengajuan)}</td>
            <td class="px-6 py-4 text-center">
              <span class="px-2 py-1 rounded-lg text-xs font-medium ${status.color}">${status.text}</span>
            </td>
            <td class="px-6 py-4 text-center">
              <button onclick="printSurat('${s.__backendId}')" class="p-2 text-emerald-600 hover:bg-emerald-50 rounded-lg transition-all" title="Cetak">
                <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 17h2a2 2 0 002-2v-4a2 2 0 00-2-2H5a2 2 0 00-2 2v4a2 2 0 002 2h2m2 4h6a2 2 0 002-2v-4a2 2 0 00-2-2H9a2 2 0 00-2 2v4a2 2 0 002 2zm8-12V5a2 2 0 00-2-2H9a2 2 0 00-2 2v4h10z"/>
                </svg>
              </button>
            </td>
          </tr>
        `;
      }).join('');
    }
    
    function updateNotifBadge(surat) {
      const pending = surat.filter(s => s.status === 'pending').length;
      const badge = document.getElementById('notifBadge');
      if (pending > 0) {
        badge.textContent = pending;
        badge.classList.remove('hidden');
        badge.classList.add('flex');
      } else {
        badge.classList.add('hidden');
        badge.classList.remove('flex');
      }
    }
    
    function updateWargaRiwayat(surat) {
      const container = document.getElementById('wargaRiwayat');
      if (!currentUser) return;
      
      const mySurat = surat.filter(s => s.nik === currentUser.nik);
      
      if (mySurat.length === 0) {
        container.innerHTML = '<p class="text-center text-slate-400 py-4">Belum ada riwayat pengajuan</p>';
        return;
      }
      
      container.innerHTML = mySurat.map(s => {
        const status = STATUS_LABELS[s.status] || STATUS_LABELS.pending;
        return `
          <div class="flex items-center gap-3 p-4 bg-slate-50 rounded-xl">
            <div class="w-10 h-10 gradient-bg rounded-lg flex items-center justify-center text-white">
              ${status.icon}
            </div>
            <div class="flex-1">
              <p class="font-medium text-slate-800 text-sm">${JENIS_SURAT[s.jenis_surat] || s.jenis_surat}</p>
              <p class="text-xs text-slate-500">🔖 ${s.no_tracking} • ${formatDate(s.tanggal_pengajuan)}</p>
            </div>
            <span class="px-2 py-1 rounded-lg text-xs font-medium ${status.color}">${status.text}</span>
          </div>
        `;
      }).join('');
    }
    
    // ============================================
    // LOGIN & NAVIGATION
    // ============================================
    
    function setLoginMode(mode) {
      currentLoginMode = mode;
      const btnAdmin = document.getElementById('btnLoginAdmin');
      const btnWarga = document.getElementById('btnLoginWarga');
      const adminForm = document.getElementById('adminLoginForm');
      const wargaForm = document.getElementById('wargaLoginForm');
      
      if (mode === 'admin') {
        btnAdmin.className = 'flex-1 py-2.5 rounded-lg text-sm font-semibold transition-all bg-white text-sky-600 shadow';
        btnWarga.className = 'flex-1 py-2.5 rounded-lg text-sm font-semibold transition-all text-slate-500';
        adminForm.classList.remove('hidden');
        wargaForm.classList.add('hidden');
      } else {
        btnWarga.className = 'flex-1 py-2.5 rounded-lg text-sm font-semibold transition-all bg-white text-sky-600 shadow';
        btnAdmin.className = 'flex-1 py-2.5 rounded-lg text-sm font-semibold transition-all text-slate-500';
        wargaForm.classList.remove('hidden');
        adminForm.classList.add('hidden');
      }
    }
    
    function loginAdmin() {
      const username = document.getElementById('adminUsername').value;
      const pin = document.getElementById('adminPin').value;
      
      if (username === 'admin' && pin === '123456') {
        currentUser = { type: 'admin', username };
        document.getElementById('loginScreen').classList.add('hidden');
        document.getElementById('adminDashboard').classList.remove('hidden');
        showToast('Selamat datang, Administrator!', 'success');
        updateUI();
      } else {
        showToast('Username atau PIN salah!', 'error');
      }
    }
    
    function loginWarga() {
      const nik = document.getElementById('wargaNik').value;
      
      if (!nik || nik.length !== 16) {
        showToast('NIK harus 16 digit!', 'error');
        return;
      }
      
      const penduduk = allData.find(d => d.type === DATA_TYPES.PENDUDUK && d.nik === nik);
      
      currentUser = { 
        type: 'warga', 
        nik,
        nama: penduduk?.nama || 'Warga',
        data: penduduk
      };
      
      document.getElementById('loginScreen').classList.add('hidden');
      document.getElementById('wargaDashboard').classList.remove('hidden');
      document.getElementById('wargaGreeting').textContent = `Halo, ${currentUser.nama}!`;
      showToast(`Selamat datang, ${currentUser.nama}!`, 'success');
      updateUI();
    }
    
    function cekTracking() {
      const nik = document.getElementById('wargaNik').value;
      if (!nik) {
        showToast('Masukkan NIK terlebih dahulu', 'error');
        return;
      }
      
      const mySurat = allData.filter(d => d.type === DATA_TYPES.SURAT && d.nik === nik);
      
      if (mySurat.length === 0) {
        showToast('Tidak ada pengajuan dengan NIK tersebut', 'info');
        return;
      }
      
      let html = `
        <div class="p-6">
          <div class="flex items-center justify-between mb-6">
            <h3 class="text-xl font-bold text-slate-800">📋 Status Pengajuan</h3>
            <button onclick="closeModal()" class="p-2 hover:bg-slate-100 rounded-lg transition-all">
              <svg class="w-5 h-5 text-slate-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
              </svg>
            </button>
          </div>
          <div class="space-y-3">
      `;
      
      mySurat.forEach(s => {
        const status = STATUS_LABELS[s.status] || STATUS_LABELS.pending;
        html += `
          <div class="flex items-center gap-3 p-4 bg-slate-50 rounded-xl">
            <div class="w-12 h-12 gradient-bg rounded-xl flex items-center justify-center text-white text-xl">
              ${status.icon}
            </div>
            <div class="flex-1">
              <p class="font-semibold text-slate-800">${JENIS_SURAT[s.jenis_surat] || s.jenis_surat}</p>
              <p class="text-sm text-slate-500">🔖 ${s.no_tracking} • ${formatDate(s.tanggal_pengajuan)}</p>
            </div>
            <span class="px-3 py-1 rounded-lg text-sm font-medium ${status.color}">${status.text}</span>
          </div>
        `;
      });
      
      html += '</div></div>';
      
      showModal(html);
    }
    
    function logout() {
      currentUser = null;
      document.getElementById('loginScreen').classList.remove('hidden');
      document.getElementById('adminDashboard').classList.add('hidden');
      document.getElementById('wargaDashboard').classList.add('hidden');
      document.getElementById('adminUsername').value = '';
      document.getElementById('adminPin').value = '';
      document.getElementById('wargaNik').value = '';
    }
    
    function showSection(section) {
      // Hide all sections
      document.querySelectorAll('[id^="section"]').forEach(el => el.classList.add('hidden'));
      
      // Show selected section
      const targetSection = document.getElementById(`section${section.charAt(0).toUpperCase() + section.slice(1)}`);
      if (targetSection) targetSection.classList.remove('hidden');
      
      // Update sidebar
      document.querySelectorAll('[data-section]').forEach(btn => {
        if (btn.dataset.section === section) {
          btn.className = 'sidebar-item w-full flex items-center gap-3 px-4 py-3 rounded-xl bg-white/20 text-white font-medium';
        } else {
          btn.className = 'sidebar-item w-full flex items-center gap-3 px-4 py-3 rounded-xl hover:bg-white/10 text-white/80 font-medium';
        }
      });
      
      // Update header
      const titles = {
        dashboard: ['Dashboard', 'Selamat datang di panel administrasi'],
        penduduk: ['Data Penduduk', 'Kelola data kependudukan'],
        pengajuan: ['Pengajuan Surat', 'Kelola pengajuan surat masuk'],
        arsip: ['Arsip Surat', 'Riwayat surat yang telah selesai'],
        pengaturan: ['Pengaturan', 'Konfigurasi sistem']
      };
      
      const [title, subtitle] = titles[section] || ['Dashboard', ''];
      document.getElementById('pageTitle').textContent = title;
      document.getElementById('pageSubtitle').textContent = subtitle;
    }
    
    function filterPengajuan(filter) {
      currentFilter = filter;
      
      document.querySelectorAll('.filter-btn').forEach(btn => {
        if (btn.dataset.filter === filter) {
          btn.className = 'filter-btn px-4 py-2 rounded-xl bg-slate-800 text-white font-medium text-sm';
        } else {
          btn.className = 'filter-btn px-4 py-2 rounded-xl bg-slate-100 text-slate-600 font-medium text-sm';
        }
      });
      
      const surat = allData.filter(d => d.type === DATA_TYPES.SURAT);
      updatePengajuanList(surat);
    }
    
    // ============================================
    // DATA OPERATIONS
    // ============================================
    
    function showAddPenduduk() {
      const html = `
        <div class="p-6">
          <div class="flex items-center justify-between mb-6">
            <h3 class="text-xl font-bold text-slate-800">➕ Tambah Data Penduduk</h3>
            <button onclick="closeModal()" class="p-2 hover:bg-slate-100 rounded-lg transition-all">
              <svg class="w-5 h-5 text-slate-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
              </svg>
            </button>
          </div>
          <form onsubmit="savePenduduk(event)" class="space-y-4">
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
              <div class="sm:col-span-2">
                <label class="block text-sm font-medium text-slate-700 mb-1.5">NIK (16 digit)</label>
                <input type="text" id="formNik" maxlength="16" required placeholder="Masukkan NIK"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
              </div>
              <div class="sm:col-span-2">
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Nama Lengkap</label>
                <input type="text" id="formNama" required placeholder="Masukkan nama lengkap"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Tempat Lahir</label>
                <input type="text" id="formTempatLahir" required placeholder="Kota/Kabupaten"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Tanggal Lahir</label>
                <input type="date" id="formTglLahir" required
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Jenis Kelamin</label>
                <select id="formJK" required class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
                  <option value="">-- Pilih --</option>
                  <option value="L">Laki-laki</option>
                  <option value="P">Perempuan</option>
                </select>
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Agama</label>
                <select id="formAgama" required class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
                  <option value="">-- Pilih --</option>
                  <option value="Islam">Islam</option>
                  <option value="Kristen">Kristen</option>
                  <option value="Katolik">Katolik</option>
                  <option value="Hindu">Hindu</option>
                  <option value="Buddha">Buddha</option>
                  <option value="Konghucu">Konghucu</option>
                </select>
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Status Perkawinan</label>
                <select id="formStatus" required class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
                  <option value="">-- Pilih --</option>
                  <option value="Belum Kawin">Belum Kawin</option>
                  <option value="Kawin">Kawin</option>
                  <option value="Cerai Hidup">Cerai Hidup</option>
                  <option value="Cerai Mati">Cerai Mati</option>
                </select>
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Pekerjaan</label>
                <input type="text" id="formPekerjaan" required placeholder="Pekerjaan"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
              </div>
              <div class="sm:col-span-2">
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Alamat</label>
                <textarea id="formAlamat" required rows="2" placeholder="Alamat lengkap"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none resize-none"></textarea>
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Nomor KK</label>
                <input type="text" id="formNoKK" maxlength="16" placeholder="Nomor Kartu Keluarga"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
              </div>
            </div>
            <div class="flex gap-3 pt-4">
              <button type="button" onclick="closeModal()" class="flex-1 py-3 border border-slate-200 text-slate-600 rounded-xl font-semibold hover:bg-slate-50 transition-all">
                Batal
              </button>
              <button type="submit" id="btnSavePenduduk" class="flex-1 py-3 gradient-bg text-white rounded-xl font-semibold hover:opacity-90 transition-all">
                💾 Simpan
              </button>
            </div>
          </form>
        </div>
      `;
      showModal(html);
    }
    
    async function savePenduduk(e) {
      e.preventDefault();
      
      const btn = document.getElementById('btnSavePenduduk');
      btn.disabled = true;
      btn.innerHTML = '<span class="animate-pulse">Menyimpan...</span>';
      
      const pendudukCount = allData.filter(d => d.type === DATA_TYPES.PENDUDUK).length;
      if (pendudukCount >= 999) {
        showToast('Batas maksimum data tercapai (999)', 'error');
        btn.disabled = false;
        btn.innerHTML = '💾 Simpan';
        return;
      }
      
      const data = {
        type: DATA_TYPES.PENDUDUK,
        nik: document.getElementById('formNik').value,
        nama: document.getElementById('formNama').value,
        tempat_lahir: document.getElementById('formTempatLahir').value,
        tanggal_lahir: document.getElementById('formTglLahir').value,
        jenis_kelamin: document.getElementById('formJK').value,
        agama: document.getElementById('formAgama').value,
        status_perkawinan: document.getElementById('formStatus').value,
        pekerjaan: document.getElementById('formPekerjaan').value,
        alamat: document.getElementById('formAlamat').value,
        no_kk: document.getElementById('formNoKK').value
      };
      
      // Check duplicate NIK
      const existing = allData.find(d => d.type === DATA_TYPES.PENDUDUK && d.nik === data.nik);
      if (existing) {
        showToast('NIK sudah terdaftar!', 'error');
        btn.disabled = false;
        btn.innerHTML = '💾 Simpan';
        return;
      }
      
      if (window.dataSdk) {
        const result = await window.dataSdk.create(data);
        if (result.isOk) {
          showToast('Data penduduk berhasil ditambahkan!', 'success');
          closeModal();
        } else {
          showToast('Gagal menyimpan data', 'error');
        }
      }
      
      btn.disabled = false;
      btn.innerHTML = '💾 Simpan';
    }
    
    function editPenduduk(id) {
      const penduduk = allData.find(d => d.__backendId === id);
      if (!penduduk) return;
      
      const html = `
        <div class="p-6">
          <div class="flex items-center justify-between mb-6">
            <h3 class="text-xl font-bold text-slate-800">✏️ Edit Data Penduduk</h3>
            <button onclick="closeModal()" class="p-2 hover:bg-slate-100 rounded-lg transition-all">
              <svg class="w-5 h-5 text-slate-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
              </svg>
            </button>
          </div>
          <form onsubmit="updatePenduduk(event, '${id}')" class="space-y-4">
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
              <div class="sm:col-span-2">
                <label class="block text-sm font-medium text-slate-700 mb-1.5">NIK (16 digit)</label>
                <input type="text" id="editNik" maxlength="16" required value="${penduduk.nik || ''}"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 bg-slate-50 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none" readonly>
              </div>
              <div class="sm:col-span-2">
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Nama Lengkap</label>
                <input type="text" id="editNama" required value="${penduduk.nama || ''}"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Tempat Lahir</label>
                <input type="text" id="editTempatLahir" required value="${penduduk.tempat_lahir || ''}"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Tanggal Lahir</label>
                <input type="date" id="editTglLahir" required value="${penduduk.tanggal_lahir || ''}"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Jenis Kelamin</label>
                <select id="editJK" required class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
                  <option value="L" ${penduduk.jenis_kelamin === 'L' ? 'selected' : ''}>Laki-laki</option>
                  <option value="P" ${penduduk.jenis_kelamin === 'P' ? 'selected' : ''}>Perempuan</option>
                </select>
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Agama</label>
                <select id="editAgama" required class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
                  <option value="Islam" ${penduduk.agama === 'Islam' ? 'selected' : ''}>Islam</option>
                  <option value="Kristen" ${penduduk.agama === 'Kristen' ? 'selected' : ''}>Kristen</option>
                  <option value="Katolik" ${penduduk.agama === 'Katolik' ? 'selected' : ''}>Katolik</option>
                  <option value="Hindu" ${penduduk.agama === 'Hindu' ? 'selected' : ''}>Hindu</option>
                  <option value="Buddha" ${penduduk.agama === 'Buddha' ? 'selected' : ''}>Buddha</option>
                  <option value="Konghucu" ${penduduk.agama === 'Konghucu' ? 'selected' : ''}>Konghucu</option>
                </select>
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Status Perkawinan</label>
                <select id="editStatus" required class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
                  <option value="Belum Kawin" ${penduduk.status_perkawinan === 'Belum Kawin' ? 'selected' : ''}>Belum Kawin</option>
                  <option value="Kawin" ${penduduk.status_perkawinan === 'Kawin' ? 'selected' : ''}>Kawin</option>
                  <option value="Cerai Hidup" ${penduduk.status_perkawinan === 'Cerai Hidup' ? 'selected' : ''}>Cerai Hidup</option>
                  <option value="Cerai Mati" ${penduduk.status_perkawinan === 'Cerai Mati' ? 'selected' : ''}>Cerai Mati</option>
                </select>
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Pekerjaan</label>
                <input type="text" id="editPekerjaan" required value="${penduduk.pekerjaan || ''}"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
              </div>
              <div class="sm:col-span-2">
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Alamat</label>
                <textarea id="editAlamat" required rows="2"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none resize-none">${penduduk.alamat || ''}</textarea>
              </div>
              <div>
                <label class="block text-sm font-medium text-slate-700 mb-1.5">Nomor KK</label>
                <input type="text" id="editNoKK" maxlength="16" value="${penduduk.no_kk || ''}"
                  class="w-full px-4 py-3 rounded-xl border border-slate-200 focus:border-sky-500 focus:ring-2 focus:ring-sky-100 outline-none">
              </div>
            </div>
            <div class="flex gap-3 pt-4">
              <button type="button" onclick="closeModal()" class="flex-1 py-3 border border-slate-200 text-slate-600 rounded-xl font-semibold hover:bg-slate-50 transition-all">
                Batal
              </button>
              <button type="submit" id="btnUpdatePenduduk" class="flex-1 py-3 gradient-bg text-white rounded-xl font-semibold hover:opacity-90 transition-all">
                💾 Simpan Perubahan
              </button>
            </div>
          </form>
        </div>
      `;
      showModal(html);
    }
    
    async function updatePenduduk(e, id) {
      e.preventDefault();
      
      const btn = document.getElementById('btnUpdatePenduduk');
      btn.disabled = true;
      btn.innerHTML = '<span class="animate-pulse">Menyimpan...</span>';
      
      const penduduk = allData.find(d => d.__backendId === id);
      if (!penduduk) return;
      
      const updatedData = {
        ...penduduk,
        nama: document.getElementById('editNama').value,
        tempat_lahir: document.getElementById('editTempatLahir').value,
        tanggal_lahir: document.getElementById('editTglLahir').value,
        jenis_kelamin: document.getElementById('editJK').value,
        agama: document.getElementById('editAgama').value,
        status_perkawinan: document.getElementById('editStatus').value,
        pekerjaan: document.getElementById('editPekerjaan').value,
        alamat: document.getElementById('editAlamat').value,
        no_kk: document.getElementById('editNoKK').value
      };
      
      if (window.dataSdk) {
        const result = await window.dataSdk.update(updatedData);
        if (result.isOk) {
          showToast('Data berhasil diperbarui!', 'success');
          closeModal();
        } else {
          showToast('Gagal memperbarui data', 'error');
        }
      }
      
      btn.disabled = false;
      btn.innerHTML = '💾 Simpan Perubahan';
    }
    
    function confirmDeletePenduduk(id) {
      const penduduk = allData.find(d => d.__backendId === id);
      if (!penduduk) return;
      
      const html = `
        <div class="p-6 text-center">
          <div class="w-16 h-16 bg-red-100 rounded-full flex items-center justify-center mx-auto mb-4">
            <svg class="w-8 h-8 text-red-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"/>
            </svg>
          </div>
          <h3 class="text-xl font-bold text-slate-800 mb-2">Hapus Data Penduduk?</h3>
          <p class="text-slate-500 mb-6">Data <strong>${penduduk.nama}</strong> akan dihapus permanen.</p>
          <div class="flex gap-3">
            <button onclick="closeModal()" class="flex-1 py-3 border border-slate-200 text-slate-600 rounded-xl font-semibold hover:bg-slate-50 transition-all">
              Batal
            </button>
            <button onclick="deletePenduduk('${id}')" id="btnDeletePenduduk" class="flex-1 py-3 bg-red-600 text-white rounded-xl font-semibold hover:bg-red-700 transition-all">
              🗑️ Hapus
            </button>
          </div>
        </div>
      `;
      showModal(html);
    }
    
    async function deletePenduduk(id) {
      const btn = document.getElementById('btnDeletePenduduk');
      btn.disabled = true;
      btn.innerHTML = '<span class="animate-pulse">Menghapus...</span>';
      
      const penduduk = allData.find(d => d.__backendId === id);
      if (!penduduk) return;
      
      if (window.dataSdk) {
        const result = await window.dataSdk.delete(penduduk);
        if (result.isOk) {
          showToast('Data berhasil dihapus!', 'success');
          closeModal();
        } else {
          showToast('Gagal menghapus data', 'error');
        }
      }
      
      btn.disabled = false;
      btn.innerHTML = '🗑️ Hapus';
    }
    
    // ============================================
    // SURAT OPERATIONS
    // ============================================
    
    async function submitPengajuan() {
      const jenisSurat = document.getElementById('wargaJenisSurat').value;
      const keperluan = document.getElementById('wargaKeperluan').value;
      const keterangan = document.getElementById('wargaKeterangan').value;
      
      if (!jenisSurat) {
        showToast('Pilih jenis surat terlebih dahulu', 'error');
        return;
      }
      
      if (!keperluan) {
        showToast('Isi keperluan surat', 'error');
        return;
      }
      
      const btn = document.getElementById('btnSubmitPengajuan');
      btn.disabled = true;
      btn.innerHTML = '<span class="animate-pulse">Mengirim...</span>';
      
      const suratCount = allData.filter(d => d.type === DATA_TYPES.SURAT).length;
      if (suratCount >= 999) {
        showToast('Batas maksimum pengajuan tercapai', 'error');
        btn.disabled = false;
        btn.innerHTML = '📤 Kirim Pengajuan';
        return;
      }
      
      const penduduk = currentUser?.data;
      const noTracking = generateTrackingNumber();
      
      const data = {
        type: DATA_TYPES.SURAT,
        nik: currentUser?.nik || '',
        nama: penduduk?.nama || currentUser?.nama || 'Warga',
        tempat_lahir: penduduk?.tempat_lahir || '',
        tanggal_lahir: penduduk?.tanggal_lahir || '',
        jenis_kelamin: penduduk?.jenis_kelamin || '',
        alamat: penduduk?.alamat || '',
        agama: penduduk?.agama || '',
        status_perkawinan: penduduk?.status_perkawinan || '',
        pekerjaan: penduduk?.pekerjaan || '',
        no_kk: penduduk?.no_kk || '',
        jenis_surat: jenisSurat,
        keperluan: keperluan,
        keterangan: keterangan,
        status: 'pending',
        no_tracking: noTracking,
        tanggal_pengajuan: new Date().toISOString(),
        tanggal_selesai: ''
      };
      
      if (window.dataSdk) {
        const result = await window.dataSdk.create(data);
        if (result.isOk) {
          showToast(`Pengajuan berhasil! No. Tracking: ${noTracking}`, 'success');
          document.getElementById('wargaJenisSurat').value = '';
          document.getElementById('wargaKeperluan').value = '';
          document.getElementById('wargaKeterangan').value = '';
        } else {
          showToast('Gagal mengirim pengajuan', 'error');
        }
      }
      
      btn.disabled = false;
      btn.innerHTML = '📤 Kirim Pengajuan';
    }
    
    async function updateStatus(id, newStatus) {
      const surat = allData.find(d => d.__backendId === id);
      if (!surat) return;
      
      const updatedData = {
        ...surat,
        status: newStatus,
        tanggal_selesai: newStatus === 'done' ? new Date().toISOString() : surat.tanggal_selesai
      };
      
      if (window.dataSdk) {
        const result = await window.dataSdk.update(updatedData);
        if (result.isOk) {
          showToast(`Status diubah ke ${STATUS_LABELS[newStatus]?.text || newStatus}`, 'success');
        } else {
          showToast('Gagal mengubah status', 'error');
        }
      }
    }
    
    function viewSurat(id) {
      const surat = allData.find(d => d.__backendId === id);
      if (!surat) return;
      
      const status = STATUS_LABELS[surat.status] || STATUS_LABELS.pending;
      
      const html = `
        <div class="p-6">
          <div class="flex items-center justify-between mb-6">
            <h3 class="text-xl font-bold text-slate-800">📄 Detail Pengajuan</h3>
            <button onclick="closeModal()" class="p-2 hover:bg-slate-100 rounded-lg transition-all">
              <svg class="w-5 h-5 text-slate-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
              </svg>
            </button>
          </div>
          
          <div class="space-y-4">
            <div class="flex items-center gap-3 p-4 bg-slate-50 rounded-xl">
              <span class="text-2xl">${status.icon}</span>
              <div class="flex-1">
                <p class="font-bold text-slate-800">${JENIS_SURAT[surat.jenis_surat] || surat.jenis_surat}</p>
                <p class="text-sm text-slate-500">No. Tracking: ${surat.no_tracking}</p>
              </div>
              <span class="px-3 py-1 rounded-lg text-sm font-medium ${status.color}">${status.text}</span>
            </div>
            
            <div class="grid grid-cols-2 gap-4">
              <div>
                <p class="text-xs text-slate-500">NIK</p>
                <p class="font-medium text-slate-800">${surat.nik || '-'}</p>
              </div>
              <div>
                <p class="text-xs text-slate-500">Nama</p>
                <p class="font-medium text-slate-800">${surat.nama || '-'}</p>
              </div>
              <div>
                <p class="text-xs text-slate-500">Tempat/Tgl Lahir</p>
                <p class="font-medium text-slate-800">${surat.tempat_lahir || '-'}, ${formatDate(surat.tanggal_lahir)}</p>
              </div>
              <div>
                <p class="text-xs text-slate-500">Jenis Kelamin</p>
                <p class="font-medium text-slate-800">${surat.jenis_kelamin === 'L' ? 'Laki-laki' : 'Perempuan'}</p>
              </div>
              <div class="col-span-2">
                <p class="text-xs text-slate-500">Alamat</p>
                <p class="font-medium text-slate-800">${surat.alamat || '-'}</p>
              </div>
              <div>
                <p class="text-xs text-slate-500">Agama</p>
                <p class="font-medium text-slate-800">${surat.agama || '-'}</p>
              </div>
              <div>
                <p class="text-xs text-slate-500">Status Perkawinan</p>
                <p class="font-medium text-slate-800">${surat.status_perkawinan || '-'}</p>
              </div>
              <div>
                <p class="text-xs text-slate-500">Pekerjaan</p>
                <p class="font-medium text-slate-800">${surat.pekerjaan || '-'}</p>
              </div>
              <div>
                <p class="text-xs text-slate-500">No. KK</p>
                <p class="font-medium text-slate-800">${surat.no_kk || '-'}</p>
              </div>
              <div class="col-span-2">
                <p class="text-xs text-slate-500">Keperluan</p>
                <p class="font-medium text-slate-800">${surat.keperluan || '-'}</p>
              </div>
              <div class="col-span-2">
                <p class="text-xs text-slate-500">Keterangan</p>
                <p class="font-medium text-slate-800">${surat.keterangan || '-'}</p>
              </div>
              <div>
                <p class="text-xs text-slate-500">Tanggal Pengajuan</p>
                <p class="font-medium text-slate-800">${formatDate(surat.tanggal_pengajuan)}</p>
              </div>
            </div>
            
            <div class="flex gap-3 pt-4">
              <button onclick="closeModal()" class="flex-1 py-3 border border-slate-200 text-slate-600 rounded-xl font-semibold hover:bg-slate-50 transition-all">
                Tutup
              </button>
              <button onclick="closeModal(); printSurat('${id}')" class="flex-1 py-3 gradient-bg text-white rounded-xl font-semibold hover:opacity-90 transition-all">
                🖨️ Cetak Surat
              </button>
            </div>
          </div>
        </div>
      `;
      showModal(html);
    }
    
    function printSurat(id) {
      const surat = allData.find(d => d.__backendId === id);
      if (!surat) return;
      
      const desa = config.nama_desa || defaultConfig.nama_desa;
      const kec = config.nama_kecamatan || defaultConfig.nama_kecamatan;
      const kab = config.nama_kabupaten || defaultConfig.nama_kabupaten;
      const prov = config.nama_provinsi || defaultConfig.nama_provinsi;
      const kepalaDesa = config.nama_kepala_desa || defaultConfig.nama_kepala_desa;
      
      const today = new Date();
      const tanggalSurat = formatDateLong(today);
      
      let isiSurat = '';
      
      switch(surat.jenis_surat) {
        case 'domisili':
          isiSurat = `
            <p style="text-indent: 50px; text-align: justify; line-height: 1.8;">
              Yang bertanda tangan di bawah ini, Kepala ${desa}, Kecamatan ${kec}, ${kab}, ${prov}, dengan ini menerangkan bahwa:
            </p>
            <table style="margin: 20px 0 20px 50px; line-height: 1.8;">
              <tr><td style="width: 180px;">Nama</td><td>: ${surat.nama}</td></tr>
              <tr><td>NIK</td><td>: ${surat.nik}</td></tr>
              <tr><td>Tempat/Tgl Lahir</td><td>: ${surat.tempat_lahir}, ${formatDate(surat.tanggal_lahir)}</td></tr>
              <tr><td>Jenis Kelamin</td><td>: ${surat.jenis_kelamin === 'L' ? 'Laki-laki' : 'Perempuan'}</td></tr>
              <tr><td>Agama</td><td>: ${surat.agama}</td></tr>
              <tr><td>Pekerjaan</td><td>: ${surat.pekerjaan}</td></tr>
              <tr><td>Alamat</td><td>: ${surat.alamat}</td></tr>
            </table>
            <p style="text-indent: 50px; text-align: justify; line-height: 1.8;">
              Adalah benar warga yang berdomisili di ${desa}, Kecamatan ${kec}, ${kab}, ${prov}.
            </p>
            <p style="text-indent: 50px; text-align: justify; line-height: 1.8;">
              Surat keterangan ini dibuat untuk keperluan: <strong>${surat.keperluan}</strong>.
            </p>
            <p style="text-indent: 50px; text-align: justify; line-height: 1.8;">
              Demikian surat keterangan ini dibuat dengan sebenarnya untuk dapat dipergunakan sebagaimana mestinya.
            </p>
          `;
          break;
        case 'usaha':
          isiSurat = `
            <p style="text-indent: 50px; text-align: justify; line-height: 1.8;">
              Yang bertanda tangan di bawah ini, Kepala ${desa}, Kecamatan ${kec}, ${kab}, ${prov}, dengan ini menerangkan bahwa:
            </p>
            <table style="margin: 20px 0 20px 50px; line-height: 1.8;">
              <tr><td style="width: 180px;">Nama</td><td>: ${surat.nama}</td></tr>
              <tr><td>NIK</td><td>: ${surat.nik}</td></tr>
              <tr><td>Tempat/Tgl Lahir</td><td>: ${surat.tempat_lahir}, ${formatDate(surat.tanggal_lahir)}</td></tr>
              <tr><td>Jenis Kelamin</td><td>: ${surat.jenis_kelamin === 'L' ? 'Laki-laki' : 'Perempuan'}</td></tr>
              <tr><td>Alamat</td><td>: ${surat.alamat}</td></tr>
            </table>
            <p style="text-indent: 50px; text-align: justify; line-height: 1.8;">
              Adalah benar warga kami yang memiliki usaha dan berdomisili di wilayah ${desa}.
            </p>
            <p style="text-indent: 50px; text-align: justify; line-height: 1.8;">
              Surat keterangan ini dibuat untuk keperluan: <strong>${surat.keperluan}</strong>.
            </p>
            <p style="text-indent: 50px; text-align: justify; line-height: 1.8;">
              Demikian surat keterangan ini dibuat dengan sebenarnya untuk dapat dipergunakan sebagaimana mestinya.
            </p>
          `;
          break;
        default:
          isiSurat = `
            <p style="text-indent: 50px; text-align: justify; line-height: 1.8;">
              Yang bertanda tangan di bawah ini, Kepala ${desa}, Kecamatan ${kec}, ${kab}, ${prov}, dengan ini menerangkan bahwa:
            </p>
            <table style="margin: 20px 0 20px 50px; line-height: 1.8;">
              <tr><td style="width: 180px;">Nama</td><td>: ${surat.nama}</td></tr>
              <tr><td>NIK</td><td>: ${surat.nik}</td></tr>
              <tr><td>Tempat/Tgl Lahir</td><td>: ${surat.tempat_lahir}, ${formatDate(surat.tanggal_lahir)}</td></tr>
              <tr><td>Jenis Kelamin</td><td>: ${surat.jenis_kelamin === 'L' ? 'Laki-laki' : 'Perempuan'}</td></tr>
              <tr><td>Agama</td><td>: ${surat.agama}</td></tr>
              <tr><td>Pekerjaan</td><td>: ${surat.pekerjaan}</td></tr>
              <tr><td>Alamat</td><td>: ${surat.alamat}</td></tr>
            </table>
            <p style="text-indent: 50px; text-align: justify; line-height: 1.8;">
              Adalah benar warga yang berdomisili di ${desa}, Kecamatan ${kec}, ${kab}, ${prov}.
            </p>
            <p style="text-indent: 50px; text-align: justify; line-height: 1.8;">
              Surat keterangan ini dibuat untuk keperluan: <strong>${surat.keperluan}</strong>.
            </p>
            ${surat.keterangan ? `<p style="text-indent: 50px; text-align: justify; line-height: 1.8;">Keterangan: ${surat.keterangan}</p>` : ''}
            <p style="text-indent: 50px; text-align: justify; line-height: 1.8;">
              Demikian surat keterangan ini dibuat dengan sebenarnya untuk dapat dipergunakan sebagaimana mestinya.
            </p>
          `;
      }
      
      const printContent = `
        <div class="print-area" style="font-family: 'Times New Roman', Times, serif; font-size: 12pt; color: #000;">
          <!-- KOP SURAT -->
          <div style="text-align: center; border-bottom: 3px double #000; padding-bottom: 15px; margin-bottom: 20px;">
            <p style="font-size: 14pt; font-weight: bold; margin: 0;">PEMERINTAH ${kab.toUpperCase()}</p>
            <p style="font-size: 14pt; font-weight: bold; margin: 0;">KECAMATAN ${kec.toUpperCase()}</p>
            <p style="font-size: 18pt; font-weight: bold; margin: 5px 0;">${desa.toUpperCase()}</p>
            <p style="font-size: 10pt; margin: 0;">${prov}</p>
          </div>
          
          <!-- JUDUL SURAT -->
          <div style="text-align: center; margin-bottom: 20px;">
            <p style="font-size: 14pt; font-weight: bold; text-decoration: underline; margin: 0;">${JENIS_SURAT[surat.jenis_surat]?.toUpperCase() || 'SURAT KETERANGAN'}</p>
            <p style="font-size: 11pt; margin: 5px 0;">Nomor: ${surat.no_tracking}</p>
          </div>
          
          <!-- ISI SURAT -->
          ${isiSurat}
          
          <!-- TANDA TANGAN -->
          <div style="margin-top: 40px; display: flex; justify-content: flex-end;">
            <div style="text-align: center; width: 250px;">
              <p style="margin: 0;">${desa}, ${tanggalSurat}</p>
              <p style="margin: 5px 0;">Kepala ${desa},</p>
              <div style="height: 80px; display: flex; align-items: center; justify-content: center;">
                <div style="border: 2px dashed #ccc; border-radius: 50%; width: 70px; height: 70px; display: flex; align-items: center; justify-content: center; font-size: 10px; color: #999;">
                  Stempel
                </div>
              </div>
              <p style="font-weight: bold; text-decoration: underline; margin: 0;">${kepalaDesa}</p>
            </div>
          </div>
        </div>
      `;
      
      const html = `
        <div class="p-6">
          <div class="flex items-center justify-between mb-4">
            <h3 class="text-xl font-bold text-slate-800">🖨️ Preview Surat</h3>
            <button onclick="closeModal()" class="p-2 hover:bg-slate-100 rounded-lg transition-all">
              <svg class="w-5 h-5 text-slate-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
              </svg>
            </button>
          </div>
          
          <div class="border rounded-xl overflow-hidden bg-white max-h-96 overflow-y-auto">
            ${printContent}
          </div>
          
          <div class="flex gap-3 mt-4">
            <button onclick="closeModal()" class="flex-1 py-3 border border-slate-200 text-slate-600 rounded-xl font-semibold hover:bg-slate-50 transition-all">
              Tutup
            </button>
            <button onclick="doPrint()" class="flex-1 py-3 gradient-bg text-white rounded-xl font-semibold hover:opacity-90 transition-all">
              🖨️ Cetak Sekarang
            </button>
          </div>
        </div>
      `;
      
      document.getElementById('printArea').innerHTML = printContent;
      showModal(html);
    }
    
    function doPrint() {
      window.print();
    }
    
    // ============================================
    // SETTINGS & EXPORT
    // ============================================
    
    async function saveSettings() {
      const newSettings = {
        nama_desa: document.getElementById('settingDesa').value,
        nama_kecamatan: document.getElementById('settingKecamatan').value,
        nama_kabupaten: document.getElementById('settingKabupaten').value,
        nama_provinsi: document.getElementById('settingProvinsi').value,
        nama_kepala_desa: document.getElementById('settingKepalaDesa').value
      };
      
      config = { ...config, ...newSettings };
      
      if (window.elementSdk) {
        await window.elementSdk.setConfig(newSettings);
      }
      
      applyConfig();
      showToast('Pengaturan berhasil disimpan!', 'success');
    }
    
    function exportData(format) {
      const surat = allData.filter(d => d.type === DATA_TYPES.SURAT);
      
      if (surat.length === 0) {
        showToast('Tidak ada data untuk diexport', 'info');
        return;
      }
      
      if (format === 'excel') {
        let csv = 'No Tracking,Jenis Surat,NIK,Nama,Alamat,Keperluan,Status,Tanggal Pengajuan\n';
        
        surat.forEach(s => {
          csv += `"${s.no_tracking}","${JENIS_SURAT[s.jenis_surat] || s.jenis_surat}","${s.nik}","${s.nama}","${s.alamat}","${s.keperluan}","${STATUS_LABELS[s.status]?.text || s.status}","${formatDate(s.tanggal_pengajuan)}"\n`;
        });
        
        const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
        const url = URL.createObjectURL(blob);
        const link = document.createElement('a');
        link.href = url;
        link.download = `data_surat_${formatDateFile(new Date())}.csv`;
        link.click();
        URL.revokeObjectURL(url);
        
        showToast('Data berhasil diexport!', 'success');
      }
    }
    
    // ============================================
    // UTILITY FUNCTIONS
    // ============================================
    
    function generateTrackingNumber() {
      const date = new Date();
      const year = date.getFullYear();
      const month = String(date.getMonth() + 1).padStart(2, '0');
      const random = Math.floor(Math.random() * 9000) + 1000;
      return `SKD/${year}${month}/${random}`;
    }
    
    function formatDate(dateStr) {
      if (!dateStr) return '-';
      const date = new Date(dateStr);
      if (isNaN(date)) return dateStr;
      return date.toLocaleDateString('id-ID', { day: 'numeric', month: 'short', year: 'numeric' });
    }
    
    function formatDateLong(date) {
      const months = ['Januari', 'Februari', 'Maret', 'April', 'Mei', 'Juni', 'Juli', 'Agustus', 'September', 'Oktober', 'November', 'Desember'];
      return `${date.getDate()} ${months[date.getMonth()]} ${date.getFullYear()}`;
    }
    
    function formatDateFile(date) {
      return date.toISOString().split('T')[0].replace(/-/g, '');
    }
    
    function showModal(content) {
      document.getElementById('modalContent').innerHTML = content;
      document.getElementById('modalContainer').classList.remove('hidden');
    }
    
    function closeModal() {
      document.getElementById('modalContainer').classList.add('hidden');
    }
    
    function showToast(message, type = 'info') {
      const toast = document.getElementById('toast');
      const toastMessage = document.getElementById('toastMessage');
      
      const colors = {
        success: 'bg-emerald-500',
        error: 'bg-red-500',
        info: 'bg-sky-500'
      };
      
      toast.className = `fixed bottom-4 right-4 z-50 px-6 py-4 rounded-xl shadow-lg text-white font-medium slide-in ${colors[type] || colors.info}`;
      toastMessage.textContent = message;
      toast.classList.remove('hidden');
      
      setTimeout(() => {
        toast.classList.add('hidden');
      }, 3000);
    }
    
    function toggleNotif() {
      showSection('pengajuan');
      filterPengajuan('pending');
    }
    
    // Search handlers
    document.addEventListener('DOMContentLoaded', () => {
      const searchPenduduk = document.getElementById('searchPenduduk');
      if (searchPenduduk) {
        searchPenduduk.addEventListener('input', () => {
          const penduduk = allData.filter(d => d.type === DATA_TYPES.PENDUDUK);
          updatePendudukTable(penduduk);
        });
      }
      
      const searchArsip = document.getElementById('searchArsip');
      if (searchArsip) {
        searchArsip.addEventListener('input', () => {
          const surat = allData.filter(d => d.type === DATA_TYPES.SURAT);
          updateArsipTable(surat);
        });
      }
    });
    
    // Initialize app
    initApp();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9ca1136072944ab2',t:'MTc3MDQ0ODMxMi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
