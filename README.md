<!DOCTYPE html>
<html lang="th" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AURUM GOLD - แพลตฟอร์มออมทองดิจิทัล</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        gold: {
                            50: '#fffbeb',
                            100: '#fef3c7',
                            200: '#fde68a',
                            300: '#fcd34d',
                            400: '#fbbf24',
                            500: '#f59e0b',
                            600: '#d97706',
                            700: '#b45309',
                            800: '#92400e',
                            900: '#78350f',
                            glow: '#ffd700'
                        },
                        navy: {
                            800: '#0f172a',
                            900: '#0b0f19',
                            950: '#030712'
                        }
                    },
                    fontFamily: {
                        sans: ['Kanit', 'Inter', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Kanit & Inter Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Kanit:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Kanit', 'Inter', sans-serif;
            background-color: #030712;
            color: #f1f5f9;
        }
        .gold-gradient-text {
            background: linear-gradient(135deg, #fde68a 0%, #f59e0b 50%, #d97706 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .gold-gradient-bg {
            background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
        }
        .gold-gradient-bg-hover:hover {
            background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
        }
        .gold-card-glow {
            box-shadow: 0 0 20px rgba(245, 158, 11, 0.15);
            border: 1px solid rgba(245, 158, 11, 0.25);
        }
        .glass-panel {
            background: rgba(15, 23, 42, 0.8);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0b0f19;
        }
        ::-webkit-scrollbar-thumb {
            background: #1e293b;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #d97706;
        }
        .pulse-emerald {
            animation: pulse-emerald 2s infinite;
        }
        @keyframes pulse-emerald {
            0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(16, 185, 129, 0.7); }
            70% { transform: scale(1); box-shadow: 0 0 0 8px rgba(16, 185, 129, 0); }
            100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(16, 185, 129, 0); }
        }
    </style>
</head>
<body class="min-h-screen bg-navy-950 text-slate-100 flex flex-col justify-between selection:bg-amber-500 selection:text-navy-950">

    <!-- HEADER / NAVIGATION -->
    <header class="sticky top-0 z-40 glass-panel border-b border-slate-800/80 px-4 lg:px-8 py-3">
        <div class="max-w-7xl mx-auto flex items-center justify-between">
            <!-- Brand Logo & Title -->
            <div class="flex items-center space-x-3">
                <div class="w-11 h-11 rounded-2xl gold-gradient-bg flex items-center justify-center text-navy-950 font-black text-2xl shadow-lg shadow-amber-500/20">
                    <i class="fa-solid fa-coins"></i>
                </div>
                <div>
                    <div class="flex items-center space-x-2">
                        <h1 class="font-extrabold text-xl leading-none tracking-wide gold-gradient-text uppercase">AURUM GOLD</h1>
                        <span class="text-[10px] bg-amber-500/20 text-amber-300 font-mono font-semibold px-2 py-0.5 rounded-full border border-amber-500/30">PRO</span>
                    </div>
                    <span class="text-[10px] text-slate-400 tracking-wider font-light block mt-0.5">แพลตฟอร์มออมทองดิจิทัลสถาบันการเงิน</span>
                </div>
            </div>

            <!-- Signal & Price Ticker Indicator -->
            <div class="hidden lg:flex items-center space-x-4 bg-navy-900/90 px-4 py-1.5 rounded-full border border-slate-800 text-xs">
                <div class="flex items-center space-x-2">
                    <div class="w-2.5 h-2.5 rounded-full bg-emerald-500 pulse-emerald"></div>
                    <span class="text-slate-300 font-medium">สมาคมฯ API Sync</span>
                </div>
                <span class="text-slate-700">|</span>
                <span class="text-slate-300 font-mono">Spot: <span class="text-amber-400 font-semibold" id="header-spot-price">$2,742.50</span></span>
                <span class="text-slate-700">|</span>
                <span class="text-slate-300 font-mono">FX: <span class="text-slate-200" id="header-fx-rate">35.82 THB/$</span></span>
            </div>

            <!-- Right Controls: Security Badges & Portal Switcher -->
            <div class="flex items-center space-x-3">
                <!-- Admin/User Portal Switcher Button -->
                <button id="toggle-admin-btn" onclick="togglePortalMode()" class="px-3.5 py-2 rounded-xl bg-slate-900 hover:bg-slate-800 text-slate-200 text-xs font-semibold border border-amber-500/30 flex items-center space-x-2 transition shadow-md">
                    <i class="fa-solid fa-user-shield text-amber-500 text-sm"></i>
                    <span id="view-mode-label">สลับเป็น Admin Control</span>
                </button>

                <!-- User Profile Badge -->
                <div class="hidden sm:flex items-center space-x-3 pl-3 border-l border-slate-800">
                    <div class="relative">
                        <img src="https://placehold.co/100x100/0f172a/f59e0b?text=USER" alt="User Profile" class="w-9 h-9 rounded-full border-2 border-amber-500/60 object-cover">
                        <span class="absolute bottom-0 right-0 w-3 h-3 bg-emerald-500 border-2 border-navy-950 rounded-full" title="KYC Verified"></span>
                    </div>
                    <div class="text-left">
                        <div class="text-xs font-bold text-slate-100 flex items-center space-x-1">
                            <span>คุณสมชาย มั่งคั่ง</span>
                            <i class="fa-solid fa-circle-check text-emerald-400 text-[11px]" title="KYC Level 2 Complete"></i>
                        </div>
                        <div class="flex items-center space-x-1 mt-0.5">
                            <span class="text-[9px] text-emerald-400 bg-emerald-950/80 border border-emerald-800/80 px-1.5 rounded font-mono">KYC L2</span>
                            <span class="text-[9px] text-slate-400 bg-slate-800 px-1.5 rounded font-mono">ISO27001</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </header>

    <main class="max-w-7xl w-full mx-auto px-4 lg:px-8 py-6 space-y-6 flex-grow">

        <!-- REAL-TIME GOLD PRICE TICKER BANNER -->
        <section class="grid grid-cols-1 lg:grid-cols-4 gap-4">
            <!-- Thai Gold Market Ticker Widget -->
            <div class="lg:col-span-3 glass-panel rounded-2xl p-4.5 gold-card-glow flex flex-wrap items-center justify-between gap-4">
                <div class="flex items-center space-x-3.5">
                    <div class="p-3 rounded-2xl bg-amber-500/10 text-amber-500 border border-amber-500/20">
                        <i class="fa-solid fa-chart-line text-2xl"></i>
                    </div>
                    <div>
                        <div class="flex items-center space-x-2">
                            <span class="text-xs text-slate-400 font-semibold uppercase tracking-wider">ราคาทองคำแท่ง 96.5% (สมาคมค้าทองคำ)</span>
                            <span class="text-[10px] bg-emerald-950 text-emerald-400 border border-emerald-800/60 px-2 py-0.5 rounded-full font-mono">LIVE API</span>
                        </div>
                        <div class="text-xs text-slate-400 mt-0.5">อัปเดตล่าสุด: <span id="last-updated-time" class="text-slate-200 font-mono font-medium">16:15:00</span> (ครั้งที่ 4)</div>
                    </div>
                </div>

                <!-- Price Counters -->
                <div class="flex items-center space-x-6 sm:space-x-10">
                    <!-- Buy Price -->
                    <div>
                        <span class="text-xs text-slate-400 font-medium block">รับซื้อคืน (บาทละ)</span>
                        <span class="text-2xl sm:text-3xl font-extrabold font-mono text-emerald-400" id="gold-buy-price">43,850</span>
                        <span class="text-[10px] text-emerald-400 block font-medium mt-0.5"><i class="fa-solid fa-caret-up"></i> +150 (+0.34%)</span>
                    </div>
                    <div class="h-10 w-px bg-slate-800"></div>
                    <!-- Sell Price -->
                    <div>
                        <span class="text-xs text-slate-400 font-medium block">ขายออก (บาทละ)</span>
                        <span class="text-2xl sm:text-3xl font-extrabold font-mono text-amber-400" id="gold-sell-price">43,950</span>
                 
