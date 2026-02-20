<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hiro Role Play | نسل بعدی گیمینگ</title>
    
    <!-- فونت‌های خفن -->
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@400;700;900&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Exo+2:wght@400;700;900&display=swap" rel="stylesheet">
    
    <style>
        /* ===== RESET & VARIABLES ===== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #ff0000;
            --primary-dark: #990000;
            --primary-glow: #ff3300;
            --secondary: #0066ff;
            --secondary-glow: #0099ff;
            --accent: #aa00ff;
            --accent-glow: #cc33ff;
            --dark: #030014;
            --darker: #000000;
            --neon-red: 255, 0, 0;
            --neon-blue: 0, 102, 255;
            --neon-purple: 170, 0, 255;
            
            /* انیمیشن‌های سه‌بعدی */
            --perspective: 1000px;
            --rotation: 5deg;
        }

        /* ===== BASE STYLES ===== */
        body {
            font-family: 'Exo 2', 'Rajdhani', 'Orbitron', sans-serif;
            color: #fff;
            background: var(--darker);
            overflow-x: hidden;
            line-height: 1.6;
            min-height: 100vh;
            position: relative;
        }

        /* پس زمینه سایبرپانک */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                linear-gradient(125deg, #000000 0%, #0a0015 40%, #15000a 80%, #000000 100%),
                repeating-linear-gradient(45deg, 
                    rgba(255, 0, 0, 0.02) 0px, 
                    rgba(255, 0, 0, 0.02) 2px,
                    rgba(0, 102, 255, 0.02) 2px, 
                    rgba(0, 102, 255, 0.02) 4px,
                    rgba(170, 0, 255, 0.02) 4px,
                    rgba(170, 0, 255, 0.02) 6px,
                    transparent 6px,
                    transparent 12px
                );
            pointer-events: none;
            z-index: 0;
            animation: matrix 20s linear infinite;
        }

        @keyframes matrix {
            0% { background-position: 0 0, 0 0; }
            100% { background-position: 100% 100%, 100% 100%; }
        }

        /* ذرات سه‌بعدی */
        .cyber-particle {
            position: fixed;
            width: 4px;
            height: 4px;
            background: linear-gradient(45deg, var(--primary), var(--secondary), var(--accent));
            border-radius: 50%;
            filter: blur(1px);
            pointer-events: none;
            z-index: 1;
            animation: float3D 15s linear infinite;
            transform-style: preserve-3d;
        }

        @keyframes float3D {
            0% {
                transform: translateZ(-500px) translateY(100vh) translateX(0) rotateX(0deg) rotateY(0deg);
                opacity: 0;
            }
            10% {
                opacity: 0.8;
            }
            90% {
                opacity: 0.8;
            }
            100% {
                transform: translateZ(500px) translateY(-100vh) translateX(100px) rotateX(360deg) rotateY(360deg);
                opacity: 0;
            }
        }

        /* خطوط سایبرپانک */
        .cyber-line {
            position: fixed;
            background: linear-gradient(90deg, transparent, var(--primary), var(--secondary), var(--accent), transparent);
            height: 2px;
            width: 100%;
            z-index: 1;
            animation: scan 8s linear infinite;
        }

        @keyframes scan {
            0% { transform: translateY(-50%) translateX(-100%); }
            100% { transform: translateY(-50%) translateX(100%); }
        }

        /* ===== PRELOADER ===== */
        #preloader {
            position: fixed;
            width: 100%;
            height: 100%;
            background: #000;
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 9999;
            transition: opacity 0.5s;
        }

        .cyber-loader {
            position: relative;
            width: 120px;
            height: 120px;
            perspective: 1000px;
        }

        .cube {
            width: 100%;
            height: 100%;
            position: absolute;
            transform-style: preserve-3d;
            animation: cubeRotate 5s infinite linear;
        }

        .cube div {
            position: absolute;
            width: 100%;
            height: 100%;
            border: 3px solid;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: 900;
            font-size: 24px;
            text-shadow: 0 0 20px currentColor;
        }

        .cube .front { transform: translateZ(60px); border-color: var(--primary); color: var(--primary); }
        .cube .back { transform: rotateY(180deg) translateZ(60px); border-color: var(--secondary); color: var(--secondary); }
        .cube .right { transform: rotateY(90deg) translateZ(60px); border-color: var(--accent); color: var(--accent); }
        .cube .left { transform: rotateY(-90deg) translateZ(60px); border-color: var(--primary-glow); color: var(--primary-glow); }
        .cube .top { transform: rotateX(90deg) translateZ(60px); border-color: var(--secondary-glow); color: var(--secondary-glow); }
        .cube .bottom { transform: rotateX(-90deg) translateZ(60px); border-color: var(--accent-glow); color: var(--accent-glow); }

        @keyframes cubeRotate {
            from { transform: rotateX(0deg) rotateY(0deg); }
            to { transform: rotateX(360deg) rotateY(360deg); }
        }

        /* ===== NAVBAR ===== */
        .navbar {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            width: 95%;
            max-width: 1300px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 35px;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(20px);
            z-index: 1000;
            border: 2px solid transparent;
            border-radius: 60px;
            background-clip: padding-box;
            animation: borderGlow 3s infinite;
            box-shadow: 0 0 30px rgba(255, 0, 0, 0.3);
        }

        @keyframes borderGlow {
            0%, 100% { border-color: var(--primary); box-shadow: 0 0 30px rgba(255, 0, 0, 0.3); }
            33% { border-color: var(--secondary); box-shadow: 0 0 30px rgba(0, 102, 255, 0.3); }
            66% { border-color: var(--accent); box-shadow: 0 0 30px rgba(170, 0, 255, 0.3); }
        }

        .logo {
            font-size: 32px;
            font-weight: 900;
            background: linear-gradient(45deg, var(--primary), var(--secondary), var(--accent));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 30px rgba(255, 0, 0, 0.5);
            font-family: 'Orbitron', sans-serif;
            letter-spacing: 4px;
            position: relative;
            animation: logoPulse 2s infinite;
        }

        @keyframes logoPulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .logo::before {
            content: '⚡';
            position: absolute;
            left: -30px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--primary);
            text-shadow: 0 0 20px var(--primary);
            animation: spin 3s linear infinite;
        }

        .logo::after {
            content: '⚡';
            position: absolute;
            right: -30px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--accent);
            text-shadow: 0 0 20px var(--accent);
            animation: spin 3s linear infinite reverse;
        }

        .navbar ul {
            display: flex;
            gap: 15px;
            list-style: none;
        }

        .navbar a {
            color: #fff;
            text-decoration: none;
            font-weight: 700;
            padding: 10px 22px;
            border-radius: 40px;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
            font-size: 15px;
            text-transform: uppercase;
            letter-spacing: 1px;
            border: 1px solid transparent;
            background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(5px);
            cursor: pointer;
        }

        .navbar a::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: 0.5s;
        }

        .navbar a:hover::before {
            left: 100%;
        }

        .navbar a:hover {
            background: linear-gradient(45deg, var(--primary), var(--accent));
            transform: scale(1.05) translateY(-2px);
            box-shadow: 0 0 20px var(--primary), 0 0 40px var(--accent);
            border-color: #fff;
        }

        /* لینک شاپ ویژه - بدون لینک */
        .navbar a.shop-link {
            background: linear-gradient(45deg, #ff0000, #ff0066, #ff00cc);
            color: #fff;
            font-weight: 900;
            border: 2px solid #fff;
            animation: shopPulse 1.5s infinite;
            position: relative;
            pointer-events: none;
            opacity: 0.9;
        }

        @keyframes shopPulse {
            0%, 100% { 
                box-shadow: 0 0 20px #ff0000, 0 0 40px #ff0066, 0 0 60px #ff00cc;
                transform: scale(1);
            }
            50% { 
                box-shadow: 0 0 30px #ff00cc, 0 0 60px #ff0000, 0 0 90px #ff0066;
                transform: scale(1.05);
            }
        }

        /* لینک انجمن - بدون لینک */
        .navbar a.forum-link {
            pointer-events: none;
            opacity: 0.9;
        }

        /* ===== HAMBURGER MENU ===== */
        .menu-toggle {
            display: none;
            flex-direction: column;
            gap: 8px;
            cursor: pointer;
            z-index: 1001;
        }

        .menu-toggle div {
            width: 35px;
            height: 4px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            border-radius: 4px;
            transition: all 0.3s;
            box-shadow: 0 0 10px var(--primary);
        }

        .menu-toggle.active div:nth-child(1) {
            transform: rotate(45deg) translate(10px, 10px);
            background: var(--secondary);
        }

        .menu-toggle.active div:nth-child(2) {
            opacity: 0;
            transform: translateX(-20px);
        }

        .menu-toggle.active div:nth-child(3) {
            transform: rotate(-45deg) translate(8px, -8px);
            background: var(--accent);
        }

        @media (max-width: 1000px) {
            .navbar ul {
                display: none;
                flex-direction: column;
                background: rgba(0, 0, 0, 0.95);
                backdrop-filter: blur(20px);
                position: absolute;
                top: 80px;
                left: 20px;
                right: 20px;
                padding: 25px;
                border-radius: 40px;
                border: 2px solid var(--primary);
                box-shadow: 0 0 40px rgba(255, 0, 0, 0.5);
            }

            .navbar ul.show {
                display: flex;
                animation: slideDown 0.3s ease;
            }

            @keyframes slideDown {
                from {
                    opacity: 0;
                    transform: translateY(-30px) scale(0.9);
                }
                to {
                    opacity: 1;
                    transform: translateY(0) scale(1);
                }
            }

            .menu-toggle {
                display: flex;
            }
        }

        /* ===== HERO SECTION ===== */
        .hero {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 20px;
            position: relative;
            z-index: 2;
            perspective: 1000px;
        }

        .hero h1 {
            font-size: clamp(60px, 12vw, 120px);
            font-weight: 900;
            font-family: 'Orbitron', sans-serif;
            text-transform: uppercase;
            background: linear-gradient(45deg, 
                var(--primary), 
                var(--secondary), 
                var(--accent), 
                var(--primary-glow), 
                var(--secondary-glow)
            );
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 
                0 0 30px rgba(255, 0, 0, 0.7),
                0 0 60px rgba(0, 102, 255, 0.5),
                0 0 90px rgba(170, 0, 255, 0.3);
            margin-bottom: 20px;
            letter-spacing: 8px;
            animation: titleRotate 5s infinite;
            transform-style: preserve-3d;
        }

        @keyframes titleRotate {
            0%, 100% { transform: rotateX(0deg) rotateY(0deg); }
            25% { transform: rotateX(5deg) rotateY(-5deg); }
            75% { transform: rotateX(-5deg) rotateY(5deg); }
        }

        .hero h2 {
            font-size: clamp(24px, 5vw, 32px);
            margin-bottom: 40px;
            color: transparent;
            background: linear-gradient(135deg, #fff, #ccc);
            -webkit-background-clip: text;
            position: relative;
        }

        #typing {
            color: #fff;
            text-shadow: 0 0 10px var(--primary), 0 0 20px var(--secondary);
            border-left: 4px solid var(--primary);
            padding-left: 20px;
            margin-left: 20px;
        }

        .glitch {
            position: relative;
        }

        .glitch::before,
        .glitch::after {
            content: attr(data-text);
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        .glitch::before {
            left: 2px;
            text-shadow: -2px 0 #ff0000;
            animation: glitch-1 2s infinite linear alternate-reverse;
        }

        .glitch::after {
            left: -2px;
            text-shadow: 2px 0 #0000ff;
            animation: glitch-2 2s infinite linear alternate-reverse;
        }

        @keyframes glitch-1 {
            0% { clip-path: inset(20% 0 30% 0); }
            20% { clip-path: inset(60% 0 10% 0); }
            40% { clip-path: inset(10% 0 80% 0); }
            60% { clip-path: inset(40% 0 50% 0); }
            80% { clip-path: inset(90% 0 5% 0); }
            100% { clip-path: inset(15% 0 70% 0); }
        }

        @keyframes glitch-2 {
            0% { clip-path: inset(30% 0 20% 0); }
            20% { clip-path: inset(80% 0 10% 0); }
            40% { clip-path: inset(5% 0 60% 0); }
            60% { clip-path: inset(20% 0 40% 0); }
            80% { clip-path: inset(50% 0 30% 0); }
            100% { clip-path: inset(70% 0 15% 0); }
        }

        .hero .btn {
            display: inline-block;
            padding: 20px 60px;
            background: linear-gradient(45deg, #ff0000, #ff6600, #ff00ff);
            color: #fff;
            text-decoration: none;
            border-radius: 60px;
            font-weight: 900;
            font-size: 22px;
            border: 3px solid #fff;
            box-shadow: 0 0 30px #ff0000, 0 0 60px #ff00ff;
            transition: all 0.3s;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            text-transform: uppercase;
            letter-spacing: 3px;
            transform-style: preserve-3d;
            animation: btnFloat 3s infinite;
        }

        @keyframes btnFloat {
            0%, 100% { transform: translateZ(0) scale(1); }
            50% { transform: translateZ(20px) scale(1.05); }
        }

        .hero .btn:hover {
            transform: translateZ(40px) scale(1.1);
            box-shadow: 0 0 40px #ff0000, 0 0 80px #ff00ff, 0 0 120px #0000ff;
        }

        /* ===== SECTIONS ===== */
        .section {
            padding: 120px 20px;
            text-align: center;
            position: relative;
            z-index: 2;
            perspective: 1000px;
        }

        .section::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: repeating-linear-gradient(45deg, 
                rgba(255, 0, 0, 0.02) 0px,
                rgba(255, 0, 0, 0.02) 20px,
                rgba(0, 102, 255, 0.02) 20px,
                rgba(0, 102, 255, 0.02) 40px,
                rgba(170, 0, 255, 0.02) 40px,
                rgba(170, 0, 255, 0.02) 60px
            );
            pointer-events: none;
        }

        .section h2 {
            font-size: 56px;
            font-weight: 900;
            margin-bottom: 70px;
            position: relative;
            display: inline-block;
            font-family: 'Orbitron', sans-serif;
            text-transform: uppercase;
            background: linear-gradient(135deg, #fff, #ff0000, #0066ff, #aa00ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 30px rgba(255, 0, 0, 0.5);
            animation: sectionTitle 4s infinite;
            transform-style: preserve-3d;
        }

        @keyframes sectionTitle {
            0%, 100% { transform: rotateY(0deg) scale(1); }
            50% { transform: rotateY(10deg) scale(1.1); }
        }

        .section h2::before,
        .section h2::after {
            content: '⚡';
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            font-size: 40px;
            animation: spark 1.5s infinite;
        }

        .section h2::before {
            left: -70px;
            color: var(--primary);
            text-shadow: 0 0 20px var(--primary);
        }

        .section h2::after {
            right: -70px;
            color: var(--accent);
            text-shadow: 0 0 20px var(--accent);
        }

        @keyframes spark {
            0%, 100% { opacity: 1; transform: translateY(-50%) scale(1); }
            50% { opacity: 0.5; transform: translateY(-50%) scale(1.5); }
        }

        /* ===== CARDS ===== */
        .cards {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 40px;
            max-width: 1400px;
            margin: 0 auto;
            perspective: 1000px;
        }

        .card {
            padding: 40px 30px;
            border-radius: 50px;
            width: 280px;
            font-weight: 700;
            font-size: 18px;
            background: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(10px);
            border: 2px solid transparent;
            transition: all 0.4s;
            cursor: default;
            position: relative;
            overflow: hidden;
            transform-style: preserve-3d;
            animation: cardFloat 6s infinite;
        }

     
