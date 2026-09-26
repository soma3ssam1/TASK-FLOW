<!DOCTYPE html>
<html lang="ar" dir="rtl">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>TaskFlow</title>

    <style>

        /* =====================================================
           GLOBAL
        ===================================================== */

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #6c63ff;
            --primary-dark: #5148e8;
            --secondary: #8b5cf6;
            --accent: #22c55e;

            --bg: #f5f7ff;
            --card: rgba(255, 255, 255, 0.86);
            --text: #182033;
            --muted: #7b8499;
            --border: rgba(108, 99, 255, 0.12);

            --danger: #ef4444;
            --warning: #f59e0b;

            --shadow:
                0 20px 50px rgba(39, 42, 78, 0.10);
        }

        body.dark {
            --bg: #0d1020;
            --card: rgba(24, 28, 49, 0.90);
            --text: #f5f7ff;
            --muted: #a7aec4;
            --border: rgba(255, 255, 255, 0.08);

            --shadow:
                0 20px 50px rgba(0, 0, 0, 0.35);
        }

        body {
            font-family:
                Arial,
                "Segoe UI",
                sans-serif;

            background:
                radial-gradient(
                    circle at 10% 10%,
                    rgba(108, 99, 255, 0.15),
                    transparent 28%
                ),
                radial-gradient(
                    circle at 90% 20%,
                    rgba(139, 92, 246, 0.13),
                    transparent 25%
                ),
                var(--bg);

            color: var(--text);

            min-height: 100vh;

            transition:
                background 0.3s ease,
                color 0.3s ease;
        }

        button,
        input {
            font-family: inherit;
        }

        button {
            cursor: pointer;
        }

        .hidden {
            display: none !important;
        }


        /* =====================================================
           WELCOME SCREEN
        ===================================================== */

        #welcomeScreen {
            min-height: 100vh;

            display: flex;
            justify-content: center;
            align-items: center;

            padding: 25px;

            position: relative;
            overflow: hidden;
        }

        .background-orb {
            position: absolute;

            width: 350px;
            height: 350px;

            border-radius: 50%;

            filter: blur(20px);

            opacity: 0.35;

            pointer-events: none;
        }

        .orb-one {
            background: #6c63ff;

            top: -100px;
            right: -100px;
        }

        .orb-two {
            background: #ec4899;

            bottom: -120px;
            left: -100px;
        }

        .welcome-card {
            width: min(600px, 100%);

            padding: 65px 45px;

            border-radius: 35px;

            background:
                linear-gradient(
                    135deg,
                    rgba(255,255,255,0.92),
                    rgba(246,245,255,0.80)
                );

            box-shadow:
                0 30px 80px rgba(68, 60, 150, 0.18);

            backdrop-filter: blur(25px);

            border:
                1px solid rgba(255,255,255,0.8);

            text-align: center;

            position: relative;

            z-index: 2;

            animation: welcomeAppear 0.8s ease;
        }

        body.dark .welcome-card {
            background:
                linear-gradient(
                    135deg,
                    rgba(25,29,52,0.95),
                    rgba(18,22,40,0.90)
                );

            border-color:
                rgba(255,255,255,0.08);
        }

        .logo-icon {
            width: 85px;
            height: 85px;

            margin: auto;
            margin-bottom: 25px;

            border-radius: 25px;

            display: flex;
            align-items: center;
            justify-content: center;

            font-size: 42px;

            color: white;

            background:
                linear-gradient(
                    135deg,
                    #6c63ff,
                    #9b5cff
                );

            box-shadow:
                0 15px 35px rgba(108,99,255,0.35);

            transform: rotate(-5deg);
        }

        .welcome-card h1 {
            font-size: 52px;

            margin-bottom: 10px;

            background:
                linear-gradient(
                    90deg,
                    #5b50ed,
                    #9b5cff,
                    #ec4899
                );

            -webkit-background-clip: text;
            background-clip: text;

            color: transparent;
        }

        .welcome-card h2 {
            font-size: 25px;

            margin-bottom: 15px;
        }

        .welcome-card p {
            color: var(--muted);

            font-size: 17px;

            line-height: 1.8;

            margin-bottom: 30px;
        }

        .start-button {
            border: none;

            color: white;

            padding: 15px 40px;

            border-radius: 14px;

            font-size: 17px;
            font-weight: bold;

            background:
                linear-gradient(
                    135deg,
                    #6c63ff,
                    #8b5cf6
                );

            box-shadow:
                0 12px 30px rgba(108,99,255,0.30);

            transition:
                transform 0.2s ease,
                box-shadow 0.2s ease;
        }

        .start-button:hover {
            transform: translateY(-3px);

            box-shadow:
                0 18px 40px rgba(108,99,255,0.38);
        }


        /* =====================================================
           APP LAYOUT
        ===================================================== */

        .app {
            min-height: 100vh;

            display: flex;
        }


        /* =====================================================
           SIDEBAR
        ===================================================== */

        .sidebar {
            width: 260px;

            min-height: 100vh;

            padding: 25px 18px;

            position: fixed;

            right: 0;
            top: 0;

            background:
                rgba(255,255,255,0.72);

            backdrop-filter: blur(25px);

            border-left:
                1px solid var(--border);

            z-index: 20;
        }

        body.dark .sidebar {
            background:
                rgba(14,17,33,0.88);
        }

        .brand {
            display: flex;

            align-items: center;

            gap: 12px;

            padding: 10px;

            margin-bottom: 35px;
        }

        .brand-logo {
            width: 45px;
            height: 45px;

            border-radius: 13px;

            display: flex;
            align-items: center;
            justify-content: center;

            background:
                linear-gradient(
                    135deg,
                    #6c63ff,
                    #9b5cff
                );

            color: white;

            font-size: 22px;
        }

        .brand h2 {
            font-size: 21px;
        }

        .brand span {
            display: block;

            color: var(--muted);

            font-size: 11px;

            margin-top: 2px;
        }

        .menu-title {
            color: var(--muted);

            font-size: 12px;

            margin:
                15px 12px 10px;
        }

        .menu-item {
            width: 100%;

            border: none;

            background: transparent;

            color: var(--muted);

            padding: 13px 15px;

            margin-bottom: 6px;

            border-radius: 12px;

            display: flex;

            align-items: center;

            gap: 12px;

            font-size: 15px;

            text-align: right;

            transition: 0.2s;
        }

        .menu-item:hover {
            background:
                rgba(108,99,255,0.08);

            color: var(--primary);
        }

        .menu-item.active {
            background:
                linear-gradient(
                    135deg,
                    rgba(108,99,255,0.15),
                    rgba(139,92,246,0.08)
                );

            color: var(--primary);

            font-weight: bold;
        }

        .menu-icon {
            font-size: 19px;

            width: 25px;

            text-align: center;
        }


        /* =====================================================
           MAIN
        ===================================================== */

        .main {
            width: calc(100% - 260px);

            margin-right: 260px;

            padding: 30px 35px;
        }


        /* =====================================================
           TOP BAR
        ===================================================== */

        .topbar {
            display: flex;

            align-items: center;

            justify-content: space-between;

            margin-bottom: 30px;
        }

        .greeting h1 {
            font-size: 30px;

            margin-bottom: 6px;
        }

        .greeting p {
            color: var(--muted);

            font-size: 14px;
        }

        .top-actions {
            display: flex;

            align-items: center;

            gap: 10px;
        }

        .icon-button {
            width: 45px;
            height: 45px;

            border: 1px solid var(--border);

            border-radius: 13px;

            background: var(--card);

            color: var(--text);

            font-size: 18px;

            box-shadow: var(--shadow);

            transition: 0.2s;
        }

        .icon-button:hover {
            transform: translateY(-2px);

            color: var(--primary);
        }


        /* =====================================================
           STAT CARDS
        ===================================================== */

        .stats {
            display: grid;

            grid-template-columns:
                repeat(4, 1fr);

            gap: 18px;

            margin-bottom: 22px;
        }

        .stat-card {
            background: var(--card);

            border:
                1px solid var(--border);

            border-radius: 20px;

            padding: 20px;

            box-shadow: var(--shadow);

            backdrop-filter: blur(20px);

            position: relative;

            overflow: hidden;
        }

        .stat-card::after {
            content: "";

            position: absolute;

            width: 90px;
            height: 90px;

            border-radius: 50%;

            background:
                rgba(108,99,255,0.10);

            left: -30px;
            bottom: -30px;
        }

        .stat-top {
            display: flex;

            justify-content: space-between;

            align-items: center;

            margin-bottom: 15px;
        }

        .stat-icon {
            width: 43px;
            height: 43px;

            border-radius: 12px;

            display: flex;

            align-items: center;
            justify-content: center;

            font-size: 19px;

            background:
                rgba(108,99,255,0.11);
        }

        .stat-card:nth-child(2)
        .stat-icon {
            background:
                rgba(34,197,94,0.12);
        }

        .stat-card:nth-child(3)
        .stat-icon {
            background:
                rgba(245,158,11,0.12);
        }

        .stat-card:nth-child(4)
        .stat-icon {
            background:
                rgba(236,72,153,0.12);
        }

        .stat-card small {
            color: var(--muted);
        }

        .stat-card h3 {
            font-size: 27px;

            margin-top: 5px;
        }


        /* =====================================================
           CONTENT GRID
        ===================================================== */

        .content-grid {
            display: grid;

            grid-template-columns:
                1.55fr
                1fr;

            gap: 20px;
        }

        .card {
            background: var(--card);

            border:
                1px solid var(--border);

            border-radius: 22px;

            padding: 23px;

            box-shadow: var(--shadow);

            backdrop-filter: blur(20px);
        }

        .card-header {
            display: flex;

            align-items: center;

            justify-content: space-between;

            margin-bottom: 20px;
        }

        .card-header h2 {
            font-size: 19px;
        }

        .card-header span {
            color: var(--muted);

            font-size: 13px;
        }


        /* =====================================================
           TASKS
        ===================================================== */

        .task-tools {
            display: flex;

            gap: 8px;

            margin-bottom: 18px;
        }

        .search {
            flex: 1;

            border:
                1px solid var(--border);

            background:
                rgba(255,255,255,0.35);

            color: var(--text);

            border-radius: 10px;

            padding: 11px 13px;

            outline: none;
        }

        body.dark .search {
            background:
                rgba(255,255,255,0.04);
        }

        .filter {
            border:
                1px solid var(--border);

            background: var(--card);

            color: var(--text);

            border-radius: 10px;

            padding: 0 12px;

            cursor: pointer;
        }

        .task-list {
            display: flex;

            flex-direction: column;

            gap: 9px;
        }

        .task {
            display: flex;

            align-items: center;

            gap: 12px;

            padding: 14px;

            border:
                1px solid transparent;

            border-radius: 14px;

            background:
                rgba(108,99,255,0.045);

            transition: 0.2s;
        }

        .task:hover {
            border-color:
                var(--border);

            transform: translateX(-2px);
        }

        .task-check {
            width: 20px;
            height: 20px;

            accent-color: var(--primary);

            cursor: pointer;
        }

        .task-info {
            flex: 1;
        }

        .task-info strong {
            display: block;

            font-size: 14px;

            margin-bottom: 5px;
        }

        .task-info small {
            color: var(--muted);

            font-size: 12px;
        }

        .task.completed strong {
            text-decoration: line-through;

            opacity: 0.55;
        }

        .delete-task {
            border: none;

            background: transparent;

            color: #a0a7b8;

            font-size: 16px;

            opacity: 0;

            transition: 0.2s;
        }

        .task:hover .delete-task {
            opacity: 1;
        }

        .delete-task:hover {
            color: var(--danger);
        }

        .add-task {
            width: 100%;

            border: 1px dashed
                rgba(108,99,255,0.35);

            background:
                rgba(108,99,255,0.05);

            color: var(--primary);

            padding: 13px;

            border-radius: 12px;

            margin-top: 13px;

            font-weight: bold;
        }


        /* =====================================================
           TIMER
        ===================================================== */

        .timer-box {
            text-align: center;

            padding:
                10px 0 5px;
        }

        .timer-circle {
            width: 190px;
            height: 190px;

            margin: 10px auto 20px;

            border-radius: 50%;

            display: flex;

            flex-direction: column;

            justify-content: center;
            align-items: center;

            background:
                radial-gradient(
                    circle,
                    var(--card) 58%,
                    transparent 59%
                ),
                conic-gradient(
                    #6c63ff 0deg,
                    #8b5cf6 180deg,
                    rgba(108,99,255,0.10) 180deg
                );

            box-shadow:
                0 15px 40px
                rgba(108,99,255,0.16);
        }

        .timer-time {
            font-size: 39px;

            font-weight: bold;
        }

        .timer-label {
            color: var(--muted);

            font-size: 12px;

            margin-top: 5px;
        }

        .timer-buttons {
            display: flex;

            justify-content: center;

            gap: 8px;
        }

        .timer-buttons button {
            border: none;

            padding: 11px 18px;

            border-radius: 10px;

            font-weight: bold;
        }

        .timer-start {
            background:
                linear-gradient(
                    135deg,
                    #6c63ff,
                    #8b5cf6
                );

            color: white;
        }

        .timer-reset {
            background:
                rgba(108,99,255,0.09);

            color: var(--primary);
        }


        /* =====================================================
           PROGRESS
        ===================================================== */

        .progress-layout {
            display: flex;

            align-items: center;

            gap: 25px;
        }

        .progress-ring {
            width: 145px;
            height: 145px;

            border-radius: 50%;

            background:
                conic-gradient(
                    #6c63ff 0deg,
                    #8b5cf6 0deg,
                    rgba(108,99,255,0.10) 0deg
                );

            display: flex;

            align-items: center;
            justify-content: center;

            flex-shrink: 0;
        }

        .progress-inner {
            width: 112px;
            height: 112px;

            border-radius: 50%;

            background: var(--card);

            display: flex;

            align-items: center;
            justify-content: center;

            font-size: 25px;

            font-weight: bold;
        }

        .progress-info h3 {
            font-size: 25px;

            margin-bottom: 6px;
        }

        .progress-info p {
            color: var(--muted);

            font-size: 13px;

            line-height: 1.6;
        }


        /* =====================================================
           CALENDAR
        ===================================================== */

        .calendar-days {
            display: grid;

            grid-template-columns:
                repeat(7, 1fr);

            gap: 6px;
        }

        .day {
            text-align: center;

            padding: 9px 3px;

            border-radius: 9px;

            font-size: 12px;

            color: var(--muted);
        }

        .day.active {
            background:
                linear-gradient(
                    135deg,
                    #6c63ff,
                    #8b5cf6);

            color: white;
        }

        .day.today {
            border: 1px solid var(--primary);
            color: var(--primary);
            font-weight: bold;
        }


        /* =====================================================
           REMINDERS
        ===================================================== */

        .reminders {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .reminder {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px;
            border-radius: 12px;
            background: rgba(108,99,255,0.05);
        }

        .reminder-icon {
            width: 38px;
            height: 38px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(108,99,255,0.10);
            font-size: 17px;
        }

        .reminder-info {
            flex: 1;
        }

        .reminder-info strong {
            display: block;
            font-size: 13px;
            margin-bottom: 3px;
        }

        .reminder-info small {
            color: var(--muted);
            font-size: 11px;
        }


        /* =====================================================
           QUICK TIP
        ===================================================== */

        .tip {
            background:
                linear-gradient(
                    135deg,
                    rgba(108,99,255,0.12),
                    rgba(139,92,246,0.08)
                );

            border: 1px solid var(--border);
            border-radius: 18px;
            padding: 18px;
        }

        .tip strong {
            display: block;
            margin-bottom: 7px;
        }

        .tip p {
            color: var(--muted);
            font-size: 13px;
            line-height: 1.7;
        }


        /* =====================================================
           MODAL
        ===================================================== */

        .modal {
            position: fixed;
            inset: 0;

            background:
                rgba(10,12,25,0.55);

            display: flex;
            align-items: center;
            justify-content: center;

            padding: 20px;

            z-index: 100;

            backdrop-filter: blur(8px);
        }

        .modal-box {
            width: min(450px, 100%);

            background: var(--card);

            border: 1px solid var(--border);

            border-radius: 22px;

            padding: 25px;

            box-shadow: 0 30px 80px rgba(0,0,0,0.25);

            animation: modalAppear 0.25s ease;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;

            margin-bottom: 20px;
        }

        .modal-header h2 {
            font-size: 20px;
        }

        .close-modal {
            border: none;
            background: transparent;
            color: var(--muted);
            font-size: 23px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 7px;
            font-size: 13px;
            font-weight: bold;
        }

        .form-group input,
        .form-group select {
            width: 100%;

            padding: 12px;

            border: 1px solid var(--border);

            border-radius: 11px;

            outline: none;

            background: rgba(255,255,255,0.4);

            color: var(--text);
        }

        body.dark .form-group input,
        body.dark .form-group select {
            background: rgba(255,255,255,0.05);
        }

        .save-task {
            width: 100%;

            border: none;

            padding: 13px;

            border-radius: 11px;

            color: white;

            font-weight: bold;

            background:
                linear-gradient(
                    135deg,
                    #6c63ff,
                    #8b5cf6
                );
        }


        /* =====================================================
           SETTINGS
        ===================================================== */

        .settings-panel {
            position: fixed;

            top: 0;
            left: -340px;

            width: 320px;
            height: 100vh;

            padding: 25px;

            background: var(--card);

            border-right: 1px solid var(--border);

            box-shadow: 10px 0 40px rgba(0,0,0,0.12);

            z-index: 90;

            transition: left 0.3s ease;

            backdrop-filter: blur(20px);
        }

        .settings-panel.open {
            left: 0;
        }

        .settings-header {
            display: flex;

            align-items: center;
            justify-content: space-between;

            margin-bottom: 30px;
        }

        .settings-header button {
            border: none;
            background: transparent;
            color: var(--muted);
            font-size: 22px;
        }

        .setting-row {
            display: flex;

            align-items: center;
            justify-content: space-between;

            padding: 15px 0;

            border-bottom: 1px solid var(--border);
        }

        .setting-row strong {
            font-size: 14px;
        }

        .setting-row small {
            display: block;
            color: var(--muted);
            margin-top: 4px;
            font-size: 11px;
        }

        .switch {
            width: 48px;
            height: 26px;

            border-radius: 20px;

            background: #cbd0dc;

            position: relative;

            cursor: pointer;

            transition: 0.2s;
        }

        .switch::after {
            content: "";

            width: 20px;
            height: 20px;

            border-radius: 50%;

            background: white;

            position: absolute;

            top: 3px;
            left: 4px;

            transition: 0.2s;
        }

        .switch.active {
            background: var(--primary);
        }

        .switch.active::after {
            left: 24px;
        }


        /* =====================================================
           ANIMATIONS
        ===================================================== */

        @keyframes welcomeAppear {
            from {
                opacity: 0;
                transform: translateY(25px) scale(0.97);
            }

            to {
                opacity: 1;
                transform: translateY(0) scale(1);
            }
        }

        @keyframes modalAppear {
            from {
                opacity: 0;
                transform: scale(0.95);
            }

            to {
                opacity: 1;
                transform: scale(1);
            }
        }


        /* =====================================================
           RESPONSIVE
        ===================================================== */

        @media (max-width: 1100px) {

            .stats {
                grid-template-columns: repeat(2, 1fr);
            }

            .content-grid {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 750px) {

            .sidebar {
                width: 75px;
                padding: 20px 10px;
            }

            .brand h2,
            .brand span,
            .menu-title,
            .menu-item span:not(.menu-icon) {
                display: none;
            }

            .brand {
                justify-content: center;
            }

            .menu-item {
                justify-content: center;
                padding: 13px 5px;
            }

            .main {
                width: calc(100% - 75px);
                margin-right: 75px;
                padding: 20px;
            }

            .stats {
                grid-template-columns: 1fr;
            }

            .topbar {
                align-items: flex-start;
                gap: 15px;
            }

            .greeting h1 {
                font-size: 24px;
            }
        }

        @media (max-width: 500px) {

            .welcome-card {
                padding: 45px 22px;
            }

            .welcome-card h1 {
                font-size: 42px;
            }

            .progress-layout {
                flex-direction: column;
                text-align: center;
            }

            .task-tools {
                flex-direction: column;
            }

            .filter {
                height: 42px;
            }
        }
<style>
      /* ===== TASKFLOW CINEMATIC THEME ===== */

:root {
    --primary: #8b5cf6;
    --primary-dark: #6d28d9;
    --primary-light: #a78bfa;

    --bg: #0b0b14;
    --surface: #12121f;
    --surface-2: #191929;
    --card: rgba(255, 255, 255, 0.055);

    --text: #f5f3ff;
    --text-light: #aaa7bd;

    --border: rgba(167, 139, 250, 0.16);

    --success: #34d399;
    --warning: #fbbf24;
    --danger: #fb7185;
}

/* الخلفية الرئيسية */
body {
    background:
        radial-gradient(circle at 15% 15%, rgba(139, 92, 246, 0.16), transparent 30%),
        radial-gradient(circle at 85% 20%, rgba(59, 130, 246, 0.10), transparent 28%),
        radial-gradient(circle at 50% 100%, rgba(124, 58, 237, 0.12), transparent 35%),
        #0b0b14 !important;

    color: var(--text);
}

/* الـSidebar */
.sidebar {
    background:
        linear-gradient(
            180deg,
            rgba(18, 18, 31, 0.98),
            rgba(10, 10, 20, 0.98)
        ) !important;

    border-left: 1px solid var(--border) !important;
    box-shadow: 10px 0 40px rgba(0, 0, 0, 0.25);
}

/* الكروت */
.card,
.stat-card,
.task-card,
.reminder-card,
.tip-card {
    background: linear-gradient(
        145deg,
        rgba(255, 255, 255, 0.075),
        rgba(255, 255, 255, 0.025)
    ) !important;

    border: 1px solid var(--border) !important;

    box-shadow:
        0 15px 45px rgba(0, 0, 0, 0.25),
        inset 0 1px 0 rgba(255, 255, 255, 0.035);

    backdrop-filter: blur(14px);
}

/* العناوين */
h1,
h2,
h3 {
    color: #f8f7ff;
}

/* اللون الأساسي */
button,
.btn-primary,
.add-task-btn {
    background: linear-gradient(
        135deg,
        #8b5cf6,
        #6d28d9
    ) !important;

    box-shadow:
        0 8px 25px rgba(139, 92, 246, 0.28);
}

/* تأثير الحركة */
button,
.nav-item,
.task-card,
.card {
    transition:
        transform 0.25s ease,
        box-shadow 0.25s ease,
        border-color 0.25s ease;
}

button:hover {
    transform: translateY(-2px);
    box-shadow:
        0 12px 30px rgba(139, 92, 246, 0.35);
}

.task-card:hover,
.card:hover,
.stat-card:hover {
    transform: translateY(-3px);
    border-color: rgba(167, 139, 250, 0.32) !important;
}

/* العناصر المختارة */
.nav-item.active,
.day.active {
    background: linear-gradient(
        135deg,
        #8b5cf6,
        #6d28d9
    ) !important;

    box-shadow:
        0 8px 25px rgba(139, 92, 246, 0.25);
}

/* شريط التقدم */
.progress-bar,
.progress-fill {
    background: linear-gradient(
        90deg,
        #6d28d9,
        #a78bfa
    ) !important;
}

/* الـInputs */
input,
select,
textarea {
    background: rgba(255, 255, 255, 0.045) !important;
    color: #f5f3ff !important;
    border: 1px solid rgba(167, 139, 250, 0.16) !important;
}

input:focus,
select:focus,
textarea:focus {
    border-color: #8b5cf6 !important;
    box-shadow: 0 0 0 3px rgba(139, 92, 246, 0.12);
    outline: none;
}

/* نصوص ثانوية */
.text-muted,
.subtitle,
.task-meta {
    color: #aaa7bd !important;
}

/* لمسة ضوء سينمائية */
.dashboard::before {
    content: "";
    position: fixed;
    width: 320px;
    height: 320px;
    top: -120px;
    right: 20%;
    background: rgba(139, 92, 246, 0.08);
    filter: blur(90px);
    border-radius: 50%;
    pointer-events: none;
    z-index: -1;
}
    </style>
  
</head>

<body>

    <!-- =====================================================
         WELCOME
    ===================================================== -->

    <section id="welcomeScreen">

        <div class="background-orb orb-one"></div>
        <div class="background-orb orb-two"></div>

        <div class="welcome-card">

            <div class="logo-icon">
                ✓
            </div>

            <h1>TaskFlow</h1>

            <h2>نظّم يومك، وحقق هدفك</h2>

            <p>
                منصة بسيطة وذكية تساعدك على تنظيم مهامك،
                متابعة مذاكرتك، وقياس تقدمك يومًا بعد يوم.
            </p>

            <button class="start-button" id="startButton">
                ابدأ الآن
            </button>

        </div>

    </section>


    <!-- =====================================================
         APPLICATION
    ===================================================== -->

    <section id="application" class="app hidden">

        <!-- SIDEBAR -->

        <aside class="sidebar">

            <div class="brand">

                <div class="brand-logo">
                    ✓
                </div>

                <div>
                    <h2>TaskFlow</h2>
                    <span>Study & Productivity</span>
                </div>

            </div>

            <div class="menu-title">
                القائمة الرئيسية
            </div>

            <button class="menu-item active">
                <span class="menu-icon">⌂</span>
                <span>الرئيسية</span>
            </button>

            <button class="menu-item" id="openTasks">
                <span class="menu-icon">✓</span>
                <span>المهام</span>
            </button>

            <button class="menu-item">
                <span class="menu-icon">◷</span>
                <span>المؤقت</span>
            </button>

            <button class="menu-item">
                <span class="menu-icon">▣</span>
                <span>التقويم</span>
            </button>

            <div class="menu-title">
                أخرى
            </div>

            <button class="menu-item" id="settingsButton">
                <span class="menu-icon">⚙</span>
                <span>الإعدادات</span>
            </button>

        </aside>


        <!-- MAIN -->

        <main class="main">

            <header class="topbar">

                <div class="greeting">

                    <h1>أهلاً بك 👋</h1>

                    <p id="currentDate">
                        يوم جديد لإنجاز أهدافك
                    </p>

                </div>

                <div class="top-actions">

                    <button class="icon-button" id="themeButton">
                        ☾
                    </button>

                    <button class="icon-button" id="quickAdd">
                        +
                    </button>

                </div>

            </header>


            <!-- STATS -->

            <section class="stats">

                <div class="stat-card">

                    <div class="stat-top">

                        <small>كل المهام</small>

                        <div class="stat-icon">
                            ✓
                        </div>

                    </div>

                    <h3 id="totalTasks">
                        0
                    </h3>

                </div>


                <div class="stat-card">

                    <div class="stat-top">

                        <small>المكتملة</small>

                        <div class="stat-icon">
                            ✓
                        </div>

                    </div>

                    <h3 id="completedTasks">
                        0
                    </h3>

                </div>


                <div class="stat-card">

                    <div class="stat-top">

                        <small>قيد التنفيذ</small>

                        <div class="stat-icon">
                            ◷
                        </div>

                    </div>

                    <h3 id="pendingTasks">
                        0
                    </h3>

                </div>


                <div class="stat-card">

                    <div class="stat-top">

                        <small>نسبة الإنجاز</small>

                        <div class="stat-icon">
                            ★
                        </div>

                    </div>

                    <h3 id="completionRate">
                        0%
                    </h3>

                </div>

            </section>


            <!-- CONTENT -->

            <section class="content-grid">


                <!-- TASK CARD -->

                <div class="card">

                    <div class="card-header">

                        <h2>
                            مهامي اليوم
                        </h2>

                        <span id="taskCountLabel">
                            0 مهام
                        </span>

                    </div>


                    <div class="task-tools">

                        <input
                            type="text"
                            class="search"
                            id="searchInput"
                            placeholder="ابحث عن مهمة..."
                        >

                        <select class="filter" id="filterSelect">

                            <option value="all">
                                الكل
                            </option>

                            <option value="pending">
                                غير مكتملة
                            </option>

                            <option value="completed">
                                مكتملة
                            </option>

                        </select>

                    </div>


                    <div class="task-list" id="taskList">
                    </div>


                    <button class="add-task" id="addTaskButton">
                        + إضافة مهمة جديدة
                    </button>

                </div>


                <!-- TIMER -->

                <div class="card">

                    <div class="card-header">

                        <h2>
                            جلسة التركيز
                        </h2>

                        <span>
                            45 دقيقة
                        </span>

                    </div>

                    <div class="timer-box">

                        <div class="timer-circle">

                            <div class="timer-time" id="timer">
                                45:00
                            </div>

                            <div class="timer-label">
                                وقت التركيز
                            </div>

                        </div>


                        <div class="timer-buttons">

                            <button
                                class="timer-start"
                                id="timerStart"
                            >
                                ابدأ
                            </button>

                            <button
                                class="timer-reset"
                                id="timerReset"
                            >
                                إعادة
                            </button>

                        </div>

                    </div>

                </div>


                <!-- PROGRESS -->

                <div class="card">

                    <div class="card-header">

                        <h2>
                            تقدمي
                        </h2>

                        <span>
                            اليوم
                        </span>

                    </div>

                    <div class="progress-layout">

                        <div
                            class="progress-ring"
                            id="progressRing"
                        >

                            <div class="progress-inner">
                                <span id="progressPercent">
                                    0%
                                </span>
                            </div>

                        </div>

                        <div class="progress-info">

                            <h3 id="progressTitle">
                                بداية جيدة
                            </h3>

                            <p>
                                أكمل مهامك اليوم لتحافظ
                                على تقدمك وتقترب من أهدافك.
                            </p>

                        </div>

                    </div>

                </div>


                <!-- CALENDAR -->

                <div class="card">

                    <div class="card-header">

                        <h2>
                            هذا الأسبوع
                        </h2>

                        <span>
                            التقويم
                        </span>

                    </div>

                    <div class="calendar-days">

                        <div class="day">السبت</div>
                        <div class="day">الأحد</div>
                        <div class="day">الإثنين</div>
                        <div class="day">الثلاثاء</div>
                        <div class="day">الأربعاء</div>
                        <div class="day">الخميس</div>
                        <div class="day">الجمعة</div>

                    </div>

                </div>


                <!-- REMINDERS -->

                <div class="card">

                    <div class="card-header">

                        <h2>
                            التذكيرات
                        </h2>

                        <span>
                            اليوم
                        </span>

                    </div>

                    <div class="reminders">

                        <div class="reminder">

                            <div class="reminder-icon">
                                📚
                            </div>

                            <div class="reminder-info">

                                <strong>
                                    وقت المذاكرة
                                </strong>

                                <small>
                                    لا تنسي جلسة التركيز
                                </small>

                            </div>

                        </div>


                        <div class="reminder">

                            <div class="reminder-icon">
                                🕌
                            </div>

                            <div class="reminder-info">

                                <strong>
                                    وقت روحاني
                                </strong>

                                <small>
                                    خصصي وقتًا هادئًا للتأمل
                                </small>

                            </div>

                        </div>

                    </div>

                </div>


                <!-- TIP -->

                <div class="tip">

                    <strong>
                        💡 نصيحة اليوم
                    </strong>

                    <p>
                        لا تحاولي إنجاز كل شيء مرة واحدة.
                        ركزي على مهمة واحدة، وبعدها انتقلي
                        للتي تليها.
                    </p>

                </div>

            </section>

        </main>

    </section>


    <!-- =====================================================
         TASK MODAL
    ===================================================== -->

    <div id="taskModal" class="modal hidden">

        <div class="modal-box">

            <div class="modal-header">

                <h2>
                    إضافة مهمة
                </h2>

                <button
                    class="close-modal"
                    id="closeModal"
                >
                    ×
                </button>

            </div>


            <div class="form-group">

                <label>
                    اسم المهمة
                </label>

                <input
                    type="text"
                    id="taskInput"
                    placeholder="مثال: مراجعة درس الرياضيات"
                >

            </div>


            <div class="form-group">

                <label>
                    المادة / التصنيف
                </label>

                <select id="taskCategory">

                    <option value="مذاكرة">
                        مذاكرة
                    </option>

                    <option value="واجب">
                        واجب
                    </option>

                    <option value="مراجعة">
                        مراجعة
                    </option>

                    <option value="شخصي">
                        شخصي
                    </option>

                </select>

            </div>


            <button
                class="save-task"
                id="saveTask"
            >
                حفظ المهمة
            </button>

        </div>

    </div>


    <!-- =====================================================
         SETTINGS PANEL
    ===================================================== -->

    <aside class="settings-panel" id="settingsPanel">

        <div class="settings-header">

            <h2>
                الإعدادات
            </h2>

            <button id="closeSettings">
                ×
            </button>

        </div>


        <div class="setting-row">

            <div>

                <strong>
                    الوضع الليلي
                </strong>

                <small>
                    تغيير مظهر التطبيق
                </small>

            </div>

            <div
                class="switch"
                id="darkSwitch"
            ></div>

        </div>

    </aside>


    <!-- =====================================================
         JAVASCRIPT
    ===================================================== -->

    <script>

        /* =====================================================
           ELEMENTS
        ===================================================== */

        const welcomeScreen =
            document.getElementById("welcomeScreen");

        const application =
            document.getElementById("application");

        const startButton =
            document.getElementById("startButton");

        const taskModal =
            document.getElementById("taskModal");

        const addTaskButton =
            document.getElementById("addTaskButton");

        const quickAdd =
            document.getElementById("quickAdd");

        const closeModal =
            document.getElementById("closeModal");

        const saveTask =
            document.getElementById("saveTask");

        const taskInput =
            document.getElementById("taskInput");

        const taskCategory =
            document.getElementById("taskCategory");

        const taskList =
            document.getElementById("taskList");

        const searchInput =
            document.getElementById("searchInput");

        const filterSelect =
            document.getElementById("filterSelect");

        const totalTasks =
            document.getElementById("totalTasks");

        const completedTasks =
            document.getElementById("completedTasks");

        const pendingTasks =
            document.getElementById("pendingTasks");

        const completionRate =
            document.getElementById("completionRate");

        const progressRing =
            document.getElementById("progressRing");

        const progressPercent =
            document.getElementById("progressPercent");

        const progressTitle =
            document.getElementById("progressTitle");

        const taskCountLabel =
            document.getElementById("taskCountLabel");

        const themeButton =
            document.getElementById("themeButton");

        const settingsButton =
            document.getElementById("settingsButton");

        const settingsPanel =
            document.getElementById("settingsPanel");

        const closeSettings =
            document.getElementById("closeSettings");

        const darkSwitch =
            document.getElementById("darkSwitch");

        const timerElement =
            document.getElementById("timer");

        const timerStart =
            document.getElementById("timerStart");

        const timerReset =
            document.getElementById("timerReset");


        /* =====================================================
           TASKS
        ===================================================== */

        let tasks =
            JSON.parse(
                localStorage.getItem("taskflowTasks")
            ) || [];


        function saveTasks() {

            localStorage.setItem(
                "taskflowTasks",
                JSON.stringify(tasks)
            );

        }


        function escapeHTML(text) {

            const div =
                document.createElement("div");

            div.textContent = text;

            return div.innerHTML;
        }


        function renderTasks() {

            const search =
                searchInput.value
                    .trim()
                    .toLowerCase();

            const filter =
                filterSelect.value;


            const filteredTasks =
                tasks.filter(task => {

                    const matchesSearch =
                        task.title
                            .toLowerCase()
                            .includes(search);

                    const matchesFilter =
                        filter === "all" ||
                        (filter === "completed" &&
                            task.completed) ||
                        (filter === "pending" &&
                            !task.completed);

                    return (
                        matchesSearch &&
                        matchesFilter
                    );

                });


            taskList.innerHTML = "";


            if (filteredTasks.length === 0) {

                taskList.innerHTML = `
                    <div style="
                        text-align:center;
                        padding:30px;
                        color:var(--muted);
                    ">
                        لا توجد مهام هنا ✨
                    </div>
                `;

            }


            filteredTasks.forEach(task => {

                const taskElement =
                    document.createElement("div");

                taskElement.className =
                    "task" +
                    (task.completed
                        ? " completed"
                        : "");

                taskElement.innerHTML = `

                    <input
                        type="checkbox"
                        class="task-check"
                        ${task.completed ? "checked" : ""}
                    >

                    <div class="task-info">

                        <strong>
                            ${escapeHTML(task.title)}
                        </strong>

                        <small>
                            ${escapeHTML(task.category)}
                        </small>

                    </div>

                    <button class="delete-task">
                        🗑
                    </button>

                `;


                const checkbox =
                    taskElement.querySelector(
                        ".task-check"
                    );

                checkbox.addEventListener(
                    "change",
                    () => {

                        task.completed =
                            checkbox.checked;

                        saveTasks();
                        renderTasks();

                    }
                );


                const deleteButton =
                    taskElement.querySelector(
                        ".delete-task"
                    );

                deleteButton.addEventListener(
                    "click",
                    () => {

                        tasks =
                            tasks.filter(
                                item =>
                                    item.id !== task.id
                            );

                        saveTasks();
                        renderTasks();

                    }
                );


                taskList.appendChild(taskElement);

            });


            updateProgress();

        }


        function updateProgress() {

            const total =
                tasks.length;

            const completed =
                tasks.filter(
                    task => task.completed
                ).length;

            const pending =
                total - completed;

            const percentage =
                total === 0
                    ? 0
                    : Math.round(
                        (completed / total) * 100
                    );


            totalTasks.textContent =
                total;

            completedTasks.textContent =
                completed;

            pendingTasks.textContent =
                pending;

            completionRate.textContent =
                percentage + "%";

            progressPercent.textContent =
                percentage + "%";


            const degrees =
                percentage * 3.6;

            progressRing.style.background =
                `conic-gradient(
                    #6c63ff 0deg,
                    #8b5cf6 ${degrees}deg,
                    rgba(108,99,255,0.10)
                    ${degrees}deg
                )`;


            if (percentage === 100) {

                progressTitle.textContent =
                    "ممتاز جدًا! 🎉";

            } else if (percentage >= 70) {

                progressTitle.textContent =
                    "أداء رائع!";

            } else if (percentage >= 40) {

                progressTitle.textContent =
                    "استمري في التقدم";

            } else {

                progressTitle.textContent =
                    "بداية جيدة";

            }


            taskCountLabel.textContent =
                total +
                (total === 1
                    ? " مهمة"
                    : " مهام");

        }


        /* =====================================================
           START APPLICATION
        ===================================================== */

        startButton.addEventListener(
            "click",
            () => {

                welcomeScreen.classList.add(
                    "hidden"
                );

                application.classList.remove(
                    "hidden"
                );

                renderTasks();

            }
        );


        /* =====================================================
           MODAL
        ===================================================== */

        function openTaskModal() {

            taskModal.classList.remove(
                "hidden"
            );

            taskInput.focus();

        }


        function closeTaskModal() {

            taskModal.classList.add(
                "hidden"
            );

            taskInput.value = "";

        }


        addTaskButton.addEventListener(
            "click",
            openTaskModal
        );

        quickAdd.addEventListener(
            "click",
            openTaskModal
        );

        closeModal.addEventListener(
            "click",
            closeTaskModal
        );


        taskModal.addEventListener(
            "click",
            event => {

                if (
                    event.target ===
                    taskModal
                ) {

                    closeTaskModal();

                }

            }
        );


        saveTask.addEventListener(
            "click",
            () => {

                const title =
                    taskInput.value.trim();

                if (!title) {

                    taskInput.focus();

                    return;

                }


                tasks.unshift({

                    id:
                        Date.now(),

                    title:
                        title,

                    category:
                        taskCategory.value,

                    completed:
                        false

                });


                saveTasks();

                renderTasks();

                closeTaskModal();

            }
        );


        /* =====================================================
           SEARCH & FILTER
        ===================================================== */

        searchInput.addEventListener(
            "input",
            renderTasks
        );

        filterSelect.addEventListener(
            "change",
            renderTasks
        );


        /* =====================================================
           DARK MODE
        ===================================================== */

        function setDarkMode(enabled) {

            document.body.classList.toggle(
                "dark",
                enabled
            );

            darkSwitch.classList.toggle(
                "active",
                enabled
            );

            themeButton.textContent =
                enabled ? "☀" : "☾";

            localStorage.setItem(
                "taskflowDark",
                enabled
                    ? "true"
                    : "false"
            );

        }


        const savedDarkMode =
            localStorage.getItem(
                "taskflowDark"
            ) === "true";


        setDarkMode(savedDarkMode);


        themeButton.addEventListener(
            "click",
            () => {

                setDarkMode(
                    !document.body.classList.contains(
                        "dark"
                    )
                );

            }
        );


        darkSwitch.addEventListener(
            "click",
            () => {

                setDarkMode(
                    !document.body.classList.contains(
                        "dark"
                    )
                );

            }
        );


        /* =====================================================
           SETTINGS
        ===================================================== */

        settingsButton.addEventListener(
            "click",
            () => {

                settingsPanel.classList.add(
                    "open"
                );

            }
        );


        closeSettings.addEventListener(
            "click",
            () => {

                settingsPanel.classList.remove(
                    "open"
                );

            }
        );


        /* =====================================================
           DATE
        ===================================================== */

        const currentDate =
            document.getElementById(
                "currentDate"
            );


        const today =
            new Date();


        currentDate.textContent =
            today.toLocaleDateString(
                "ar-EG",
                {
                    weekday: "long",
                    year: "numeric",
                    month: "long",
                    day: "numeric"
                }
            );


        /* =====================================================
           TIMER
        ===================================================== */

        let timeLeft = 45 * 60;

        let timerInterval = null;

        let timerRunning = false;


        function updateTimer() {

            const minutes =
                Math.floor(
                    timeLeft / 60
                );

            const seconds =
                timeLeft % 60;


            timerElement.textContent =
                String(minutes).padStart(
                    2,
                    "0"
                ) +
                ":" +
                String(seconds).padStart(
                    2,
                    "0"
                );

        }


        timerStart.addEventListener(
            "click",
            () => {

                if (timerRunning) {

                    clearInterval(
                        timerInterval
                    );

                    timerRunning = false;

                    timerStart.textContent =
                        "استمرار";

                    return;

                }


                timerRunning = true;

                timerStart.textContent =
                    "إيقاف مؤقت";


                timerInterval =
                    setInterval(
                        () => {

                            if (timeLeft > 0) {

                                timeLeft--;

                                updateTimer();

                            } else {

                                clearInterval(
                                    timerInterval
                                );

                                timerRunning =
                                    false;

                                timerStart.textContent =
                                    "ابدأ";

                                alert(
                                    "انتهت جلسة التركيز! 🎉"
                                );

                            }

                        },
                        1000
                    );

            }
        );


        timerReset.addEventListener(
            "click",
            () => {

                clearInterval(
                    timerInterval
                );

                timeLeft =
                    45 * 60;

                timerRunning =
                    false;

                timerStart.textContent =
                    "ابدأ";

                updateTimer();

            }
        );


        /* =====================================================
           INITIAL
        ===================================================== */

        updateTimer();
        updateProgress();

    </script>

</body>

</html>
