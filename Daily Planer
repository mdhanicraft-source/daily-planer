<!DOCTYPE html>
<html lang="ml">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Plan & Finance</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #fafafa;
            color: #171717;
            -webkit-tap-highlight-color: transparent;
        }
        .app-card {
            background: #ffffff;
            border: 1px solid #f0f0f0;
            border-radius: 1rem;
            box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.03);
            transition: all 0.15s ease;
        }
        .app-card:hover {
            box-shadow: 0 4px 12px 0 rgba(0, 0, 0, 0.05);
        }
        .tab-btn {
            transition: all 0.2s ease;
            color: #737373;
        }
        .tab-btn.active {
            color: #171717;
            background-color: #ffffff;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
            font-weight: 600;
        }
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
    </style>
</head>
<body class="min-h-screen pb-20 antialiased selection:bg-neutral-200">

    <!-- MPIN LOCK OVERLAY -->
    <div id="mpin-screen" class="fixed inset-0 bg-neutral-950 z-50 flex flex-col items-center justify-center p-4 text-white">
        <div class="max-w-xs w-full text-center space-y-6">
            <div class="w-16 h-16 bg-neutral-800 rounded-2xl flex items-center justify-center mx-auto text-amber-400 shadow-xl border border-neutral-700">
                <i class="fa-solid fa-lock text-2xl"></i>
            </div>
            <div>
                <h2 class="text-lg font-bold tracking-tight" id="mpin-title">Enter MPIN</h2>
                <p class="text-xs text-neutral-400 mt-1" id="mpin-subtitle">സുരക്ഷയ്ക്കായി 4-അക്ക MPIN നൽകുക (Default: 1234)</p>
            </div>

            <!-- PIN Input Display -->
            <div class="flex justify-center gap-3 my-4">
                <div class="w-10 h-12 bg-neutral-900 border border-neutral-800 rounded-xl flex items-center justify-center text-xl font-bold" id="pin-box-1">•</div>
                <div class="w-10 h-12 bg-neutral-900 border border-neutral-800 rounded-xl flex items-center justify-center text-xl font-bold" id="pin-box-2">•</div>
                <div class="w-10 h-12 bg-neutral-900 border border-neutral-800 rounded-xl flex items-center justify-center text-xl font-bold" id="pin-box-3">•</div>
                <div class="w-10 h-12 bg-neutral-900 border border-neutral-800 rounded-xl flex items-center justify-center text-xl font-bold" id="pin-box-4">•</div>
            </div>

            <p id="mpin-error" class="text-xs text-rose-500 font-medium hidden">തെറ്റായ MPIN! വീണ്ടും ശ്രമിക്കുക.</p>

            <!-- Keypad -->
            <div class="grid grid-cols-3 gap-3 pt-2 max-w-[240px] mx-auto">
                <button onclick="pressPin('1')" class="h-12 bg-neutral-900 hover:bg-neutral-800 rounded-xl font-bold text-lg active:scale-95 transition-all">1</button>
                <button onclick="pressPin('2')" class="h-12 bg-neutral-900 hover:bg-neutral-800 rounded-xl font-bold text-lg active:scale-95 transition-all">2</button>
                <button onclick="pressPin('3')" class="h-12 bg-neutral-900 hover:bg-neutral-800 rounded-xl font-bold text-lg active:scale-95 transition-all">3</button>
                <button onclick="pressPin('4')" class="h-12 bg-neutral-900 hover:bg-neutral-800 rounded-xl font-bold text-lg active:scale-95 transition-all">4</button>
                <button onclick="pressPin('5')" class="h-12 bg-neutral-900 hover:bg-neutral-800 rounded-xl font-bold text-lg active:scale-95 transition-all">5</button>
                <button onclick="pressPin('6')" class="h-12 bg-neutral-900 hover:bg-neutral-800 rounded-xl font-bold text-lg active:scale-95 transition-all">6</button>
                <button onclick="pressPin('7')" class="h-12 bg-neutral-900 hover:bg-neutral-800 rounded-xl font-bold text-lg active:scale-95 transition-all">7</button>
                <button onclick="pressPin('8')" class="h-12 bg-neutral-900 hover:bg-neutral-800 rounded-xl font-bold text-lg active:scale-95 transition-all">8</button>
                <button onclick="pressPin('9')" class="h-12 bg-neutral-900 hover:bg-neutral-800 rounded-xl font-bold text-lg active:scale-95 transition-all">9</button>
                <button onclick="triggerPinReset()" class="h-12 text-xs font-semibold text-neutral-400 hover:text-white flex items-center justify-center">Reset</button>
                <button onclick="pressPin('0')" class="h-12 bg-neutral-900 hover:bg-neutral-800 rounded-xl font-bold text-lg active:scale-95 transition-all">0</button>
                <button onclick="clearPin()" class="h-12 bg-neutral-900 hover:bg-neutral-800 text-rose-400 rounded-xl font-bold text-sm active:scale-95 transition-all"><i class="fa-solid fa-backspace"></i></button>
            </div>
        </div>
    </div>

    <!-- Header -->
    <header class="bg-white/90 backdrop-blur-md border-b border-neutral-100 sticky top-0 z-30 px-4 py-3">
        <div class="max-w-xl mx-auto flex justify-between items-center">
            <div class="flex items-center gap-2.5">
                <div class="w-8 h-8 bg-neutral-900 text-white rounded-lg flex items-center justify-center text-xs font-semibold">
                    <i class="fa-solid fa-compass"></i>
                </div>
                <div>
                    <h1 class="text-xs font-bold text-neutral-900 tracking-tight" data-i18n="app_title">Plan & Finance</h1>
                    <p class="text-[10px] text-neutral-400 font-medium" id="current-date"></p>
                </div>
            </div>
            <div class="flex items-center gap-2">
                <!-- Lock App Button -->
                <button onclick="lockApp()" class="bg-neutral-100 hover:bg-neutral-200 p-1.5 rounded-lg text-neutral-700 transition-all text-xs" title="Lock App">
                    <i class="fa-solid fa-lock"></i>
                </button>
                <!-- Language Toggle Button -->
                <button onclick="toggleLanguage()" class="bg-neutral-100 hover:bg-neutral-200 px-2.5 py-1 rounded-lg text-[11px] font-bold text-neutral-700 transition-all flex items-center gap-1">
                    <i class="fa-solid fa-globe text-neutral-500"></i>
                    <span id="lang-label">EN</span>
                </button>
                <div class="bg-neutral-100 px-2.5 py-1 rounded-lg text-[11px] font-semibold text-neutral-700">
                    <span id="completion-stats">0/0</span>
                </div>
            </div>
        </div>
    </header>

    <main class="max-w-xl mx-auto px-4 mt-4">

        <!-- Navigation Tabs -->
        <div class="flex p-1 bg-neutral-100 rounded-xl mb-4 text-xs font-medium gap-1 no-scrollbar overflow-x-auto">
            <button id="tab-dashboard-btn" onclick="switchTab('dashboard')" class="tab-btn active flex-1 py-1.5 px-3 rounded-lg text-center flex items-center justify-center gap-1.5 whitespace-nowrap">
                <i class="fa-solid fa-chart-pie text-[11px]"></i> <span data-i18n="tab_dashboard">ഓവർവ്യൂ</span>
            </button>
            <button id="tab-report-btn" onclick="switchTab('report')" class="tab-btn flex-1 py-1.5 px-3 rounded-lg text-center flex items-center justify-center gap-1.5 whitespace-nowrap">
                <i class="fa-solid fa-calculator text-[11px]"></i> <span data-i18n="tab_report">റിപ്പോർട്ട്</span>
            </button>
            <button id="tab-routines-btn" onclick="switchTab('routines')" class="tab-btn flex-1 py-1.5 px-3 rounded-lg text-center flex items-center justify-center gap-1.5 whitespace-nowrap">
                <i class="fa-solid fa-rotate-right text-[11px]"></i> <span data-i18n="tab_routines">റൂട്ടീൻസ്</span>
            </button>
            <button id="tab-tasks-btn" onclick="switchTab('tasks')" class="tab-btn flex-1 py-1.5 px-3 rounded-lg text-center flex items-center justify-center gap-1.5 whitespace-nowrap">
                <i class="fa-solid fa-check text-[11px]"></i> <span data-i18n="tab_tasks">ടാസ്കുകൾ</span>
            </button>
            <button id="tab-finance-btn" onclick="switchTab('finance')" class="tab-btn flex-1 py-1.5 px-3 rounded-lg text-center flex items-center justify-center gap-1.5 whitespace-nowrap">
                <i class="fa-solid fa-arrow-left-right text-[11px]"></i> <span data-i18n="tab_finance">വരവ് / ചെലവ്</span>
            </button>
            <button id="tab-debts-btn" onclick="switchTab('debts')" class="tab-btn flex-1 py-1.5 px-3 rounded-lg text-center flex items-center justify-center gap-1.5 whitespace-nowrap">
                <i class="fa-solid fa-handshake text-[11px]"></i> <span data-i18n="tab_debts">കടങ്ങൾ</span>
            </button>
            <button id="tab-loans-btn" onclick="switchTab('loans')" class="tab-btn flex-1 py-1.5 px-3 rounded-lg text-center flex items-center justify-center gap-1.5 whitespace-nowrap">
                <i class="fa-solid fa-building-columns text-[11px]"></i> <span data-i18n="tab_loans">വായ്പകൾ</span>
            </button>
            <button id="tab-chitty-btn" onclick="switchTab('chitty')" class="tab-btn flex-1 py-1.5 px-3 rounded-lg text-center flex items-center justify-center gap-1.5 whitespace-nowrap">
                <i class="fa-solid fa-piggy-bank text-[11px]"></i> <span data-i18n="tab_chitty">ചിട്ടി</span>
            </button>
            <button id="tab-accounts-btn" onclick="switchTab('accounts')" class="tab-btn flex-1 py-1.5 px-3 rounded-lg text-center flex items-center justify-center gap-1.5 whitespace-nowrap">
                <i class="fa-solid fa-wallet text-[11px]"></i> <span data-i18n="tab_accounts">അക്കൗണ്ട്</span>
            </button>
            <button id="tab-goals-btn" onclick="switchTab('goals')" class="tab-btn flex-1 py-1.5 px-3 rounded-lg text-center flex items-center justify-center gap-1.5 whitespace-nowrap">
                <i class="fa-solid fa-bullseye text-[11px]"></i> <span data-i18n="tab_goals">ലക്ഷ്യങ്ങൾ</span>
            </button>
        </div>

        <!-- DASHBOARD OVERVIEW -->
        <div id="tab-dashboard" class="space-y-3">
            <div id="notification-banner" class="hidden bg-neutral-900 text-white p-3.5 rounded-xl flex items-center justify-between">
                <div class="flex items-center gap-2.5">
                    <i class="fa-solid fa-bell text-amber-400 text-sm"></i>
                    <div>
                        <span class="text-[9px] uppercase font-bold text-neutral-400 tracking-wider block" data-i18n="notif_reminder">Reminder</span>
                        <h4 class="text-xs font-medium" id="notif-title">Task Title</h4>
                    </div>
                </div>
                <button onclick="dismissNotification()" class="bg-neutral-800 hover:bg-neutral-700 text-white text-[11px] px-2.5 py-1 rounded-lg" data-i18n="dismiss">Dismiss</button>
            </div>

            <!-- Daily Target Banner on Dashboard -->
            <div class="bg-gradient-to-br from-neutral-900 to-neutral-800 text-white p-4 rounded-xl shadow-sm space-y-1">
                <span class="text-[10px] font-semibold text-neutral-400 uppercase tracking-wider block" data-i18n="dash_target_label">പ്രതിദിന മിനിമം വരുമാന ലക്ഷ്യം</span>
                <div class="flex items-baseline justify-between">
                    <h2 class="text-xl font-extrabold text-amber-400" id="dash-daily-target-val">₹0 / day</h2>
                    <button onclick="switchTab('report')" class="text-[11px] text-neutral-300 hover:text-white underline font-medium" data-i18n="view_breakdown">വിശദാംശങ്ങൾ ➔</button>
                </div>
            </div>

            <!-- Summary Cards -->
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-2">
                <div class="bg-white p-3 rounded-xl border border-neutral-100 shadow-sm">
                    <span class="text-[10px] font-medium text-neutral-400 block" data-i18n="card_balance">ആകെ ബാലൻസ്</span>
                    <h3 class="text-sm font-bold text-neutral-900 mt-0.5" id="dash-total-bal">₹0</h3>
                </div>
                <div class="bg-white p-3 rounded-xl border border-neutral-100 shadow-sm">
                    <span class="text-[10px] font-medium text-emerald-600 block" data-i18n="card_receivable">കിട്ടാനുള്ളത്</span>
                    <h3 class="text-sm font-bold text-emerald-700 mt-0.5" id="dash-total-rec">₹0</h3>
                </div>
                <div class="bg-white p-3 rounded-xl border border-neutral-100 shadow-sm">
                    <span class="text-[10px] font-medium text-rose-500 block" data-i18n="card_payable">കൊടുക്കാനുള്ളത്</span>
                    <h3 class="text-sm font-bold text-rose-600 mt-0.5" id="dash-total-pay">₹0</h3>
                </div>
                <div class="bg-white p-3 rounded-xl border border-neutral-100 shadow-sm">
                    <span class="text-[10px] font-medium text-neutral-500 block" data-i18n="card_progress">ഇന്നത്തെ പുരോഗതി</span>
                    <h3 class="text-sm font-bold text-neutral-800 mt-0.5" id="dash-task-prog">0/0</h3>
                </div>
            </div>

            <!-- Today's Daily Routines -->
            <div class="app-card p-3.5 space-y-2.5">
                <div class="flex justify-between items-center">
                    <h3 class="text-xs font-bold text-neutral-800 flex items-center gap-1.5">
                        <i class="fa-solid fa-rotate-right text-neutral-400"></i> <span data-i18n="routines_heading">ദിവസേനയുള്ള ശീലങ്ങൾ</span>
                    </h3>
                    <button onclick="switchTab('routines')" class="text-[11px] text-neutral-500 hover:text-neutral-900" data-i18n="more">കൂടുതൽ</button>
                </div>
                <div id="dash-today-routines" class="space-y-1.5"></div>
            </div>

            <!-- Today's Scheduled Tasks -->
            <div class="app-card p-3.5 space-y-2.5">
                <div class="flex justify-between items-center">
                    <h3 class="text-xs font-bold text-neutral-800 flex items-center gap-1.5">
                        <i class="fa-solid fa-calendar-check text-neutral-400"></i> <span data-i18n="today_tasks_heading">ഇന്നത്തെ ടാസ്കുകൾ</span>
                    </h3>
                    <button onclick="switchTab('tasks')" class="text-[11px] text-neutral-500 hover:text-neutral-900" data-i18n="view_all">എല്ലാം കാണുക</button>
                </div>
                <div id="dash-today-tasks" class="space-y-1.5"></div>
            </div>

            <!-- Goals Summary -->
            <div class="app-card p-3.5 space-y-2.5">
                <div class="flex justify-between items-center">
                    <h3 class="text-xs font-bold text-neutral-800 flex items-center gap-1.5">
                        <i class="fa-solid fa-bullseye text-neutral-400"></i> <span data-i18n="goals_heading">ലക്ഷ്യങ്ങൾ (Goals)</span>
                    </h3>
                    <button onclick="switchTab('goals')" class="text-[11px] text-neutral-500 hover:text-neutral-900" data-i18n="more">കൂടുതൽ</button>
                </div>
                <div id="dash-goals-summary" class="space-y-2"></div>
            </div>

            <!-- Debts Quick Action -->
            <div class="app-card p-3.5 space-y-2.5">
                <div class="flex justify-between items-center">
                    <h3 class="text-xs font-bold text-neutral-800 flex items-center gap-1.5">
                        <i class="fa-solid fa-hand-holding-dollar text-neutral-400"></i> <span data-i18n="payables_heading">നൽകാനുള്ള തുകകൾ</span>
                    </h3>
                    <button onclick="switchTab('debts')" class="text-[11px] text-neutral-500 hover:text-neutral-900" data-i18n="debts">കടങ്ങൾ</button>
                </div>
                <div id="dash-payables-list" class="space-y-1.5"></div>
            </div>
        </div>

        <!-- FINANCIAL REPORT & DAILY TARGET TAB -->
        <div id="tab-report" class="hidden space-y-3">
            <div class="app-card p-4 space-y-3">
                <div class="border-b border-neutral-100 pb-2">
                    <h3 class="text-xs font-bold text-neutral-900 flex items-center gap-1.5">
                        <i class="fa-solid fa-calculator text-neutral-500"></i> <span data-i18n="report_title">സാമ്പത്തിക വിശകലന റിപ്പോർട്ട്</span>
                    </h3>
                    <p class="text-[11px] text-neutral-500 mt-0.5" data-i18n="report_desc">നിങ്ങളുടെ പ്രതിമാസ അടവുകളും സാമ്പത്തിക ഭദ്രതയും കണക്കാക്കിയുള്ള റിപ്പോർട്ട്.</p>
                </div>

                <!-- Calculated Target Display -->
                <div class="bg-emerald-50 border border-emerald-100 rounded-xl p-3.5 text-emerald-950 space-y-1">
                    <span class="text-[10px] font-bold uppercase text-emerald-700 tracking-wide block" data-i18n="report_min_earning">പ്രതിദിനം സമ്പാദിക്കേണ്ട തുക</span>
                    <div class="text-2xl font-black text-emerald-800" id="rpt-daily-target">₹0 / day</div>
                    <p class="text-[11px] text-emerald-700 leading-snug" id="rpt-target-explain">കണക്കുകൾ വിശകലനം ചെയ്യുന്നു...</p>
                </div>

                <!-- Monthly Commitments Breakdown -->
                <div class="space-y-2">
                    <h4 class="text-xs font-bold text-neutral-800" data-i18n="monthly_obligations">മാസാന്ത സ്ഥിര അടവുകൾ (Monthly Commitments)</h4>
                    <div class="bg-neutral-50 p-3 rounded-xl border border-neutral-100 text-xs space-y-1.5">
                        <div class="flex justify-between text-neutral-600">
                            <span data-i18n="rep_emis">മാസാന്ത ലോൺ EMI കൾ:</span>
                            <span class="font-bold text-neutral-900" id="rpt-loan-emis">₹0</span>
                        </div>
                        <div class="flex justify-between text-neutral-600">
                            <span data-i18n="rep_chitty">മാസാന്ത ചിട്ടി അടവുകൾ:</span>
                            <span class="font-bold text-neutral-900" id="rpt-chitty-inst">₹0</span>
                        </div>
                        <div class="flex justify-between text-neutral-600">
                            <span data-i18n="rep_debts">കൊടുക്കാനുള്ള ആകെ കടങ്ങൾ:</span>
                            <span class="font-bold text-rose-600" id="rpt-total-debts">₹0</span>
                        </div>
                        <div class="pt-1.5 border-t border-neutral-200 flex justify-between font-bold text-neutral-900">
                            <span data-i18n="rep_total_monthly">പ്രതിമാസ ബാധ്യത തുക:</span>
                            <span id="rpt-total-monthly-req">₹0</span>
                        </div>
                    </div>
                </div>

                <!-- Net Worth Summary -->
                <div class="space-y-2">
                    <h4 class="text-xs font-bold text-neutral-800" data-i18n="net_financial_status">നിലവിലെ സാമ്പത്തിക ഭദ്രത (Net Balance Position)</h4>
                    <div class="bg-neutral-50 p-3 rounded-xl border border-neutral-100 text-xs space-y-1.5">
                        <div class="flex justify-between text-neutral-600">
                            <span data-i18n="rep_total_cash">ലഭ്യമായ ആകെ ബാലൻസ്:</span>
                            <span class="font-bold text-neutral-900" id="rpt-total-cash">₹0</span>
                        </div>
                        <div class="flex justify-between text-neutral-600">
                            <span data-i18n="rep_receivable">മറ്റുള്ളവരിൽ നിന്ന് കിട്ടാനുള്ളത്:</span>
                            <span class="font-bold text-emerald-600" id="rpt-receivables">₹0</span>
                        </div>
                        <div class="flex justify-between text-neutral-600">
                            <span data-i18n="rep_payable">കൊടുക്കാനുള്ള ഉത്തരവാദിത്തം:</span>
                            <span class="font-bold text-rose-600" id="rpt-payables">₹0</span>
                        </div>
                        <div class="pt-1.5 border-t border-neutral-200 flex justify-between font-bold text-neutral-900 text-sm">
                            <span data-i18n="rep_net_worth">യഥാർത്ഥ സാമ്പത്തിക സ്ഥിതി:</span>
                            <span id="rpt-net-worth">₹0</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- DAILY ROUTINES TAB -->
        <div id="tab-routines" class="hidden space-y-3">
            <div class="app-card p-3.5">
                <form id="routine-form" onsubmit="addRoutine(event)" class="space-y-2.5">
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
                        <input type="text" id="routine-title" required placeholder="ശീലം (ഉദാ: വാക്കിംഗ്)" class="sm:col-span-2 w-full px-3 py-2 text-xs rounded-lg border border-neutral-200 focus:outline-none focus:border-neutral-400">
                        <input type="time" id="routine-time" required class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200 focus:outline-none focus:border-neutral-400">
                    </div>
                    <button type="submit" class="w-full bg-neutral-900 hover:bg-neutral-800 text-white text-xs font-medium py-2 rounded-lg" data-i18n="btn_add_routine">റൂട്ടീൻ ചേർക്കുക</button>
                </form>
            </div>
            <div class="flex justify-between items-center px-1">
                <h4 class="text-xs font-bold text-neutral-600" data-i18n="tab_routines">റൂട്ടീനുകൾ</h4>
                <button onclick="resetRoutinesForToday()" class="text-[11px] text-neutral-500 hover:text-neutral-900" data-i18n="reset_progress">Reset Progress</button>
            </div>
            <div id="routines-list" class="space-y-1.5"></div>
        </div>

        <!-- ONE-TIME TASKS TAB -->
        <div id="tab-tasks" class="hidden space-y-3">
            <div class="app-card p-3.5">
                <form id="task-form" onsubmit="addTask(event)" class="space-y-2.5">
                    <input type="text" id="task-title" required placeholder="ചെയ്യാനുള്ള കാര്യം..." class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200 focus:outline-none focus:border-neutral-400">
                    <div class="grid grid-cols-2 gap-2">
                        <input type="date" id="task-date" required class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200 focus:outline-none focus:border-neutral-400">
                        <input type="time" id="task-time" required class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200 focus:outline-none focus:border-neutral-400">
                    </div>
                    <button type="submit" class="w-full bg-neutral-900 hover:bg-neutral-800 text-white text-xs font-medium py-2 rounded-lg" data-i18n="btn_add_task">ടാസ്ക് ചേർക്കുക</button>
                </form>
            </div>
            <div id="tasks-list" class="space-y-1.5"></div>
        </div>

        <!-- FINANCE TAB -->
        <div id="tab-finance" class="hidden space-y-3">
            <div class="app-card p-3.5">
                <form id="finance-form" onsubmit="addTransaction(event)" class="space-y-2.5">
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-2">
                        <input type="text" id="finance-desc" required placeholder="വിവരണം (ഉദാ: ചായ, ശമ്പളം)" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200 focus:outline-none">
                        <input type="number" id="finance-amount" required min="1" placeholder="തുക (₹)" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200 focus:outline-none">
                    </div>
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
                        <select id="finance-type" class="w-full px-2.5 py-2 text-xs rounded-lg border border-neutral-200 bg-white">
                            <option value="expense">🔴 ചെലവ് (Expense)</option>
                            <option value="income">🟢 വരവ് (Income)</option>
                        </select>
                        <select id="finance-account" class="w-full px-2.5 py-2 text-xs rounded-lg border border-neutral-200 bg-white">
                            <option value="cash">💵 Cash</option>
                            <option value="federal">🏦 Federal Bank</option>
                            <option value="sbi">🏛️ SBI Bank</option>
                        </select>
                        <input type="date" id="finance-date" required class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                    </div>
                    <button type="submit" class="w-full bg-neutral-900 hover:bg-neutral-800 text-white text-xs font-medium py-2 rounded-lg" data-i18n="btn_save">സേവ് ചെയ്യുക</button>
                </form>
            </div>
            <div id="finance-list" class="space-y-1.5"></div>
        </div>

        <!-- DEBTS TAB -->
        <div id="tab-debts" class="hidden space-y-3">
            <div class="grid grid-cols-2 gap-2">
                <div class="bg-emerald-50/50 border border-emerald-100 p-3 rounded-xl">
                    <span class="text-[10px] text-emerald-600 font-semibold block" data-i18n="card_receivable">കിട്ടാനുള്ളത്</span>
                    <span class="text-base font-bold text-emerald-800 mt-0.5 block" id="total-receivable">₹0</span>
                </div>
                <div class="bg-rose-50/50 border border-rose-100 p-3 rounded-xl">
                    <span class="text-[10px] text-rose-600 font-semibold block" data-i18n="card_payable">കൊടുക്കാനുള്ളത്</span>
                    <span class="text-base font-bold text-rose-800 mt-0.5 block" id="total-payable">₹0</span>
                </div>
            </div>

            <div class="app-card p-3.5">
                <form id="debt-form" onsubmit="addDebt(event)" class="space-y-2.5">
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-2">
                        <input type="text" id="debt-person" required placeholder="ആളുടെ പേര്" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        <input type="number" id="debt-amount" required min="1" placeholder="തുക (₹)" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                    </div>
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
                        <select id="debt-type" class="w-full px-2.5 py-2 text-xs rounded-lg border border-neutral-200 bg-white">
                            <option value="receivable">🟢 കിട്ടാനുള്ളത്</option>
                            <option value="payable">🔴 കൊടുക്കാനുള്ളത്</option>
                        </select>
                        <input type="date" id="debt-date" required class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        <input type="text" id="debt-desc" placeholder="കുറിപ്പ്" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                    </div>
                    <button type="submit" class="w-full bg-neutral-900 hover:bg-neutral-800 text-white text-xs font-medium py-2 rounded-lg" data-i18n="btn_record">രേഖപ്പെടുത്തുക</button>
                </form>
            </div>
            <div id="debts-list" class="space-y-1.5"></div>
        </div>

        <!-- LOANS TAB -->
        <div id="tab-loans" class="hidden space-y-3">
            <div class="app-card p-3.5">
                <form id="loan-form" onsubmit="addLoan(event)" class="space-y-2.5">
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-2">
                        <input type="text" id="loan-title" required placeholder="ലോൺ സ്ഥാപനം / ബാങ്ക്" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        <input type="number" id="loan-principal" required min="1" placeholder="ആകെ വായ്പാ തുക (₹)" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                    </div>
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
                        <input type="number" id="loan-emi" required min="1" placeholder="മാസാന്ത EMI (₹)" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        <input type="number" id="loan-dueday" required min="1" max="31" placeholder="തീയതി (1-31)" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        <select id="loan-account" class="w-full px-2.5 py-2 text-xs rounded-lg border border-neutral-200 bg-white">
                            <option value="federal">🏦 Federal Bank</option>
                            <option value="sbi">🏛️ SBI Bank</option>
                            <option value="cash">💵 Cash</option>
                        </select>
                    </div>
                    <button type="submit" class="w-full bg-neutral-900 hover:bg-neutral-800 text-white text-xs font-medium py-2 rounded-lg" data-i18n="btn_add_emi">EMI ചേർക്കുക</button>
                </form>
            </div>
            <div id="loans-list" class="space-y-1.5"></div>
        </div>

        <!-- CHITTY TAB -->
        <div id="tab-chitty" class="hidden space-y-3">
            <div class="app-card p-3.5">
                <form id="chitty-form" onsubmit="addChitty(event)" class="space-y-2.5">
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-2">
                        <input type="text" id="chitty-name" required placeholder="ചിട്ടിയുടെ പേര് (KSFE / മറ്റുള്ളവ)" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        <input type="number" id="chitty-total" required min="1" placeholder="ആകെ തുക (₹)" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                    </div>
                    <div class="grid grid-cols-1 sm:grid-cols-4 gap-2">
                        <input type="number" id="chitty-installment" required min="1" placeholder="പ്രതിമാസം (₹)" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        <input type="number" id="chitty-months" required min="1" placeholder="മാസങ്ങൾ" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        <input type="number" id="chitty-dueday" required min="1" max="31" placeholder="തീയതി" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        <input type="number" id="chitty-paid-count" min="0" placeholder="അടച്ച മാസങ്ങൾ" value="0" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                    </div>
                    <button type="submit" class="w-full bg-neutral-900 hover:bg-neutral-800 text-white text-xs font-medium py-2 rounded-lg" data-i18n="btn_add_chitty">ചിട്ടി ചേർക്കുക</button>
                </form>
            </div>
            <div id="chitty-list" class="space-y-1.5"></div>
        </div>

        <!-- ACCOUNTS TAB -->
        <div id="tab-accounts" class="hidden space-y-3">
            <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
                <div class="bg-white p-3 rounded-xl border border-neutral-100 shadow-sm">
                    <span class="text-[10px] font-medium text-neutral-400 block">Cash Balance</span>
                    <h3 class="text-base font-bold text-neutral-800 mt-0.5" id="acc-cash-val">₹0</h3>
                </div>
                <div class="bg-white p-3 rounded-xl border border-neutral-100 shadow-sm">
                    <span class="text-[10px] font-medium text-neutral-400 block">Federal Bank</span>
                    <h3 class="text-base font-bold text-neutral-800 mt-0.5" id="acc-federal-val">₹0</h3>
                </div>
                <div class="bg-white p-3 rounded-xl border border-neutral-100 shadow-sm">
                    <span class="text-[10px] font-medium text-neutral-400 block">SBI Bank</span>
                    <h3 class="text-base font-bold text-neutral-800 mt-0.5" id="acc-sbi-val">₹0</h3>
                </div>
            </div>

            <div class="app-card p-3.5">
                <h4 class="text-xs font-bold text-neutral-800 mb-2" data-i18n="adjust_balance">അക്കൗണ്ട് ബാലൻസ് ക്രമീകരിക്കുക</h4>
                <form id="balance-update-form" onsubmit="updateBalances(event)" class="space-y-2.5">
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
                        <div>
                            <label class="block text-[10px] font-medium text-neutral-400 mb-1">Cash (₹)</label>
                            <input type="number" id="init-cash" required placeholder="0" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        </div>
                        <div>
                            <label class="block text-[10px] font-medium text-neutral-400 mb-1">Federal (₹)</label>
                            <input type="number" id="init-federal" required placeholder="0" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        </div>
                        <div>
                            <label class="block text-[10px] font-medium text-neutral-400 mb-1">SBI (₹)</label>
                            <input type="number" id="init-sbi" required placeholder="0" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        </div>
                    </div>
                    <button type="submit" class="w-full bg-neutral-900 hover:bg-neutral-800 text-white text-xs font-medium py-2 rounded-lg" data-i18n="btn_update">അപ്ഡേറ്റ് ചെയ്യുക</button>
                </form>
            </div>
        </div>

        <!-- GOALS TAB -->
        <div id="tab-goals" class="hidden space-y-3">
            <div class="app-card p-3.5">
                <form id="goal-form" onsubmit="addGoal(event)" class="space-y-2.5">
                    <input type="text" id="goal-title" required placeholder="ലക്ഷ്യം (ഉദാ: പുതിയ ബൈക്ക്)" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-2">
                        <input type="number" id="goal-target" required min="1" placeholder="ലക്ഷ്യ തുക (₹)" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        <input type="number" id="goal-saved" min="0" placeholder="സേവ് ചെയ്തത് (₹)" value="0" class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                        <input type="date" id="goal-date" required class="w-full px-3 py-2 text-xs rounded-lg border border-neutral-200">
                    </div>
                    <button type="submit" class="w-full bg-neutral-900 hover:bg-neutral-800 text-white text-xs font-medium py-2 rounded-lg" data-i18n="btn_add_goal">ലക്ഷ്യം ക്രിയേറ്റ് ചെയ്യുക</button>
                </form>
            </div>
            <div id="goals-list" class="space-y-1.5"></div>
        </div>

    </main>

    <!-- MPIN RESET MODAL -->
    <div id="pin-reset-modal" class="fixed inset-0 bg-neutral-950/80 backdrop-blur-sm z-[60] hidden flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl p-5 max-w-xs w-full text-neutral-900 space-y-4">
            <h3 class="text-sm font-bold text-center">Change MPIN</h3>
            <div class="space-y-2 text-xs">
                <div>
                    <label class="block text-[10px] text-neutral-500 font-semibold mb-1">Current MPIN</label>
                    <input type="password" id="cur-pin-input" maxlength="4" placeholder="1234" class="w-full px-3 py-2 rounded-lg border border-neutral-200 font-bold text-center">
                </div>
                <div>
                    <label class="block text-[10px] text-neutral-500 font-semibold mb-1">New 4-Digit MPIN</label>
                    <input type="password" id="new-pin-input" maxlength="4" placeholder="••••" class="w-full px-3 py-2 rounded-lg border border-neutral-200 font-bold text-center">
                </div>
            </div>
            <div class="flex gap-2">
                <button onclick="closePinResetModal()" class="flex-1 py-2 bg-neutral-100 hover:bg-neutral-200 rounded-lg text-xs font-bold text-neutral-600">Cancel</button>
                <button onclick="submitPinReset()" class="flex-1 py-2 bg-neutral-900 hover:bg-neutral-800 rounded-lg text-xs font-bold text-white">Save PIN</button>
            </div>
        </div>
    </div>

    <div id="toast" class="fixed bottom-5 left-1/2 -translate-x-1/2 bg-neutral-900 text-white px-3.5 py-1.5 rounded-xl shadow-lg flex items-center gap-2 transition-all duration-200 opacity-0 pointer-events-none z-50 text-xs font-medium">
        <i class="fa-solid fa-circle-check text-emerald-400"></i>
        <span id="toast-message"></span>
    </div>

    <script>
        // GLOBAL STATE & MULTI-LANGUAGE
        window.currentLang = 'ml'; // Default Malayalam
        window.enteredPin = '';
        window.storedPin = '1234'; // Default PIN

        const i18n = {
            ml: {
                app_title: 'Plan & Finance',
                tab_dashboard: 'ഓവർവ്യൂ',
                tab_report: 'റിപ്പോർട്ട്',
                tab_routines: 'റൂട്ടീൻസ്',
                tab_tasks: 'ടാസ്കുകൾ',
                tab_finance: 'വരവ് / ചെലവ്',
                tab_debts: 'കടങ്ങൾ',
                tab_loans: 'വായ്പകൾ',
                tab_chitty: 'ചിട്ടി',
                tab_accounts: 'അക്കൗണ്ട്',
                tab_goals: 'ലക്ഷ്യങ്ങൾ',
                notif_reminder: 'Reminder',
                dismiss: 'Dismiss',
                dash_target_label: 'പ്രതിദിന മിനിമം വരുമാന ലക്ഷ്യം',
                view_breakdown: 'വിശദാംശങ്ങൾ ➔',
                card_balance: 'ആകെ ബാലൻസ്',
                card_receivable: 'കിട്ടാനുള്ളത്',
                card_payable: 'കൊടുക്കാനുള്ളത്',
                card_progress: 'ഇന്നത്തെ പുരോഗതി',
                routines_heading: 'ദിവസേനയുള്ള ശീലങ്ങൾ',
                today_tasks_heading: 'ഇന്നത്തെ ടാസ്കുകൾ',
                goals_heading: 'ലക്ഷ്യങ്ങൾ (Goals)',
                payables_heading: 'നൽകാനുള്ള തുകകൾ',
                more: 'കൂടുതൽ',
                view_all: 'എല്ലാം കാണുക',
                debts: 'കടങ്ങൾ',
                report_title: 'സാമ്പത്തിക വിശകലന റിപ്പോർട്ട്',
                report_desc: 'നിങ്ങളുടെ പ്രതിമാസ അടവുകളും സാമ്പത്തിക ഭദ്രതയും കണക്കാക്കിയുള്ള റിപ്പോർട്ട്.',
                report_min_earning: 'പ്രതിദിനം സമ്പാദിക്കേണ്ട തുക',
                monthly_obligations: 'മാസാന്ത സ്ഥിര അടവുകൾ (Monthly Commitments)',
                rep_emis: 'മാസാന്ത ലോൺ EMI കൾ:',
                rep_chitty: 'മാസാന്ത ചിട്ടി അടവുകൾ:',
                rep_debts: 'കൊടുക്കാനുള്ള ആകെ കടങ്ങൾ:',
                rep_total_monthly: 'പ്രതിമാസ ബാധ്യത തുക:',
                net_financial_status: 'നിലവിലെ സാമ്പത്തിക ഭദ്രത (Net Balance Position)',
                rep_total_cash: 'ലഭ്യമായ ആകെ ബാലൻസ്:',
                rep_receivable: 'മറ്റുള്ളവരിൽ നിന്ന് കിട്ടാനുള്ളത്:',
                rep_payable: 'കൊടുക്കാനുള്ള ഉത്തരവാദിത്തം:',
                rep_net_worth: 'യഥാർത്ഥ സാമ്പത്തിക സ്ഥിതി:',
                reset_progress: 'Reset Progress',
                adjust_balance: 'അക്കൗണ്ട് ബാലൻസ് ക്രമീകരിക്കുക',
                btn_add_routine: 'റൂട്ടീൻ ചേർക്കുക',
                btn_add_task: 'ടാസ്ക് ചേർക്കുക',
                btn_save: 'സേവ് ചെയ്യുക',
                btn_record: 'രേഖപ്പെടുത്തുക',
                btn_add_emi: 'EMI ചേർക്കുക',
                btn_add_chitty: 'ചിട്ടി ചേർക്കുക',
                btn_update: 'അപ്ഡേറ്റ് ചെയ്യുക',
                btn_add_goal: 'ലക്ഷ്യം ക്രിയേറ്റ് ചെയ്യുക',
                pay_now: 'പണം അടയ്ക്കുക'
            },
            en: {
                app_title: 'Plan & Finance',
                tab_dashboard: 'Overview',
                tab_report: 'Report',
                tab_routines: 'Routines',
                tab_tasks: 'Tasks',
                tab_finance: 'Income/Expense',
                tab_debts: 'Debts',
                tab_loans: 'Loans',
                tab_chitty: 'Chit Funds',
                tab_accounts: 'Accounts',
                tab_goals: 'Goals',
                notif_reminder: 'Reminder',
                dismiss: 'Dismiss',
                dash_target_label: 'DAILY MINIMUM EARNING TARGET',
                view_breakdown: 'Breakdown ➔',
                card_balance: 'Total Balance',
                card_receivable: 'Receivable',
                card_payable: 'Payable',
                card_progress: 'Today Progress',
                routines_heading: 'Daily Routines',
                today_tasks_heading: "Today's Tasks",
                goals_heading: 'Savings Goals',
                payables_heading: 'Pending Payables',
                more: 'More',
                view_all: 'View All',
                debts: 'Debts',
                report_title: 'Financial Analysis Report',
                report_desc: 'Comprehensive report based on your monthly EMIs, debts and savings targets.',
                report_min_earning: 'Daily Minimum Required Earnings',
                monthly_obligations: 'Monthly Fixed Commitments',
                rep_emis: 'Monthly Loan EMIs:',
                rep_chitty: 'Monthly Chit Payments:',
                rep_debts: 'Total Pending Debts:',
                rep_total_monthly: 'Total Monthly Obligation:',
                net_financial_status: 'Net Balance Position',
                rep_total_cash: 'Total Cash Available:',
                rep_receivable: 'Receivables:',
                rep_payable: 'Payables:',
                rep_net_worth: 'Net Worth:',
                reset_progress: 'Reset Progress',
                adjust_balance: 'Adjust Account Balances',
                btn_add_routine: 'Add Routine',
                btn_add_task: 'Add Task',
                btn_save: 'Save Record',
                btn_record: 'Record Debt',
                btn_add_emi: 'Add EMI',
                btn_add_chitty: 'Add Chit Fund',
                btn_update: 'Update Balances',
                btn_add_goal: 'Create Goal',
                pay_now: 'Pay Debt'
            }
        };

        window.tasks = [];
        window.routines = [
            { id: 101, title: 'Morning Exercise / Yoga', time: '06:30', completed: false },
            { id: 102, title: 'Read Book / Study', time: '21:00', completed: false }
        ];
        window.transactions = [];
        window.debts = [];
        window.loans = [];
        window.chitty = [];
        window.goals = [];
        window.accountBalances = { cash: 0, federal: 0, sbi: 0 };

        // MPIN FUNCTIONALITY
        function pressPin(num) {
            if (window.enteredPin.length < 4) {
                window.enteredPin += num;
                updatePinUI();
                if (window.enteredPin.length === 4) {
                    setTimeout(verifyPin, 150);
                }
            }
        }

        function clearPin() {
            window.enteredPin = window.enteredPin.slice(0, -1);
            updatePinUI();
            document.getElementById('mpin-error').classList.add('hidden');
        }

        function updatePinUI() {
            for (let i = 1; i <= 4; i++) {
                const box = document.getElementById(`pin-box-${i}`);
                if (i <= window.enteredPin.length) {
                    box.innerText = '•';
                    box.classList.add('border-amber-400', 'text-amber-400');
                } else {
                    box.innerText = '•';
                    box.classList.remove('border-amber-400', 'text-amber-400');
                }
            }
        }

        function verifyPin() {
            if (window.enteredPin === window.storedPin) {
                document.getElementById('mpin-screen').classList.add('hidden');
                window.enteredPin = '';
                updatePinUI();
                renderAll();
            } else {
                document.getElementById('mpin-error').classList.remove('hidden');
                window.enteredPin = '';
                updatePinUI();
            }
        }

        window.lockApp = function() {
            window.enteredPin = '';
            updatePinUI();
            document.getElementById('mpin-error').classList.add('hidden');
            document.getElementById('mpin-screen').classList.remove('hidden');
        };

        window.triggerPinReset = function() {
            document.getElementById('cur-pin-input').value = '';
            document.getElementById('new-pin-input').value = '';
            document.getElementById('pin-reset-modal').classList.remove('hidden');
        };

        window.closePinResetModal = function() {
            document.getElementById('pin-reset-modal').classList.add('hidden');
        };

        window.submitPinReset = function() {
            const cur = document.getElementById('cur-pin-input').value;
            const next = document.getElementById('new-pin-input').value;

            if (cur !== window.storedPin) {
                alert("Incorrect Current MPIN!");
                return;
            }

            if (!next || next.length !== 4 || isNaN(next)) {
                alert("Please enter a valid 4-digit numeric PIN!");
                return;
            }

            window.storedPin = next;
            window.saveState();
            closePinResetModal();
            showToast("MPIN Updated Successfully!");
        };

        // LANGUAGE TOGGLE FUNCTION
        window.toggleLanguage = function() {
            window.currentLang = window.currentLang === 'ml' ? 'en' : 'ml';
            document.getElementById('lang-label').innerText = window.currentLang === 'ml' ? 'EN' : 'ML';
            applyLanguage();
            renderAll();
        };

        function applyLanguage() {
            const langData = i18n[window.currentLang];
            document.querySelectorAll('[data-i18n]').forEach(el => {
                const key = el.getAttribute('data-i18n');
                if(langData[key]) {
                    el.innerText = langData[key];
                }
            });
        }

        // STORAGE LOGIC
        window.saveState = function() {
            const data = {
                tasks: window.tasks,
                routines: window.routines,
                transactions: window.transactions,
                debts: window.debts,
                loans: window.loans,
                chitty: window.chitty,
                goals: window.goals,
                accountBalances: window.accountBalances,
                lang: window.currentLang,
                pin: window.storedPin
            };
            try {
                localStorage.setItem('pfm_app_state', JSON.stringify(data));
            } catch(e) {
                console.error('Storage Error:', e);
            }
        };

        window.loadState = function() {
            try {
                const stored = localStorage.getItem('pfm_app_state');
                if (stored) {
                    const parsed = JSON.parse(stored);
                    window.tasks = parsed.tasks || [];
                    window.routines = parsed.routines || window.routines;
                    window.transactions = parsed.transactions || [];
                    window.debts = parsed.debts || [];
                    window.loans = parsed.loans || [];
                    window.chitty = parsed.chitty || [];
                    window.goals = parsed.goals || [];
                    window.accountBalances = parsed.accountBalances || { cash: 0, federal: 0, sbi: 0 };
                    window.currentLang = parsed.lang || 'ml';
                    window.storedPin = parsed.pin || '1234';
                    document.getElementById('lang-label').innerText = window.currentLang === 'ml' ? 'EN' : 'ML';
                }
            } catch(e) {
                console.error('Loading Error:', e);
            }
        };

        window.switchTab = function(tabId) {
            const tabs = ['dashboard', 'report', 'routines', 'tasks', 'finance', 'debts', 'loans', 'chitty', 'accounts', 'goals'];
            tabs.forEach(t => {
                const el = document.getElementById(`tab-${t}`);
                const btn = document.getElementById(`tab-${t}-btn`);
                if (el) el.classList.add('hidden');
                if (btn) btn.classList.remove('active');
            });

            const activeEl = document.getElementById(`tab-${tabId}`);
            const activeBtn = document.getElementById(`tab-${tabId}-btn`);
            if (activeEl) activeEl.classList.remove('hidden');
            if (activeBtn) activeBtn.classList.add('active');
        };

        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toast-message').innerText = msg;
            toast.classList.remove('opacity-0', 'pointer-events-none');
            setTimeout(() => toast.classList.add('opacity-0', 'pointer-events-none'), 2500);
        }

        // RENDER FUNCTIONS
        window.renderAll = function() {
            renderReport();
            renderDashboard();
            renderRoutines();
            renderTasks();
            renderFinance();
            renderDebts();
            renderLoans();
            renderChitty();
            renderAccounts();
            renderGoals();
        };

        function renderReport() {
            let monthlyLoans = 0;
            window.loans.forEach(l => monthlyLoans += (l.emi || 0));

            let monthlyChits = 0;
            window.chitty.forEach(c => monthlyChits += (c.installment || 0));

            let totalDebtsPayable = 0;
            let totalDebtsReceivable = 0;
            window.debts.forEach(d => {
                if(d.type === 'payable') totalDebtsPayable += d.amount;
                else if(d.type === 'receivable') totalDebtsReceivable += d.amount;
            });

            const totalMonthlyObligation = monthlyLoans + monthlyChits + (totalDebtsPayable / 2);
            const dailyTarget = Math.ceil(totalMonthlyObligation / 30);

            document.getElementById('rpt-daily-target').innerText = `₹${dailyTarget.toLocaleString('en-IN')} / ${window.currentLang === 'ml' ? 'ദിവസം' : 'day'}`;
            document.getElementById('dash-daily-target-val').innerText = `₹${dailyTarget.toLocaleString('en-IN')} / ${window.currentLang === 'ml' ? 'ദിവസം' : 'day'}`;

            document.getElementById('rpt-loan-emis').innerText = `₹${monthlyLoans.toLocaleString('en-IN')}`;
            document.getElementById('rpt-chitty-inst').innerText = `₹${monthlyChits.toLocaleString('en-IN')}`;
            document.getElementById('rpt-total-debts').innerText = `₹${totalDebtsPayable.toLocaleString('en-IN')}`;
            document.getElementById('rpt-total-monthly-req').innerText = `₹${Math.round(totalMonthlyObligation).toLocaleString('en-IN')}`;

            const totalCash = window.accountBalances.cash + window.accountBalances.federal + window.accountBalances.sbi;
            const netWorth = (totalCash + totalDebtsReceivable) - totalDebtsPayable;

            document.getElementById('rpt-total-cash').innerText = `₹${totalCash.toLocaleString('en-IN')}`;
            document.getElementById('rpt-receivables').innerText = `₹${totalDebtsReceivable.toLocaleString('en-IN')}`;
            document.getElementById('rpt-payables').innerText = `₹${totalDebtsPayable.toLocaleString('en-IN')}`;
            
            const netWorthEl = document.getElementById('rpt-net-worth');
            netWorthEl.innerText = `₹${netWorth.toLocaleString('en-IN')}`;
            netWorthEl.className = netWorth >= 0 ? 'font-bold text-emerald-700 text-sm' : 'font-bold text-rose-600 text-sm';

            const explanationEl = document.getElementById('rpt-target-explain');
            if(window.currentLang === 'ml') {
                explanationEl.innerText = `മാസാന്ത ലോൺ EMI (₹${monthlyLoans}), ചിട്ടി (₹${monthlyChits}), കുടിശ്ശികകൾ എന്നിവ കണക്കിലെടുക്കുമ്പോൾ ദിവസം കുറഞ്ഞത് ₹${dailyTarget} വീതം സമ്പാദിക്കേണ്ടതുണ്ട്.`;
            } else {
                explanationEl.innerText = `To cover your monthly EMIs (₹${monthlyLoans}), Chits (₹${monthlyChits}), and pending payables, you need to earn at least ₹${dailyTarget} daily.`;
            }
        }

        function renderDashboard() {
            const totalBal = window.accountBalances.cash + window.accountBalances.federal + window.accountBalances.sbi;
            document.getElementById('dash-total-bal').innerText = `₹${totalBal.toLocaleString('en-IN')}`;

            let rec = 0, pay = 0;
            window.debts.forEach(d => d.type === 'receivable' ? rec += d.amount : pay += d.amount);
            document.getElementById('dash-total-rec').innerText = `₹${rec.toLocaleString('en-IN')}`;
            document.getElementById('dash-total-pay').innerText = `₹${pay.toLocaleString('en-IN')}`;

            const todayStr = new Date().toISOString().split('T')[0];
            const todayTasks = window.tasks.filter(t => t.date === todayStr);
            const doneTasks = todayTasks.filter(t => t.completed).length;
            const doneRoutines = window.routines.filter(r => r.completed).length;
            const totalItemsToday = todayTasks.length + window.routines.length;
            const doneTotalToday = doneTasks + doneRoutines;

            document.getElementById('completion-stats').innerText = `${doneTotalToday}/${totalItemsToday}`;
            document.getElementById('dash-task-prog').innerText = `${doneTotalToday}/${totalItemsToday}`;

            const dashRoutines = document.getElementById('dash-today-routines');
            dashRoutines.innerHTML = '';
            if(!window.routines.length) {
                dashRoutines.innerHTML = `<p class="text-neutral-400 text-xs py-2 text-center">${window.currentLang === 'ml' ? 'ദിവസേനയുള്ള റൂട്ടീനുകൾ ഒന്നും നൽകിയിട്ടില്ല.' : 'No routines configured.'}</p>`;
            } else {
                window.routines.forEach(r => {
                    const row = document.createElement('div');
                    row.className = 'flex items-center justify-between p-2.5 rounded-xl bg-neutral-50 border border-neutral-100 text-xs';
                    row.innerHTML = `
                        <div class="flex items-center gap-2.5">
                            <input type="checkbox" ${r.completed ? 'checked' : ''} onchange="toggleRoutine(${r.id})" class="rounded border-neutral-300">
                            <div>
                                <span class="font-semibold text-neutral-800 ${r.completed ? 'line-through opacity-50' : ''}">${r.title}</span>
                                <span class="block text-[10px] text-neutral-400">${r.time}</span>
                            </div>
                        </div>
                        <span class="text-[10px] font-bold ${r.completed ? 'text-emerald-600' : 'text-neutral-400'}">${r.completed ? 'Done' : 'Pending'}</span>
                    `;
                    dashRoutines.appendChild(row);
                });
            }

            const dashTasks = document.getElementById('dash-today-tasks');
            dashTasks.innerHTML = '';
            if(!todayTasks.length) {
                dashTasks.innerHTML = `<p class="text-neutral-400 text-xs py-2 text-center">${window.currentLang === 'ml' ? 'ഇന്ന് പ്രത്യേക വൺ-ടൈം ടാസ്കുകൾ ഒന്നുമില്ല!' : 'No tasks scheduled for today.'}</p>`;
            } else {
                todayTasks.forEach(t => {
                    const row = document.createElement('div');
                    row.className = 'flex items-center justify-between p-2.5 rounded-xl bg-neutral-50 border border-neutral-100 text-xs';
                    row.innerHTML = `
                        <div class="flex items-center gap-2.5">
                            <input type="checkbox" ${t.completed ? 'checked' : ''} onchange="toggleTask(${t.id})" class="rounded border-neutral-300">
                            <div>
                                <span class="font-semibold text-neutral-800 ${t.completed ? 'line-through opacity-50' : ''}">${t.title}</span>
                                <span class="block text-[10px] text-neutral-400">${t.time}</span>
                            </div>
                        </div>
                        <span class="text-[10px] font-bold ${t.completed ? 'text-emerald-600' : 'text-neutral-400'}">${t.completed ? 'Done' : 'Pending'}</span>
                    `;
                    dashTasks.appendChild(row);
                });
            }

            const dashGoals = document.getElementById('dash-goals-summary');
            dashGoals.innerHTML = '';
            if(!window.goals.length) {
                dashGoals.innerHTML = `<p class="text-neutral-400 text-xs py-2 text-center">${window.currentLang === 'ml' ? 'ലക്ഷ്യങ്ങൾ ഒന്നും ചേർത്തിട്ടില്ല.' : 'No goals added yet.'}</p>`;
            } else {
                window.goals.slice(0, 3).forEach(g => {
                    const pct = Math.min(100, Math.round((g.saved / g.target) * 100));
                    const el = document.createElement('div');
                    el.className = 'space-y-1';
                    el.innerHTML = `
                        <div class="flex justify-between text-xs font-semibold text-neutral-700">
                            <span>${g.title}</span>
                            <span>₹${g.saved.toLocaleString('en-IN')} / ₹${g.target.toLocaleString('en-IN')} (${pct}%)</span>
                        </div>
                        <div class="w-full bg-neutral-100 rounded-full h-1.5 overflow-hidden">
                            <div class="bg-emerald-500 h-1.5 rounded-full" style="width: ${pct}%"></div>
                        </div>
                    `;
                    dashGoals.appendChild(el);
                });
            }

            const dashPay = document.getElementById('dash-payables-list');
            dashPay.innerHTML = '';
            const payables = window.debts.filter(d => d.type === 'payable');
            if(!payables.length) {
                dashPay.innerHTML = `<p class="text-neutral-400 text-xs py-2 text-center">${window.currentLang === 'ml' ? 'കൊടുക്കാനുള്ള കുടിശ്ശികകൾ ഒന്നുമില്ല! 🎉' : 'No pending debts to pay! 🎉'}</p>`;
            } else {
                payables.forEach(d => {
                    const el = document.createElement('div');
                    el.className = 'flex items-center justify-between p-2.5 rounded-xl bg-rose-50/50 border border-rose-100 text-xs';
                    el.innerHTML = `
                        <div>
                            <h5 class="font-bold text-neutral-800">${d.person}</h5>
                            <span class="text-[10px] text-rose-600 font-semibold">${window.currentLang === 'ml' ? 'ബാക്കി' : 'Due'}: ₹${d.amount.toLocaleString('en-IN')}</span>
                        </div>
                        <button onclick="payDebtAmount(${d.id})" class="bg-rose-600 hover:bg-rose-700 text-white text-[11px] font-semibold px-3 py-1.5 rounded-xl transition-all shadow-sm">
                            ${i18n[window.currentLang].pay_now}
                        </button>
                    `;
                    dashPay.appendChild(el);
                });
            }
        }

        window.payDebtAmount = function(id) {
            const debt = window.debts.find(d => d.id === id);
            if (!debt) return;
            const accPrompt = prompt("Select account to pay from (cash / federal / sbi):", "cash");
            if (!accPrompt || !['cash', 'federal', 'sbi'].includes(accPrompt.toLowerCase())) return;
            const acc = accPrompt.toLowerCase();

            const amtStr = prompt(`Total due: ₹${debt.amount}\nEnter payment amount:`, debt.amount);
            const payAmt = parseFloat(amtStr);
            if (payAmt && payAmt > 0) {
                window.accountBalances[acc] -= payAmt;
                window.transactions.push({
                    id: Date.now(),
                    desc: `Debt Payment to ${debt.person}`,
                    amount: payAmt,
                    type: 'expense',
                    account: acc,
                    date: new Date().toISOString().split('T')[0]
                });
                if (payAmt >= debt.amount) {
                    window.debts = window.debts.filter(d => d.id !== id);
                } else {
                    debt.amount -= payAmt;
                }
                window.saveState();
                renderAll();
                showToast("Payment recorded successfully!");
            }
        };

        // DAILY ROUTINES HANDLERS
        window.addRoutine = function(e) {
            e.preventDefault();
            window.routines.push({
                id: Date.now(),
                title: document.getElementById('routine-title').value,
                time: document.getElementById('routine-time').value,
                completed: false
            });
            document.getElementById('routine-form').reset();
            window.saveState();
            renderAll();
            showToast("Routine added!");
        };

        function renderRoutines() {
            const list = document.getElementById('routines-list');
            list.innerHTML = '';
            if(!window.routines.length) {
                list.innerHTML = `<p class="text-neutral-400 text-xs py-2 text-center">No routines configured.</p>`;
                return;
            }
            window.routines.forEach(r => {
                const row = document.createElement('div');
                row.className = 'flex items-center justify-between p-3 rounded-xl bg-white border border-neutral-100 text-xs shadow-sm';
                row.innerHTML = `
                    <div class="flex items-center gap-3">
                        <input type="checkbox" ${r.completed ? 'checked' : ''} onchange="toggleRoutine(${r.id})" class="rounded border-neutral-300">
                        <span class="${r.completed ? 'line-through opacity-50' : ''} font-medium text-neutral-800">${r.title} (${r.time})</span>
                    </div>
                    <button onclick="deleteRoutine(${r.id})" class="text-neutral-300 hover:text-rose-500"><i class="fa-solid fa-trash"></i></button>
                `;
                list.appendChild(row);
            });
        }

        window.toggleRoutine = function(id) {
            const r = window.routines.find(x => x.id === id);
            if(r) r.completed = !r.completed;
            window.saveState();
            renderAll();
        };

        window.deleteRoutine = function(id) {
            window.routines = window.routines.filter(x => x.id !== id);
            window.saveState();
            renderAll();
        };

        window.resetRoutinesForToday = function() {
            window.routines.forEach(r => r.completed = false);
            window.saveState();
            renderAll();
            showToast("Routines progress reset!");
        };

        // ONE-TIME TASKS HANDLERS
        window.addTask = function(e) {
            e.preventDefault();
            window.tasks.push({
                id: Date.now(),
                title: document.getElementById('task-title').value,
                date: document.getElementById('task-date').value,
                time: document.getElementById('task-time').value,
                completed: false
            });
            document.getElementById('task-form').reset();
            window.saveState();
            renderAll();
            showToast("Task scheduled!");
        };

        function renderTasks() {
            const list = document.getElementById('tasks-list');
            list.innerHTML = '';
            if(!window.tasks.length) {
                list.innerHTML = `<p class="text-neutral-400 text-xs py-2 text-center">No tasks available.</p>`;
                return;
            }
            window.tasks.forEach(t => {
                const row = document.createElement('div');
                row.className = 'flex items-center justify-between p-3 rounded-xl bg-white border border-neutral-100 text-xs shadow-sm';
                row.innerHTML = `
                    <div class="flex items-center gap-3">
                        <input type="checkbox" ${t.completed ? 'checked' : ''} onchange="toggleTask(${t.id})" class="rounded border-neutral-300">
                        <span class="${t.completed ? 'line-through opacity-50' : ''} font-medium text-neutral-800">${t.title} (${t.date} ${t.time})</span>
                    </div>
                    <button onclick="deleteTask(${t.id})" class="text-neutral-300 hover:text-rose-500"><i class="fa-solid fa-trash"></i></button>
                `;
