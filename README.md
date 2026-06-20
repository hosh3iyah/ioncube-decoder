<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>IonCube + SourceGuardian Decoder</title>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" />
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(145deg, #0d0f14 0%, #1a1e26 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 2rem 1rem;
        }

        .card {
            max-width: 820px;
            width: 100%;
            background: rgba(22, 27, 34, 0.85);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.06);
            border-radius: 48px;
            padding: 2.8rem 2.2rem;
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.8), 0 0 0 1px rgba(255, 255, 255, 0.03);
            transition: all 0.3s ease;
        }

        .card:hover {
            border-color: rgba(0, 200, 255, 0.15);
            box-shadow: 0 40px 80px rgba(0, 0, 0, 0.9), 0 0 0 1px rgba(0, 200, 255, 0.1);
        }

        /* هدر */
        .header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 1rem;
            margin-bottom: 2rem;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 0.6rem;
        }

        .logo i {
            font-size: 2.2rem;
            color: #00d4ff;
            filter: drop-shadow(0 0 8px rgba(0, 212, 255, 0.4));
        }

        .logo span {
            font-size: 1.5rem;
            font-weight: 700;
            background: linear-gradient(135deg, #f0f9ff, #a5d8ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .badge {
            background: rgba(0, 212, 255, 0.12);
            border: 1px solid rgba(0, 212, 255, 0.2);
            border-radius: 100px;
            padding: 0.4rem 1.2rem;
            font-size: 0.8rem;
            font-weight: 600;
            color: #b3e5ff;
            letter-spacing: 0.3px;
            backdrop-filter: blur(4px);
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .badge i {
            font-size: 0.75rem;
            color: #00d4ff;
        }

        .title {
            font-size: 2.1rem;
            font-weight: 700;
            color: #ffffff;
            margin: 1.2rem 0 0.3rem 0;
            letter-spacing: -0.5px;
        }

        .title span {
            background: linear-gradient(to right, #00d4ff, #7b61ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .sub {
            color: #a0b3cc;
            font-size: 1rem;
            font-weight: 400;
            border-right: 3px solid #00d4ff;
            padding-right: 14px;
            margin-bottom: 2rem;
            line-height: 1.6;
        }

        /* لیست نسخه‌ها */
        .version-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 10px 12px;
            margin: 1.8rem 0 2.2rem 0;
            padding: 1.2rem 1.5rem;
            background: rgba(0, 0, 0, 0.25);
            border-radius: 40px;
            border: 1px solid rgba(255, 255, 255, 0.03);
        }

        .version-item {
            background: rgba(255, 255, 255, 0.04);
            border-radius: 60px;
            padding: 0.3rem 1.2rem;
            font-size: 0.9rem;
            font-weight: 500;
            color: #c8d9f0;
            border: 1px solid rgba(255, 255, 255, 0.04);
            transition: all 0.2s;
            backdrop-filter: blur(4px);
            letter-spacing: 0.2px;
        }

        .version-item:hover {
            background: rgba(0, 212, 255, 0.08);
            border-color: rgba(0, 212, 255, 0.2);
            color: #fff;
            transform: translateY(-2px);
        }

        .version-item i {
            margin-left: 6px;
            font-size: 0.75rem;
            color: #00d4ff;
            opacity: 0.6;
        }

        /* بخش قیمت و ویژگی */
        .pricing-box {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            background: rgba(0, 20, 40, 0.4);
            border-radius: 60px;
            padding: 0.8rem 2rem 0.8rem 1.8rem;
            border: 1px solid rgba(0, 212, 255, 0.1);
            margin: 1.5rem 0 2rem 0;
            backdrop-filter: blur(4px);
        }

        .price {
            display: flex;
            align-items: baseline;
            gap: 6px;
        }

        .price .number {
            font-size: 2.4rem;
            font-weight: 800;
            color: #fff;
            letter-spacing: -0.5px;
        }

        .price .currency {
            font-size: 1.2rem;
            font-weight: 600;
            color: #a5d8ff;
        }

        .price .period {
            font-size: 0.9rem;
            color: #8899bb;
            margin-right: 6px;
        }

        .unlimited {
            display: flex;
            align-items: center;
            gap: 8px;
            color: #b3e5ff;
            background: rgba(0, 212, 255, 0.06);
            padding: 0.4rem 1.4rem;
            border-radius: 40px;
            border: 1px solid rgba(0, 212, 255, 0.08);
            font-weight: 500;
            font-size: 0.95rem;
        }

        .unlimited i {
            color: #00d4ff;
            font-size: 1rem;
        }

        /* دکمه تلگرام */
        .telegram-btn {
            display: inline-flex;
            align-items: center;
            gap: 14px;
            background: linear-gradient(135deg, #0088cc, #005f8a);
            padding: 0.9rem 2.5rem;
            border-radius: 80px;
            color: #fff;
            font-weight: 600;
            font-size: 1.1rem;
            text-decoration: none;
            transition: all 0.25s ease;
            border: 1px solid rgba(255, 255, 255, 0.08);
            box-shadow: 0 8px 20px rgba(0, 136, 204, 0.25);
            margin-top: 0.5rem;
            width: fit-content;
        }

        .telegram-btn i {
            font-size: 1.5rem;
            transition: transform 0.2s;
        }

        .telegram-btn:hover {
            transform: translateY(-3px) scale(1.02);
            background: linear-gradient(135deg, #0099dd, #006fa0);
            box-shadow: 0 12px 30px rgba(0, 136, 204, 0.4);
            border-color: rgba(255, 255, 255, 0.15);
        }

        .telegram-btn:hover i {
            transform: rotate(-6deg) scale(1.1);
        }

        .footer-note {
            margin-top: 2.2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 0.8rem;
            border-top: 1px solid rgba(255, 255, 255, 0.04);
            padding-top: 1.8rem;
        }

        .footer-note small {
            color: #68748e;
            font-size: 0.8rem;
            letter-spacing: 0.3px;
        }

        .footer-note small i {
            margin-left: 6px;
            color: #00d4ff;
            opacity: 0.5;
        }

        .support-tag {
            display: flex;
            align-items: center;
            gap: 10px;
            color: #a5b9d6;
            font-size: 0.9rem;
        }

        .support-tag i {
            color: #00d4ff;
        }

        /* ریسپانسیو */
        @media (max-width: 600px) {
            .card {
                padding: 1.8rem 1.2rem;
                border-radius: 32px;
            }

            .title {
                font-size: 1.6rem;
            }

            .pricing-box {
                flex-direction: column;
                align-items: stretch;
                gap: 12px;
                border-radius: 40px;
                padding: 1.2rem 1.5rem;
            }

            .price .number {
                font-size: 2rem;
            }

            .telegram-btn {
                width: 100%;
                justify-content: center;
                padding: 0.9rem 1.5rem;
            }

            .version-grid {
                padding: 1rem 1.2rem;
                gap: 8px;
            }

            .header {
                flex-direction: column;
                align-items: flex-start;
            }

            .badge {
                align-self: flex-start;
            }

            .unlimited {
                justify-content: center;
            }
        }

        @media (max-width: 400px) {
            .version-item {
                font-size: 0.75rem;
                padding: 0.2rem 0.9rem;
            }

            .title {
                font-size: 1.3rem;
            }
        }
    </style>
</head>
<body>
    <div class="card">

        <!-- هدر -->
        <div class="header">
            <div class="logo">
                <i class="fas fa-shield-halved"></i>
                <span>Decoder</span>
            </div>
            <div class="badge">
                <i class="fas fa-circle-check"></i> فعال ۲۴/۷
            </div>
        </div>

        <!-- عنوان اصلی -->
        <h1 class="title">
            <span>IonCube</span> + <span>SourceGuardian</span>
        </h1>
        <div class="sub">
            <i class="fas fa-chevron-left" style="margin-left:8px; font-size:0.7rem; opacity:0.5;"></i>
            دیکد کردن حرفه‌ای فایل‌های PHP در تمام نسخه‌ها
        </div>

        <!-- لیست نسخه‌های پشتیبانی شده -->
        <div class="version-grid">
            <span class="version-item"><i class="fas fa-check-circle"></i> PHP 5.0</span>
            <span class="version-item"><i class="fas fa-check-circle"></i> PHP 5.3</span>
            <span class="version-item"><i class="fas fa-check-circle"></i> PHP 5.4</span>
            <span class="version-item"><i class="fas fa-check-circle"></i> PHP 5.5</span>
            <span class="version-item"><i class="fas fa-check-circle"></i> PHP 5.6</span>
            <span class="version-item"><i class="fas fa-check-circle"></i> PHP 7.0</span>
            <span class="version-item"><i class="fas fa-check-circle"></i> PHP 7.1</span>
            <span class="version-item"><i class="fas fa-check-circle"></i> PHP 7.2</span>
            <span class="version-item"><i class="fas fa-check-circle"></i> PHP 7.4</span>
            <span class="version-item"><i class="fas fa-check-circle"></i> PHP 8.1</span>
            <span class="version-item"><i class="fas fa-check-circle"></i> PHP 8.2</span>
            <span class="version-item"><i class="fas fa-check-circle"></i> PHP 8.3</span>
        </div>

        <!-- قیمت و ویژگی unlimited -->
        <div class="pricing-box">
            <div class="price">
                <span class="number">۱۵</span>
                <span class="currency">$</span>
                <span class="period">/ ماهانه</span>
            </div>
            <div class="unlimited">
                <i class="fas fa-infinity"></i>
                تعداد فایل‌ها نامحدود
            </div>
        </div>

        <!-- دکمه تماس با تلگرام -->
        <a href="https://t.me/hosh3iyah" target="_blank" class="telegram-btn">
            <i class="fab fa-telegram-plane"></i>
            تماس در تلگرام : @HOSH3IYAH
        </a>

        <!-- فوتر -->
        <div class="footer-note">
            <small>
                <i class="fas fa-lock"></i> رمزگشایی امن &bull; بدون محدودیت
            </small>
            <div class="support-tag">
                <i class="fas fa-headset"></i>
                پشتیبانی ۲۴ ساعته
            </div>
        </div>

    </div>
</body>
</html>
