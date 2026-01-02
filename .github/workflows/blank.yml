<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hubs Shop - Покупка геймпассов и Robux</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { background: linear-gradient(135deg, #0d1b2a 0%, #1b263b 100%); color: #e0e1dd; min-height: 100vh; padding: 15px; }
        .container { max-width: 1200px; margin: 0 auto; }
        .header { display: flex; justify-content: space-between; align-items: center; padding: 20px 0; margin-bottom: 25px; border-bottom: 2px solid #778da9; }
        .logo-container { display: flex; align-items: center; gap: 15px; }
        .logo { font-size: 32px; font-weight: 800; color: #e0e1dd; text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3); display: flex; align-items: center; gap: 10px; }
        .logo-icon { width: 40px; height: 40px; background: linear-gradient(135deg, #415a77, #778da9); border-radius: 8px; display: flex; align-items: center; justify-content: center; font-weight: bold; color: #e0e1dd; }
        .admin-btn, .robux-btn { background: linear-gradient(135deg, #415a77, #778da9); color: white; border: none; padding: 10px 20px; border-radius: 8px; cursor: pointer; font-weight: 600; transition: all 0.3s; display: flex; align-items: center; gap: 8px; }
        .admin-btn:hover, .robux-btn:hover { background: linear-gradient(135deg, #778da9, #415a77); transform: translateY(-2px); }
        .header-buttons { display: flex; gap: 10px; }
        .step-indicator { display: flex; gap: 30px; margin-bottom: 25px; justify-content: center; }
        .step { display: flex; flex-direction: column; align-items: center; position: relative; }
        .step-circle { width: 40px; height: 40px; border-radius: 50%; background-color: #415a77; display: flex; align-items: center; justify-content: center; font-weight: bold; color: #e0e1dd; border: 2px solid #778da9; margin-bottom: 8px; font-size: 18px; transition: all 0.3s; z-index: 2; }
        .step.active .step-circle { background-color: #778da9; color: #0d1b2a; border-color: #e0e1dd; box-shadow: 0 0 15px rgba(119, 141, 169, 0.5); }
        .step-text { font-size: 14px; color: #778da9; font-weight: 600; white-space: nowrap; }
        .step.active .step-text { color: #e0e1dd; }
        .step:not(:last-child)::after { content: ''; position: absolute; top: 20px; left: 50px; width: 30px; height: 2px; background-color: #415a77; z-index: 1; }
        .step.active:not(:last-child)::after { background-color: #778da9; }
        .page { display: none; background: linear-gradient(135deg, #1b263b, #0d1b2a); border-radius: 16px; padding: 30px; margin-bottom: 25px; box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3); border: 1px solid #415a77; position: relative; overflow: hidden; }
        .page::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 5px; background: linear-gradient(to right, #415a77, #778da9, #415a77); }
        .page.active { display: block; animation: fadeIn 0.4s ease; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .page-title { text-align: center; font-size: 32px; margin-bottom: 10px; color: #e0e1dd; font-weight: 800; text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5); position: relative; display: inline-block; left: 50%; transform: translateX(-50%); padding: 0 20px; }
        .page-title::after { content: ''; position: absolute; bottom: -5px; left: 0; width: 100%; height: 3px; background: linear-gradient(to right, transparent, #778da9, transparent); }
        .page-subtitle { text-align: center; font-size: 18px; margin-bottom: 25px; color: #778da9; font-weight: 500; }
        .game-carousel-container { position: relative; width: 100%; height: 400px; overflow: hidden; margin: 30px auto; border-radius: 16px; border: 3px solid #415a77; background: linear-gradient(135deg, #0d1b2a, #1b263b); box-shadow: 0 8px 25px rgba(0, 0, 0, 0.5); }
        .game-carousel { display: flex; flex-direction: column; transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1); height: 100%; }
        .game-item { flex: 0 0 100%; height: 100%; display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 30px; background: linear-gradient(135deg, #1b263b, #0d1b2a); cursor: pointer; transition: all 0.3s; border: 3px solid transparent; position: relative; }
        .game-item:hover { background: linear-gradient(135deg, #0d1b2a, #1b263b); transform: scale(1.01); }
        .game-item.selected { border-color: #778da9; background: linear-gradient(135deg, #0d1b2a, #1b263b); box-shadow: inset 0 0 20px rgba(119, 141, 169, 0.3), 0 5px 15px rgba(119, 141, 169, 0.2); }
        .game-preview { width: 100%; height: 250px; object-fit: cover; border-radius: 12px; margin-bottom: 20px; box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5); border: 3px solid #415a77; }
        .game-title { font-size: 28px; font-weight: 800; color: #e0e1dd; margin-bottom: 10px; text-align: center; text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5); }
        .game-rating { font-size: 18px; color: #ffb703; font-weight: 700; background-color: rgba(27, 38, 59, 0.8); padding: 8px 20px; border-radius: 20px; display: inline-block; border: 1px solid #ffb703; }
        .carousel-controls { display: flex; justify-content: center; margin-top: 20px; }
        .carousel-btn { background: linear-gradient(135deg, #415a77, #778da9); color: white; border: none; width: 55px; height: 55px; border-radius: 50%; font-size: 24px; cursor: pointer; margin: 0 12px; transition: all 0.3s; box-shadow: 0 5px 15px rgba(65, 90, 119, 0.4); display: flex; align-items: center; justify-content: center; }
        .carousel-btn:hover { background: linear-gradient(135deg, #778da9, #415a77); transform: translateY(-3px); box-shadow: 0 8px 20px rgba(65, 90, 119, 0.6); }
        .carousel-btn:disabled { background: linear-gradient(135deg, #415a77, #1b263b); cursor: not-allowed; transform: none; box-shadow: none; }
        .carousel-btn:disabled:hover { background: linear-gradient(135deg, #415a77, #1b263b); transform: none; box-shadow: none; }
        .gamepass-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 25px; margin-top: 30px; }
        @media (max-width: 768px) { .gamepass-grid { grid-template-columns: repeat(2, 1fr); } }
        @media (max-width: 480px) { .gamepass-grid { grid-template-columns: 1fr; } }
        .gamepass-item { background: linear-gradient(145deg, #1b263b, #0d1b2a); border-radius: 16px; padding: 0; cursor: pointer; transition: all 0.3s; border: 2px solid #415a77; overflow: hidden; box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4); position: relative; display: flex; flex-direction: column; }
        .gamepass-item:hover { transform: translateY(-8px); box-shadow: 0 15px 30px rgba(0, 0, 0, 0.6); border-color: #778da9; }
        .gamepass-item.selected { border-color: #ffb703; box-shadow: 0 15px 30px rgba(255, 183, 3, 0.4); background: linear-gradient(145deg, #0d1b2a, #1b263b); }
        .gamepass-image-container { width: 100%; height: 180px; position: relative; overflow: hidden; }
        .gamepass-img { width: 100%; height: 100%; object-fit: cover; border-bottom: 2px solid #415a77; }
        .robux-price-overlay { position: absolute; bottom: 10px; left: 50%; transform: translateX(-50%); background: rgba(0, 0, 0, 0.8); color: #ffd700; padding: 5px 15px; border-radius: 20px; font-weight: bold; font-size: 18px; border: 1px solid #ffd700; z-index: 2; }
        .gamepass-name { font-size: 22px; font-weight: 800; color: #e0e1dd; text-align: center; padding: 15px; background-color: rgba(27, 38, 59, 0.8); }
        .ruble-price { text-align: center; font-size: 22px; font-weight: 800; color: #ffb703; padding: 15px 0; border-top: 2px dashed #415a77; background-color: rgba(13, 27, 42, 0.9); }
        .selected-badge { position: absolute; top: 10px; right: 10px; background: linear-gradient(135deg, #415a77, #778da9); color: white; width: 35px; height: 35px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; box-shadow: 0 3px 8px rgba(0, 0, 0, 0.5); opacity: 0; transition: opacity 0.3s; font-size: 18px; z-index: 3; }
        .gamepass-item.selected .selected-badge { opacity: 1; }
        .next-btn { display: block; margin: 40px auto 0; background: linear-gradient(to right, #415a77, #778da9); color: white; border: none; padding: 18px 50px; font-size: 18px; font-weight: 700; border-radius: 12px; cursor: pointer; transition: all 0.3s; box-shadow: 0 8px 20px rgba(65, 90, 119, 0.4); text-transform: uppercase; letter-spacing: 1px; position: relative; overflow: hidden; }
        .next-btn::after { content: ''; position: absolute; top: -50%; left: -50%; width: 200%; height: 200%; background: linear-gradient(to right, transparent, rgba(255, 255, 255, 0.2), transparent); transform: rotate(30deg); transition: all 0.5s; }
        .next-btn:hover { transform: translateY(-4px); box-shadow: 0 12px 25px rgba(65, 90, 119, 0.6); }
        .next-btn:hover::after { left: 100%; }
        .next-btn:disabled { background: linear-gradient(to right, #415a77, #1b263b); cursor: not-allowed; transform: none; box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3); }
        .search-container { max-width: 600px; margin: 30px auto; text-align: center; }
        .search-box { display: flex; margin-bottom: 30px; box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4); border-radius: 12px; overflow: hidden; border: 2px solid #415a77; }
        .search-input { flex: 1; padding: 18px 20px; border: none; font-size: 16px; background-color: #0d1b2a; color: #e0e1dd; border-right: 1px solid #415a77; }
        .search-input::placeholder { color: #778da9; }
        .search-btn { padding: 0 30px; background: linear-gradient(to right, #415a77, #778da9); color: white; border: none; font-size: 16px; font-weight: 700; cursor: pointer; transition: all 0.3s; }
        .search-btn:hover { background: linear-gradient(to right, #778da9, #415a77); }
        .user-results { display: flex; flex-direction: column; gap: 15px; margin-top: 30px; }
        .user-item { display: flex; align-items: center; background: linear-gradient(135deg, #1b263b, #0d1b2a); padding: 18px; border-radius: 12px; cursor: pointer; transition: all 0.3s; border: 2px solid #415a77; box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3); }
        .user-item:hover { background: linear-gradient(135deg, #0d1b2a, #1b263b); transform: translateX(5px); border-color: #778da9; }
        .user-item.selected { border-color: #ffb703; background: linear-gradient(135deg, #0d1b2a, #1b263b); box-shadow: 0 8px 20px rgba(255, 183, 3, 0.3); }
        .user-avatar { width: 55px; height: 55px; border-radius: 50%; margin-right: 18px; background: linear-gradient(135deg, #415a77, #778da9); display: flex; align-items: center; justify-content: center; font-size: 22px; color: white; font-weight: 700; box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5); }
        .user-name { font-size: 18px; font-weight: 700; color: #e0e1dd; }
        .code-container { text-align: center; padding: 40px 30px; background: linear-gradient(145deg, #1b263b, #0d1b2a); border-radius: 20px; max-width: 600px; margin: 0 auto; border: 2px solid #415a77; box-shadow: 0 12px 30px rgba(0, 0, 0, 0.5); position: relative; overflow: hidden; }
        .code-container::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 5px; background: linear-gradient(to right, #415a77, #778da9, #415a77); }
        .code-title { font-size: 26px; margin-bottom: 20px; color: #e0e1dd; font-weight: 800; }
        .code { background: linear-gradient(135deg, #0d1b2a, #1b263b); padding: 25px; border-radius: 15px; font-size: 36px; letter-spacing: 5px; font-weight: 900; color: #ffb703; margin: 30px 0; border: 3px dashed #ffb703; font-family: 'Courier New', monospace; text-shadow: 0 2px 4px rgba(0, 0, 0, 0.5); box-shadow: inset 0 0 20px rgba(0, 0, 0, 0.5), 0 8px 20px rgba(0, 0, 0, 0.3); }
        .instructions { background: linear-gradient(135deg, #1b263b, #0d1b2a); padding: 25px; border-radius: 15px; margin-top: 35px; text-align: left; border-left: 5px solid #ffb703; box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3); }
        .instructions h3 { color: #e0e1dd; margin-bottom: 15px; font-size: 22px; font-weight: 800; background: #3498db; color: #f1c40f; padding: 10px; border-radius: 5px; text-align: center; }
        .instructions ol { padding-left: 25px; line-height: 1.7; }
        .instructions li { margin-bottom: 12px; font-size: 16px; color: #778da9; font-weight: 500; }
        .instructions li strong { color: #e0e1dd; }
        .action-buttons { display: flex; justify-content: center; gap: 20px; margin-top: 25px; flex-wrap: wrap; }
        .telegram-contact, .pdf-btn { display: inline-flex; align-items: center; gap: 12px; background: linear-gradient(to right, #415a77, #778da9); color: white; padding: 15px 30px; border-radius: 12px; text-decoration: none; font-weight: 800; transition: all 0.3s; box-shadow: 0 8px 20px rgba(65, 90, 119, 0.4); font-size: 18px; border: none; cursor: pointer; }
        .telegram-contact:hover, .pdf-btn:hover { background: linear-gradient(to right, #778da9, #415a77); transform: translateY(-3px); box-shadow: 0 12px 25px rgba(65, 90, 119, 0.6); }
        .pdf-btn { background: linear-gradient(to right, #ffb703, #fb8500); }
        .pdf-btn:hover { background: linear-gradient(to right, #fb8500, #ffb703); }
        .footer { text-align: center; margin-top: 40px; padding-top: 20px; border-top: 2px solid #415a77; color: #778da9; font-size: 14px; font-weight: 500; }
        .creator { position: absolute; bottom: 10px; left: 10px; color: #778da9; font-size: 12px; }
        .next-btn:active, .carousel-btn:active, .admin-btn-submit:active, .telegram-contact:active, .pdf-btn:active, .search-btn:active { outline: 3px solid #00ffaa; outline-offset: 2px; }
        .robux-container { text-align: center; padding: 40px 30px; background: linear-gradient(145deg, #1b263b, #0d1b2a); border-radius: 20px; max-width: 800px; margin: 0 auto; border: 2px solid #415a77; box-shadow: 0 12px 30px rgba(0, 0, 0, 0.5); position: relative; overflow: hidden; }
        .robux-container::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 5px; background: linear-gradient(to right, #415a77, #778da9, #415a77); }
        .robux-available { font-size: 24px; color: #ffb703; font-weight: bold; margin-bottom: 30px; background: rgba(0, 0, 0, 0.3); padding: 15px; border-radius: 12px; border: 2px solid #ffb703; display: flex; align-items: center; justify-content: center; gap: 10px; }
        .robux-available img { height: 30px; }
        .robux-packages { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; margin: 30px 0; }
        @media (max-width: 768px) { .robux-packages { grid-template-columns: repeat(2, 1fr); } }
        @media (max-width: 480px) { .robux-packages { grid-template-columns: 1fr; } }
        .robux-package { background: linear-gradient(145deg, #1b263b, #0d1b2a); border-radius: 16px; padding: 25px 15px; cursor: pointer; transition: all 0.3s; border: 2px solid #415a77; box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4); position: relative; }
        .robux-package:hover { transform: translateY(-8px); box-shadow: 0 15px 30px rgba(0, 0, 0, 0.6); border-color: #778da9; }
        .robux-package.selected { border-color: #ffb703; box-shadow: 0 15px 30px rgba(255, 183, 3, 0.4); background: linear-gradient(145deg, #0d1b2a, #1b263b); }
        .robux-amount { font-size: 28px; font-weight: 800; color: #e0e1dd; text-align: center; margin-bottom: 10px; display: flex; align-items: center; justify-content: center; gap: 5px; }
        .robux-amount img { height: 30px; }
        .robux-price { font-size: 22px; font-weight: 800; color: #ffb703; text-align: center; }
        .robux-summary { display: flex; justify-content: space-around; margin: 30px 0; padding: 25px; background: rgba(27, 38, 59, 0.8); border-radius: 16px; border: 2px solid #415a77; }
        .summary-item { text-align: center; }
        .summary-label { font-size: 18px; color: #778da9; margin-bottom: 10px; font-weight: 600; }
        .summary-value { font-size: 32px; font-weight: 800; color: #ffb703; display: flex; align-items: center; justify-content: center; gap: 5px; }
        .summary-value img { height: 35px; }
        .promo-section { margin: 30px 0; padding: 25px; background: rgba(27, 38, 59, 0.8); border-radius: 16px; border: 2px solid #415a77; text-align: center; }
        .promo-input { background: #0d1b2a; border: 2px solid #415a77; border-radius: 8px; padding: 12px; color: #e0e1dd; font-size: 16px; width: 250px; margin-right: 10px; }
        .promo-btn { background: linear-gradient(to right, #415a77, #778da9); color: white; border: none; padding: 12px 25px; border-radius: 8px; cursor: pointer; font-weight: 600; transition: all 0.3s; }
        .promo-btn:hover { background: linear-gradient(to right, #778da9, #415a77); }
        .promo-link { display: block; margin-top: 15px; color: #3498db; text-decoration: none; font-weight: 600; }
        .promo-link:hover { text-decoration: underline; }
        .admin-panel { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(13, 27, 42, 0.95); z-index: 1000; padding: 20px; overflow-y: auto; }
        .admin-panel.active { display: block; }
        .admin-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 30px; padding-bottom: 15px; border-bottom: 2px solid #415a77; }
        .admin-title { font-size: 28px; color: #e0e1dd; font-weight: 800; }
        .close-admin { background: linear-gradient(135deg, #415a77, #778da9); color: white; border: none; padding: 10px 20px; border-radius: 8px; cursor: pointer; font-weight: 600; transition: all 0.3s; }
        .close-admin:hover { background: linear-gradient(135deg, #778da9, #415a77); }
        .admin-tabs { display: flex; gap: 10px; margin-bottom: 30px; border-bottom: 2px solid #415a77; padding-bottom: 10px; flex-wrap: wrap; }
        .admin-tab { background: linear-gradient(135deg, #415a77, #1b263b); color: #e0e1dd; border: none; padding: 12px 24px; border-radius: 8px 8px 0 0; cursor: pointer; font-weight: 600; transition: all 0.3s; }
        .admin-tab.active { background: linear-gradient(135deg, #778da9, #415a77); color: #0d1b2a; }
        .admin-tab:hover { background: linear-gradient(135deg, #778da9, #415a77); }
        .admin-content { display: none; }
        .admin-content.active { display: block; }
        .admin-section { background: linear-gradient(135deg, #1b263b, #0d1b2a); border-radius: 12px; padding: 25px; margin-bottom: 25px; border: 1px solid #415a77; box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3); }
        .admin-section-title { font-size: 22px; color: #e0e1dd; margin-bottom: 20px; font-weight: 700; border-bottom: 2px solid #415a77; padding-bottom: 10px; }
        .admin-form { display: flex; flex-direction: column; gap: 15px; }
        .form-group { display: flex; flex-direction: column; gap: 8px; }
        .form-label { color: #e0e1dd; font-weight: 600; }
        .form-input { background: #0d1b2a; border: 2px solid #415a77; border-radius: 8px; padding: 12px; color: #e0e1dd; font-size: 16px; }
        .form-input:focus { outline: none; border-color: #778da9; }
        .admin-btn-submit { background: linear-gradient(135deg, #415a77, #778da9); color: white; border: none; padding: 15px; border-radius: 8px; cursor: pointer; font-weight: 600; font-size: 16px; transition: all 0.3s; margin-top: 10px; }
        .admin-btn-submit:hover { background: linear-gradient(135deg, #778da9, #415a77); transform: translateY(-2px); }
        .codes-list { display: flex; flex-direction: column; gap: 15px; }
        .code-item { background: linear-gradient(135deg, #1b263b, #0d1b2a); border-radius: 10px; padding: 20px; border: 1px solid #415a77; display: flex; justify-content: space-between; align-items: center; }
        .code-info { display: flex; flex-direction: column; gap: 5px; }
        .code-value { font-size: 20px; font-weight: 800; color: #ffb703; font-family: 'Courier New', monospace; }
        .code-details { color: #778da9; font-size: 14px; }
        .code-status { padding: 5px 15px; border-radius: 20px; font-weight: 600; font-size: 14px; }
        .status-used { background: rgba(255, 0, 0, 0.2); color: #ff6b6b; border: 1px solid #ff6b6b; }
        .status-active { background: rgba(0, 255, 0, 0.2); color: #4ade80; border: 1px solid #4ade80; }
        .empty-list { text-align: center; color: #778da9; padding: 40px; font-size: 18px; }
        .list-container { max-height: 400px; overflow-y: auto; margin-top: 20px; border: 1px solid #415a77; border-radius: 8px; padding: 10px; }
        .list-item { background: rgba(27, 38, 59, 0.8); border-radius: 8px; padding: 15px; margin-bottom: 10px; display: flex; justify-content: space-between; align-items: center; border: 1px solid #415a77; }
        .list-item-info { display: flex; flex-direction: column; gap: 5px; }
        .list-item-name { font-size: 18px; font-weight: 600; color: #e0e1dd; }
        .list-item-details { font-size: 14px; color: #778da9; }
        .delete-btn { background: linear-gradient(135deg, #ff6b6b, #ff4757); color: white; border: none; padding: 8px 15px; border-radius: 6px; cursor: pointer; font-weight: 600; transition: all 0.3s; }
        .delete-btn:hover { background: linear-gradient(135deg, #ff4757, #ff6b6b); transform: translateY(-2px); }
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(13, 27, 42, 0.95); z-index: 1001; align-items: center; justify-content: center; }
        .modal.active { display: flex; }
        .modal-content { background: linear-gradient(135deg, #1b263b, #0d1b2a); border-radius: 16px; padding: 40px; max-width: 500px; width: 90%; border: 2px solid #415a77; box-shadow: 0 15px 35px rgba(0, 0, 0, 0.5); }
        .modal-title { font-size: 24px; color: #e0e1dd; margin-bottom: 20px; text-align: center; font-weight: 800; }
        .error-message { color: #ff6b6b; text-align: center; margin-top: 10px; font-weight: 600; }
        .pdf-content { display: none; }
        .pdf-preview { background: white; color: #000; padding: 40px; max-width: 800px; margin: 0 auto; border-radius: 10px; }
        .pdf-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 30px; padding-bottom: 20px; border-bottom: 3px solid #415a77; }
        .pdf-logo { display: flex; align-items: center; gap: 15px; }
        .pdf-logo-icon { width: 60px; height: 60px; background: linear-gradient(135deg, #415a77, #778da9); border-radius: 10px; display: flex; align-items: center; justify-content: center; font-weight: bold; color: white; font-size: 24px; }
        .pdf-shop-name { font-size: 32px; font-weight: 800; color: #1b263b; }
        .pdf-date { color: #666; font-size: 14px; }
        .pdf-main { text-align: center; margin: 40px 0; }
        .pdf-title { font-size: 28px; color: #1b263b; margin-bottom: 20px; font-weight: 800; }
        .pdf-code { font-size: 48px; font-weight: 900; color: #ffb703; margin: 30px 0; padding: 20px; border: 3px dashed #415a77; border-radius: 10px; background: #f5f5f5; font-family: 'Courier New', monospace; }
        .pdf-details { background: #f5f5f5; padding: 25px; border-radius: 10px; margin: 30px 0; }
        .pdf-detail-row { display: flex; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid #ddd; }
        .pdf-detail-row:last-child { border-bottom: none; }
        .pdf-footer { margin-top: 50px; padding-top: 20px; border-top: 2px solid #415a77; color: #666; font-size: 12px; text-align: right; }
        .info-message { text-align: center; background: linear-gradient(135deg, rgba(65, 90, 119, 0.1), rgba(119, 141, 169, 0.1)); padding: 15px; border-radius: 12px; margin: 20px 0; border-left: 5px solid #415a77; color: #e0e1dd; font-weight: 600; font-size: 15px; box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2); }
        .empty-message { text-align: center; padding: 50px 30px; color: #778da9; font-size: 18px; font-weight: 600; background: linear-gradient(135deg, rgba(27, 38, 59, 0.5), rgba(13, 27, 42, 0.5)); border-radius: 12px; border: 2px dashed #415a77; }
        .page-navigation { text-align: center; margin-top: 20px; }
        .page-btn { background: linear-gradient(135deg, #415a77, #778da9); color: white; border: none; padding: 12px 25px; border-radius: 8px; cursor: pointer; font-weight: 600; transition: all 0.3s; margin: 0 10px; }
        .page-btn:hover { background: linear-gradient(135deg, #778da9, #415a77); transform: translateY(-2px); }
        .robux-details { text-align: left; margin: 20px 0; padding: 20px; background: rgba(27, 38, 59, 0.8); border-radius: 12px; border: 2px solid #415a77; }
        .robux-detail-row { display: flex; justify-content: space-between; margin: 10px 0; padding: 10px 0; border-bottom: 1px solid #415a77; }
        .robux-detail-row:last-child { border-bottom: none; }
        .custom-robux-container { margin: 30px 0; padding: 25px; background: rgba(27, 38, 59, 0.8); border-radius: 16px; border: 2px solid #415a77; text-align: center; }
        .custom-robux-input { background: #0d1b2a; border: 2px solid #415a77; border-radius: 8px; padding: 12px; color: #e0e1dd; font-size: 18px; width: 200px; margin-right: 10px; text-align: center; }
        .custom-robux-btn { background: linear-gradient(to right, #415a77, #778da9); color: white; border: none; padding: 12px 25px; border-radius: 8px; cursor: pointer; font-weight: 600; transition: all 0.3s; font-size: 16px; }
        .custom-robux-btn:hover { background: linear-gradient(to right, #778da9, #415a77); }
        .custom-robux-info { margin-top: 15px; font-size: 16px; color: #778da9; }
        .promo-list-item { background: rgba(27, 38, 59, 0.8); border-radius: 8px; padding: 15px; margin-bottom: 10px; border: 1px solid #415a77; }
        .promo-list-info { display: flex; justify-content: space-between; align-items: center; }
        .promo-code { font-size: 18px; font-weight: 800; color: #ffb703; font-family: 'Courier New', monospace; }
        .promo-details { font-size: 14px; color: #778da9; }
        .promo-discount { background: rgba(255, 183, 3, 0.2); color: #ffb703; padding: 3px 10px; border-radius: 10px; font-weight: 600; }
        .robux-icon { height: 20px; vertical-align: middle; }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="logo-container">
                <div class="logo">
                    <div class="logo-icon">H</div>
                    Hubs Shop
                </div>
            </div>
            <div class="header-buttons">
                <button class="robux-btn" id="robuxBtn">
                    <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M12 2L15.09 8.26L22 9.27L17 14.14L18.18 21.02L12 17.77L5.82 21.02L7 14.14L2 9.27L8.91 8.26L12 2z"/>
                    </svg>
                    Купить Robux
                </button>
                <button class="admin-btn" id="adminBtn">
                    <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M12 15l8-8-8-8-8 8 8 8z"/>
                        <path d="M4 22h16"/>
                        <path d="M4 15l8-8 8 8"/>
                    </svg>
                    Админ
                </button>
            </div>
        </div>

        <div class="step-indicator">
            <div class="step active" id="step1"><div class="step-circle">1</div><div class="step-text">ВЫБОР ИГРЫ</div></div>
            <div class="step" id="step2"><div class="step-circle">2</div><div class="step-text">ВЫБОР ПАССА</div></div>
            <div class="step" id="step3"><div class="step-circle">3</div><div class="step-text">ВАШ АККАУНТ</div></div>
            <div class="step" id="step4"><div class="step-circle">4</div><div class="step-text">ПОЛУЧЕНИЕ</div></div>
        </div>

        <div class="page active" id="page1">
            <h1 class="page-title">ВЫБЕРИТЕ ИГРУ</h1>
            <p class="page-subtitle">Выберите игру из списка ниже</p>
            <div class="info-message">НА ПОСЛЕДНЕМ ЭТАПЕ ВАМ ПРИДЁТСЯ ЗАЙТИ В ИГРУ ДЛЯ ПОЛУЧЕНИЯ ГЕЙМПАССА</div>
            <div class="game-carousel-container">
                <div class="game-carousel" id="gameCarousel"></div>
            </div>
            <div class="carousel-controls">
                <button class="carousel-btn" id="prevGameBtn">↑</button>
                <button class="carousel-btn" id="nextGameBtn">↓</button>
            </div>
            <button class="next-btn" id="toPage2Btn" disabled>ДАЛЕЕ →</button>
        </div>

        <div class="page" id="page2">
            <h1 class="page-title" id="selectedGameTitle">ВЫБЕРИТЕ ПАСС</h1>
            <p class="page-subtitle">Выберите нужный геймпасс для покупки</p>
            <div class="info-message">ВЫБЕРИТЕ ОДИН ИЗ ПРЕДЛОЖЕННЫХ ГЕЙМПАССОВ ДЛЯ ПРИОБРЕТЕНИЯ</div>
            <div class="gamepass-grid" id="gamepassGrid"></div>
            <button class="next-btn" id="toPage3Btn" disabled>ДАЛЕЕ →</button>
        </div>

        <div class="page" id="page3">
            <h1 class="page-title">ВВЕДИТЕ ДАННЫЕ</h1>
            <p class="page-subtitle">Введите ваш никнейм в Roblox для получения геймпасса</p>
            <div class="search-container">
                <div class="search-box">
                    <input type="text" class="search-input" id="usernameInput" placeholder="Введите ваш никнейм Roblox">
                    <button class="search-btn" id="searchBtn">ПОИСК</button>
                </div>
                <div class="user-results" id="userResults">
                    <div class="empty-message">Введите ваш никнейм выше и нажмите "ПОИСК"</div>
                </div>
            </div>
            <div class="info-message">ВЫБЕРИТЕ СВОЙ АККАУНТ ИЗ СПИСКА. УБЕДИТЕСЬ, ЧТО ВЫБРАЛИ ПРАВИЛЬНЫЙ АККАУНТ</div>
            <button class="next-btn" id="toPage4Btn" disabled>ДАЛЕЕ →</button>
        </div>

        <div class="page" id="page4">
            <h1 class="page-title">ВАШ ГЕЙМПАСС ГОТОВ!</h1>
            <div class="code-container">
                <div class="code-title">КОД ГЕЙМПАССА:</div>
                <div class="code" id="gamepassCode">XXXXX</div>
                <div class="instructions">
                    <h3>ИНФОРМАЦИЯ О ПОКУПКЕ:</h3>
                    <div class="robux-details">
                        <div class="robux-detail-row"><strong>Игра:</strong><span id="pdfGameName">Провинция</span></div>
                        <div class="robux-detail-row"><strong>Геймпасс:</strong><span id="pdfGamepassName">Радио</span></div>
                        <div class="robux-detail-row"><strong>Стоимость в Robux:</strong><span id="pdfRobuxPrice">199 <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" class="robux-icon"></span></div>
                        <div class="robux-detail-row"><strong>Стоимость в рублях:</strong><span id="pdfRublePrice">199 Р</span></div>
                        <div class="robux-detail-row"><strong>Никнейм Roblox:</strong><span id="pdfUsername">Player123</span></div>
                        <div class="robux-detail-row"><strong>Дата покупки:</strong><span id="pdfDate">01.01.2026</span></div>
                    </div>
                </div>
                <div class="action-buttons">
                    <button class="pdf-btn" id="generatePdfBtn">📄 СКАЧАТЬ PDF ЧЕК</button>
                    <a href="https://t.me/HubsBuy" target="_blank" class="telegram-contact">📲 ПЕРЕЙТИ В TELEGRAM</a>
                </div>
                <div class="instructions">
                    <h3>ИНСТРУКЦИЯ ПО ПОЛУЧЕНИЮ:</h3>
                    <ol>
                        <li><strong>Скопируйте код</strong> геймпасса выше</li>
                        <li><strong>Перейдите в Telegram</strong> и найдите @HubsBuy</li>
                        <li><strong>Отправьте чек</strong> (PDF файл) и ваш ник в Roblox</li>
                        <li><strong>В течение 24 часов</strong> вы получите свой геймпасс в игре</li>
                    </ol>
                </div>
            </div>
        </div>

        <div class="page" id="page5">
            <h1 class="page-title">ПОКУПКА ROBUX</h1>
            <div class="robux-container">
                <div class="robux-available">
                    В наличии: <span id="availableRobuxAmount">1 119 300</span> <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" alt="Robux">
                </div>
                
                <div class="custom-robux-container">
                    <h3 style="color: #e0e1dd; margin-bottom: 15px;">ХОЧУ СВОЮ СУММУ</h3>
                    <div style="margin-bottom: 15px;">
                        <input type="number" class="custom-robux-input" id="customRobuxInput" placeholder="Количество" min="10" max="10000">
                        <button class="custom-robux-btn" id="calculateCustomBtn">РАССЧИТАТЬ</button>
                    </div>
                    <div class="custom-robux-info">
                        Стоимость: <span id="customRobuxPrice">0 Р</span> за <span id="customRobuxAmount">0</span> <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" class="robux-icon">
                    </div>
                </div>
                
                <div class="robux-packages" id="robuxPackages"></div>
                
                <div class="robux-summary">
                    <div class="summary-item">
                        <div class="summary-label">ТЫ ПЛАТИШЬ:</div>
                        <div class="summary-value" id="youPayAmount">0 Р</div>
                    </div>
                    <div class="summary-item">
                        <div class="summary-label">ТЫ ПОЛУЧИШЬ:</div>
                        <div class="summary-value" id="youGetAmount">0 <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" alt="Robux"></div>
                    </div>
                </div>
                
                <div class="promo-section">
                    <input type="text" class="promo-input" id="promoCodeRobux" placeholder="У МЕНЯ ЕСТЬ ПРОМОКОД">
                    <button class="promo-btn" id="applyPromoBtn">ПРИМЕНИТЬ</button>
                    <a href="https://t.me/HubsShopz" target="_blank" class="promo-link">ГДЕ ВЗЯТЬ ПРОМОКОД? @HubsShopz</a>
                </div>
                
                <div style="text-align: center; margin-top: 30px;">
                    <button class="next-btn" id="buyRobuxBtn">КУПИТЬ ROBUX</button>
                </div>
            </div>
            <div class="page-navigation">
                <button class="page-btn" id="backToGamepasses">← НАЗАД К ГЕЙМПАССАМ</button>
            </div>
        </div>

        <div class="footer">
            <p>© 2026 HUBS SHOP. Все права защищены. Покупка игровых предметов осуществляется через официальные платформы.</p>
            <div class="creator">maksim87a1</div>
        </div>
    </div>

    <div class="pdf-content" id="pdfPreview">
        <div class="pdf-preview">
            <div class="pdf-header">
                <div class="pdf-logo"><div class="pdf-logo-icon">H</div><div class="pdf-shop-name">Hubs Shop</div></div>
                <div class="pdf-date" id="previewDate">01.01.2026</div>
            </div>
            <div class="pdf-main">
                <div class="pdf-title">ЧЕК О ПОКУПКЕ ГЕЙМПАССА</div>
                <div class="pdf-code" id="previewCode">XXXXX</div>
                <div class="pdf-details">
                    <div class="pdf-detail-row"><strong>Игра:</strong><span id="previewGameName">Провинция</span></div>
                    <div class="pdf-detail-row"><strong>Геймпасс:</strong><span id="previewGamepassName">Радио</span></div>
                    <div class="pdf-detail-row"><strong>Стоимость в Robux:</strong><span id="previewRobuxPrice">199 <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" style="height:20px; vertical-align:middle;"></span></div>
                    <div class="pdf-detail-row"><strong>Стоимость в рублях:</strong><span id="previewRublePrice">199 Р</span></div>
                    <div class="pdf-detail-row"><strong>Никнейм Roblox:</strong><span id="previewUsername">Player123</span></div>
                    <div class="pdf-detail-row"><strong>Дата покупки:</strong><span id="previewPurchaseDate">01.01.2026</span></div>
                    <div class="pdf-detail-row"><strong>Статус:</strong><span style="color: green; font-weight: bold;">АКТИВЕН</span></div>
                </div>
                <div style="margin-top: 30px; padding: 20px; background: #f5f5f5; border-radius: 10px; text-align: left;">
                    <h3 style="margin-bottom: 15px; color: #1b263b;">Инструкция:</h3>
                    <ol style="padding-left: 20px;">
                        <li style="margin-bottom: 8px;">Скопируйте код геймпасса выше</li>
                        <li style="margin-bottom: 8px;">Перейдите в Telegram и найдите @HubsBuy</li>
                        <li style="margin-bottom: 8px;">Отправьте чек (PDF файл) и ваш ник в Roblox</li>
                        <li>В течение 24 часов вы получите свой геймпасс в игре</li>
                    </ol>
                </div>
            </div>
            <div class="pdf-footer">
                <div>Сгенерировано: <span id="previewGenerationTime">01.01.2026 12:00</span></div>
                <div>© 2026 Hubs Shop. Все права защищены.</div>
                <div class="creator">maksim87a1</div>
            </div>
        </div>
    </div>

    <div class="pdf-content" id="robuxPdfPreview">
        <div class="pdf-preview">
            <div class="pdf-header">
                <div class="pdf-logo"><div class="pdf-logo-icon">H</div><div class="pdf-shop-name">Hubs Shop</div></div>
                <div class="pdf-date" id="robuxPdfDate">01.01.2026</div>
            </div>
            <div class="pdf-main">
                <div class="pdf-title">ЧЕК О ПОКУПКЕ ROBUX</div>
                <div class="pdf-code" id="robuxPdfCode">RBX123</div>
                <div class="pdf-details">
                    <div class="pdf-detail-row"><strong>Количество Robux:</strong><span id="robuxPdfAmount">100 <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" style="height:20px; vertical-align:middle;"></span></div>
                    <div class="pdf-detail-row"><strong>Стоимость в рублях:</strong><span id="robuxPdfPrice">70 Р</span></div>
                    <div class="pdf-detail-row"><strong>Промокод:</strong><span id="robuxPdfPromo">Не использовался</span></div>
                    <div class="pdf-detail-row"><strong>Дата покупки:</strong><span id="robuxPdfPurchaseDate">01.01.2026</span></div>
                    <div class="pdf-detail-row"><strong>Код активации:</strong><span id="robuxPdfActivationCode">RBX123</span></div>
                    <div class="pdf-detail-row"><strong>Статус:</strong><span style="color: green; font-weight: bold;">АКТИВЕН</span></div>
                </div>
                <div style="margin-top: 30px; padding: 20px; background: #f5f5f5; border-radius: 10px; text-align: left;">
                    <h3 style="margin-bottom: 15px; color: #1b263b;">Инструкция:</h3>
                    <ol style="padding-left: 20px;">
                        <li style="margin-bottom: 8px;">Скопируйте код активации выше</li>
                        <li style="margin-bottom: 8px;">Перейдите в Telegram и найдите @HubsBuy</li>
                        <li style="margin-bottom: 8px;">Отправьте чек (PDF файл)</li>
                        <li>В течение 24 часов вы получите свои Robux на аккаунт</li>
                    </ol>
                </div>
            </div>
            <div class="pdf-footer">
                <div>Сгенерировано: <span id="robuxPdfGenerationTime">01.01.2026 12:00</span></div>
                <div>© 2026 Hubs Shop. Все права защищены.</div>
                <div class="creator">maksim87a1</div>
            </div>
        </div>
    </div>

    <div class="modal" id="passwordModal">
        <div class="modal-content">
            <h2 class="modal-title">ВХОД В АДМИН-ПАНЕЛЬ</h2>
            <p style="text-align: center; color: #778da9; margin-bottom: 25px;">Введите пароль для доступа к админ-панели</p>
            <div class="admin-form">
                <div class="form-group"><input type="password" class="form-input" id="adminPassword" placeholder="Введите пароль"></div>
                <button class="admin-btn-submit" id="submitPassword">ВОЙТИ</button>
                <div class="error-message" id="passwordError"></div>
            </div>
        </div>
    </div>

    <div class="admin-panel" id="adminPanel">
        <div class="admin-header">
            <h2 class="admin-title">Админ-панель Hubs Shop</h2>
            <button class="close-admin" id="closeAdmin">Закрыть</button>
        </div>
        <div class="admin-tabs">
            <button class="admin-tab active" data-tab="codes">Сгенерированные коды</button>
            <button class="admin-tab" data-tab="addGame">Добавить игру</button>
            <button class="admin-tab" data-tab="addGamepass">Добавить геймпасс</button>
            <button class="admin-tab" data-tab="promocodes">Промокоды</button>
            <button class="admin-tab" data-tab="manageRobux">Управление Robux</button>
            <button class="admin-tab" data-tab="deleteItems">Удаление</button>
            <button class="admin-tab" data-tab="manage">Управление</button>
        </div>
        <div class="admin-content active" id="codesTab">
            <div class="admin-section">
                <h3 class="admin-section-title">Сгенерированные коды</h3>
                <div class="codes-list" id="codesList"></div>
            </div>
        </div>
        <div class="admin-content" id="addGameTab">
            <div class="admin-section">
                <h3 class="admin-section-title">Добавить новую игру</h3>
                <form class="admin-form" id="addGameForm">
                    <div class="form-group"><label class="form-label">Название игры</label><input type="text" class="form-input" id="gameName" required></div>
                    <div class="form-group"><label class="form-label">Ссылка на превью (изображение)</label><input type="url" class="form-input" id="gameImage" required placeholder="https://example.com/image.jpg"></div>
                    <div class="form-group"><label class="form-label">Рейтинг/Описание</label><input type="text" class="form-input" id="gameRating" placeholder="95% Rating" required></div>
                    <button type="submit" class="admin-btn-submit">ДОБАВИТЬ ИГРУ</button>
                </form>
            </div>
        </div>
        <div class="admin-content" id="addGamepassTab">
            <div class="admin-section">
                <h3 class="admin-section-title">Добавить геймпасс</h3>
                <form class="admin-form" id="addGamepassForm">
                    <div class="form-group"><label class="form-label">Выберите игру</label><select class="form-input" id="gameSelect" required><option value="">-- Выберите игру --</option></select></div>
                    <div class="form-group"><label class="form-label">Название геймпасса</label><input type="text" class="form-input" id="gamepassName" required></div>
                    <div class="form-group"><label class="form-label">Ссылка на изображение</label><input type="url" class="form-input" id="gamepassImage" required placeholder="https://example.com/image.jpg"></div>
                    <div class="form-group"><label class="form-label">Цена в Robux</label><input type="number" class="form-input" id="gamepassRobux" min="0" required></div>
                    <div class="form-group"><label class="form-label">Цена в рублях</label><input type="number" class="form-input" id="gamepassRubles" min="0" required></div>
                    <button type="submit" class="admin-btn-submit">ДОБАВИТЬ ГЕЙМПАСС</button>
                </form>
                <div class="gamepass-code-display" id="gamepassCodeDisplay">
                    <div class="gamepass-code-label">Код для нового геймпасса:</div>
                    <div class="gamepass-code-value" id="newGamepassCode">XXXXX</div>
                    <p style="margin-top: 10px; color: #778da9; font-size: 14px;">Сохраните этот код. Он будет использоваться для активации геймпасса.</p>
                </div>
            </div>
        </div>
        <div class="admin-content" id="promocodesTab">
            <div class="admin-section">
                <h3 class="admin-section-title">Создать промокод</h3>
                <form class="admin-form" id="addPromoForm">
                    <div class="form-group">
                        <label class="form-label">Код промокода</label>
                        <input type="text" class="form-input" id="promoCode" required placeholder="Например: SUMMER2024">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Скидка (%)</label>
                        <input type="number" class="form-input" id="promoDiscount" min="1" max="100" required value="10">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Срок действия (дней)</label>
                        <input type="number" class="form-input" id="promoDays" min="1" required value="30">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Максимальное использование</label>
                        <input type="number" class="form-input" id="promoMaxUses" min="1" required value="100">
                    </div>
                    <button type="submit" class="admin-btn-submit">СОЗДАТЬ ПРОМОКОД</button>
                </form>
            </div>
            <div class="admin-section">
                <h3 class="admin-section-title">Активные промокоды</h3>
                <div class="list-container" id="promoCodesList"></div>
            </div>
        </div>
        <div class="admin-content" id="manageRobuxTab">
            <div class="admin-section">
                <h3 class="admin-section-title">Управление количеством Robux</h3>
                <div class="admin-form">
                    <div class="form-group"><label class="form-label">Доступное количество Robux</label><input type="number" class="form-input" id="robuxAmountInput" min="0" value="1119300"></div>
                    <button class="admin-btn-submit" id="saveRobuxBtn">СОХРАНИТЬ КОЛИЧЕСТВО</button>
                </div>
                <p style="color: #778da9; margin-top: 15px; font-size: 14px;">Указанное количество Robux будет отображаться на странице покупки Robux.</p>
            </div>
            <div class="admin-section">
                <h3 class="admin-section-title">Настройка пакетов Robux</h3>
                <div class="admin-form" id="robuxPackagesForm">
                    <div class="form-group">
                        <label class="form-label">Пакет 1: Robux</label>
                        <input type="number" class="form-input" id="robux1" min="0" value="20" placeholder="Количество Robux">
                        <input type="number" class="form-input" id="price1" min="0" value="14" placeholder="Цена в рублях" style="margin-top: 5px;">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Пакет 2: Robux</label>
                        <input type="number" class="form-input" id="robux2" min="0" value="50" placeholder="Количество Robux">
                        <input type="number" class="form-input" id="price2" min="0" value="40" placeholder="Цена в рублях" style="margin-top: 5px;">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Пакет 3: Robux</label>
                        <input type="number" class="form-input" id="robux3" min="0" value="100" placeholder="Количество Robux">
                        <input type="number" class="form-input" id="price3" min="0" value="70" placeholder="Цена в рублях" style="margin-top: 5px;">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Пакет 4: Robux</label>
                        <input type="number" class="form-input" id="robux4" min="0" value="250" placeholder="Количество Robux">
                        <input type="number" class="form-input" id="price4" min="0" value="160" placeholder="Цена в рублях" style="margin-top: 5px;">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Пакет 5: Robux</label>
                        <input type="number" class="form-input" id="robux5" min="0" value="400" placeholder="Количество Robux">
                        <input type="number" class="form-input" id="price5" min="0" value="240" placeholder="Цена в рублях" style="margin-top: 5px;">
                    </div>
                    <div class="form-group">
                        <label class="form-label">Пакет 6: Robux</label>
                        <input type="number" class="form-input" id="robux6" min="0" value="600" placeholder="Количество Robux">
                        <input type="number" class="form-input" id="price6" min="0" value="340" placeholder="Цена в рублях" style="margin-top: 5px;">
                    </div>
                    <button class="admin-btn-submit" id="saveRobuxPackagesBtn">СОХРАНИТЬ ПАКЕТЫ</button>
                </div>
            </div>
        </div>
        <div class="admin-content" id="deleteItemsTab">
            <div class="admin-section">
                <h3 class="admin-section-title">Удаление игр</h3>
                <div class="list-container" id="gamesList"></div>
            </div>
            <div class="admin-section">
                <h3 class="admin-section-title">Удаление геймпассов</h3>
                <div class="form-group"><label class="form-label">Выберите игру</label><select class="form-input" id="deleteGameSelect"><option value="">-- Выберите игру --</option></select></div>
                <div class="list-container" id="gamepassesList"></div>
            </div>
        </div>
        <div class="admin-content" id="manageTab">
            <div class="admin-section">
                <h3 class="admin-section-title">Управление системой</h3>
                <div class="admin-form">
                    <button class="admin-btn-submit" id="clearStorage" style="background: linear-gradient(135deg, #ff6b6b, #ff4757); margin-bottom: 15px;">ОЧИСТИТЬ ВСЕ ДАННЫЕ</button>
                    <button class="admin-btn-submit" id="exportData">ЭКСПОРТИРОВАТЬ ДАННЫЕ</button>
                    <button class="admin-btn-submit" id="importData" style="background: linear-gradient(135deg, #4ade80, #22c55e); margin-top: 15px;">ИМПОРТИРОВАТЬ ДАННЫЕ</button>
                    <input type="file" id="importFile" accept=".json" style="display: none;">
                </div>
            </div>
            <div class="admin-section">
                <h3 class="admin-section-title">Статистика</h3>
                <div style="color: #e0e1dd;">
                    <p>Всего игр: <span id="statsGames">0</span></p>
                    <p>Всего геймпассов: <span id="statsGamepasses">0</span></p>
                    <p>Сгенерировано кодов: <span id="statsCodes">0</span></p>
                    <p>Активных кодов: <span id="statsActiveCodes">0</span></p>
                    <p>Использованных кодов: <span id="statsUsedCodes">0</span></p>
                    <p>Доступно Robux: <span id="statsRobux">0</span> <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" class="robux-icon"></p>
                    <p>Активных промокодов: <span id="statsPromoCodes">0</span></p>
                </div>
            </div>
        </div>
    </div>

    <script>
        const ADMIN_PASSWORD = "HubsAdmin2026!";
        const defaultGames = [{ id: 1, name: "Провинция", image: "https://i.ibb.co/Mx8Mvjhv/Province-PR.webp", rating: "Топовая игра 2026" }];
        const defaultGamepasses = { 1: [ { id: 101, name: "Радио", price: "199", cost: "199", image: "https://i.ibb.co/sD0NxQM/Padio.webp", code: "SCI8Z" }, { id: 102, name: "ОМОН", price: "699", cost: "512", image: "https://i.ibb.co/wZZbVpt4/OMOH.webp", code: "JK9L3" }, { id: 103, name: "ФСБ", price: "3099", cost: "1929", image: "https://i.ibb.co/XftKr4WS/FIB.webp", code: "MNO2P" } ] };
        const defaultRobuxPackages = [ { robux: 20, price: 14 }, { robux: 50, price: 40 }, { robux: 100, price: 70 }, { robux: 250, price: 160 }, { robux: 400, price: 240 }, { robux: 600, price: 340 } ];
        let currentPage = 1, selectedGame = null, selectedGamepass = null, selectedUser = null, currentGameIndex = 0, generatedCodes = [], availableRobux = 1119300, selectedRobuxPackage = null, robuxPackages = [...defaultRobuxPackages];
        let games = JSON.parse(localStorage.getItem('hubs_games')) || defaultGames;
        let gamepasses = JSON.parse(localStorage.getItem('hubs_gamepasses')) || defaultGamepasses;
        generatedCodes = JSON.parse(localStorage.getItem('hubs_generated_codes')) || [];
        availableRobux = parseInt(localStorage.getItem('hubs_available_robux')) || 1119300;
        robuxPackages = JSON.parse(localStorage.getItem('hubs_robux_packages')) || defaultRobuxPackages;
        let promoCodes = JSON.parse(localStorage.getItem('hubs_promo_codes')) || [];
        let customRobuxAmount = 0;
        let customRobuxPrice = 0;

        function generateEnglishCode(length = 5) {
            let result = '';
            const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
            for (let i = 0; i < length; i++) {
                result += chars.charAt(Math.floor(Math.random() * chars.length));
            }
            return result;
        }

        function generateGamepassCode(gamepassName) {
            return generateEnglishCode(5);
        }

        document.addEventListener('DOMContentLoaded', function() {
            initGameCarousel();
            setupEventListeners();
            updateCarouselButtons();
            loadAdminData();
            updateRobuxDisplay();
            loadRobuxPackages();
            updateExistingGamepassesWithCodes();
        });

        function updateExistingGamepassesWithCodes() {
            let needUpdate = false;
            for (const gameId in gamepasses) {
                for (const gamepass of gamepasses[gameId]) {
                    if (!gamepass.code) {
                        gamepass.code = generateGamepassCode(gamepass.name);
                        needUpdate = true;
                    }
                }
            }
            if (needUpdate) {
                localStorage.setItem('hubs_gamepasses', JSON.stringify(gamepasses));
            }
        }

        function initGameCarousel() {
            const carousel = document.getElementById('gameCarousel');
            if (!carousel) return;
            carousel.innerHTML = '';
            games.forEach((game, index) => {
                const gameItem = document.createElement('div');
                gameItem.className = 'game-item';
                gameItem.dataset.id = game.id;
                gameItem.dataset.index = index;
                gameItem.innerHTML = `
                    <img src="${game.image}" alt="${game.name}" class="game-preview" onerror="this.onerror=null; this.src='https://via.placeholder.com/800x250/1b263b/778da9?text=${encodeURIComponent(game.name)}'">
                    <div class="game-title">${game.name}</div>
                    <div class="game-rating">${game.rating}</div>
                `;
                gameItem.addEventListener('click', () => selectGame(game.id, gameItem));
                carousel.appendChild(gameItem);
            });
            updateCarouselPosition();
            if (games.length > 0) {
                const firstGameItem = document.querySelector('.game-item');
                if (firstGameItem) {
                    selectGame(games[0].id, firstGameItem);
                }
            }
        }

        function updateCarouselPosition() {
            const carousel = document.getElementById('gameCarousel');
            if (!carousel) return;
            carousel.style.transform = `translateY(-${currentGameIndex * 100}%)`;
            updateCarouselButtons();
        }

        function updateCarouselButtons() {
            const prevBtn = document.getElementById('prevGameBtn');
            const nextBtn = document.getElementById('nextGameBtn');
            if (prevBtn) { prevBtn.disabled = currentGameIndex === 0; }
            if (nextBtn) { nextBtn.disabled = currentGameIndex === games.length - 1; }
        }

        function selectGame(gameId, element) {
            document.querySelectorAll('.game-item').forEach(item => { item.classList.remove('selected'); });
            element.classList.add('selected');
            selectedGame = games.find(game => game.id === gameId);
            const toPage2Btn = document.getElementById('toPage2Btn');
            if (toPage2Btn) { toPage2Btn.disabled = false; }
            const selectedGameTitle = document.getElementById('selectedGameTitle');
            if (selectedGameTitle && selectedGame) { selectedGameTitle.textContent = `Геймпассы для ${selectedGame.name}`; }
            loadGamepasses(gameId);
        }

        function loadGamepasses(gameId) {
            const gamepassGrid = document.getElementById('gamepassGrid');
            if (!gamepassGrid) return;
            gamepassGrid.innerHTML = '';
            const passes = gamepasses[gameId] || [];
            passes.forEach(pass => {
                const gamepassItem = document.createElement('div');
                gamepassItem.className = 'gamepass-item';
                gamepassItem.dataset.id = pass.id;
                gamepassItem.innerHTML = `
                    <div class="selected-badge">✓</div>
                    <div class="gamepass-image-container">
                        <img src="${pass.image}" alt="${pass.name}" class="gamepass-img" onerror="this.onerror=null; this.src='https://via.placeholder.com/300x180/1b263b/778da9?text=${encodeURIComponent(pass.name)}'">
                        <div class="robux-price-overlay">${pass.price} <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" style="height:16px; vertical-align:middle;"></div>
                    </div>
                    <div class="gamepass-name">${pass.name}</div>
                    <div class="ruble-price">${pass.cost} Р</div>
                `;
                gamepassItem.addEventListener('click', () => selectGamepass(pass.id, gamepassItem));
                gamepassGrid.appendChild(gamepassItem);
            });
            if (passes.length === 0) {
                gamepassGrid.innerHTML = '<div class="empty-message">Для этой игры пока нет доступных геймпассов</div>';
            }
            selectedGamepass = null;
            const toPage3Btn = document.getElementById('toPage3Btn');
            if (toPage3Btn) { toPage3Btn.disabled = true; }
        }

        function selectGamepass(gamepassId, element) {
            document.querySelectorAll('.gamepass-item').forEach(item => { item.classList.remove('selected'); });
            element.classList.add('selected');
            let foundPass = null;
            for (const gameId in gamepasses) {
                const pass = gamepasses[gameId].find(p => p.id === gamepassId);
                if (pass) { foundPass = pass; break; }
            }
            selectedGamepass = foundPass;
            if (selectedGamepass) {
                document.getElementById('pdfGamepassName').textContent = selectedGamepass.name;
                document.getElementById('pdfRobuxPrice').innerHTML = `${selectedGamepass.price} <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" class="robux-icon">`;
                document.getElementById('pdfRublePrice').textContent = `${selectedGamepass.cost} Р`;
                document.getElementById('previewGamepassName').textContent = selectedGamepass.name;
                document.getElementById('previewRobuxPrice').innerHTML = `${selectedGamepass.price} <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" style="height:20px; vertical-align:middle;">`;
                document.getElementById('previewRublePrice').textContent = `${selectedGamepass.cost} Р`;
            }
            const toPage3Btn = document.getElementById('toPage3Btn');
            if (toPage3Btn) { toPage3Btn.disabled = false; }
        }

        function updateRobuxDisplay() {
            document.getElementById('availableRobuxAmount').textContent = availableRobux.toLocaleString();
        }

        function loadRobuxPackages() {
            const robuxPackagesContainer = document.getElementById('robuxPackages');
            if (!robuxPackagesContainer) return;
            robuxPackagesContainer.innerHTML = '';
            robuxPackages.forEach((pkg, index) => {
                const packageElement = document.createElement('div');
                packageElement.className = 'robux-package';
                packageElement.dataset.robux = pkg.robux;
                packageElement.dataset.price = pkg.price;
                packageElement.dataset.index = index;
                packageElement.innerHTML = `
                    <div class="robux-amount">${pkg.robux} <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" alt="Robux"></div>
                    <div class="robux-price">${pkg.price} Р</div>
                `;
                packageElement.addEventListener('click', () => selectRobuxPackage(pkg, packageElement));
                robuxPackagesContainer.appendChild(packageElement);
            });
        }

        function selectRobuxPackage(pkg, element) {
            document.querySelectorAll('.robux-package').forEach(item => { item.classList.remove('selected'); });
            document.querySelectorAll('.robux-package').forEach(item => { item.style.borderColor = '#415a77'; });
            element.classList.add('selected');
            element.style.borderColor = '#ffb703';
            selectedRobuxPackage = pkg;
            customRobuxAmount = 0;
            customRobuxPrice = 0;
            document.getElementById('customRobuxInput').value = '';
            document.getElementById('customRobuxPrice').textContent = '0 Р';
            document.getElementById('customRobuxAmount').textContent = '0';
            document.getElementById('youPayAmount').textContent = `${pkg.price} Р`;
            document.getElementById('youGetAmount').innerHTML = `${pkg.robux} <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" alt="Robux">`;
        }

        function calculateCustomRobux() {
            const customInput = document.getElementById('customRobuxInput');
            const amount = parseInt(customInput.value);
            
            if (!amount || amount < 10) {
                alert('Пожалуйста, введите количество Robux (минимум 10)');
                return;
            }
            
            if (amount > 10000) {
                alert('Максимальное количество Robux за один раз: 10,000');
                return;
            }
            
            // Расчет цены: примерно 0.7 рубля за 1 Robux
            const price = Math.round(amount * 0.7);
            customRobuxAmount = amount;
            customRobuxPrice = price;
            
            document.getElementById('customRobuxPrice').textContent = `${price} Р`;
            document.getElementById('customRobuxAmount').textContent = amount;
            
            // Сбросить выбранный пакет
            selectedRobuxPackage = null;
            document.querySelectorAll('.robux-package').forEach(item => { 
                item.classList.remove('selected'); 
                item.style.borderColor = '#415a77';
            });
            
            document.getElementById('youPayAmount').textContent = `${price} Р`;
            document.getElementById('youGetAmount').innerHTML = `${amount} <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" alt="Robux">`;
        }

        function setupEventListeners() {
            document.getElementById('prevGameBtn').addEventListener('click', () => { if (currentGameIndex > 0) { currentGameIndex--; updateCarouselPosition(); } });
            document.getElementById('nextGameBtn').addEventListener('click', () => { if (currentGameIndex < games.length - 1) { currentGameIndex++; updateCarouselPosition(); } });
            document.getElementById('toPage2Btn').addEventListener('click', () => switchPage(2));
            document.getElementById('toPage3Btn').addEventListener('click', () => switchPage(3));
            document.getElementById('toPage4Btn').addEventListener('click', () => { savePurchaseInfo(); switchPage(4); });
            document.getElementById('robuxBtn').addEventListener('click', () => { switchToRobuxPage(); });
            document.getElementById('backToGamepasses').addEventListener('click', () => { switchToGamepasses(); });
            document.getElementById('searchBtn').addEventListener('click', searchUser);
            document.getElementById('usernameInput').addEventListener('keypress', (e) => { if (e.key === 'Enter') { searchUser(); } });
            document.getElementById('generatePdfBtn').addEventListener('click', generatePDF);
            document.getElementById('buyRobuxBtn').addEventListener('click', buyRobux);
            document.getElementById('applyPromoBtn').addEventListener('click', applyPromoCode);
            document.getElementById('calculateCustomBtn').addEventListener('click', calculateCustomRobux);
            document.getElementById('customRobuxInput').addEventListener('keypress', (e) => { if (e.key === 'Enter') { calculateCustomRobux(); } });
            document.getElementById('adminBtn').addEventListener('click', showPasswordModal);
            document.getElementById('closeAdmin').addEventListener('click', hideAdminPanel);
            document.getElementById('submitPassword').addEventListener('click', checkAdminPassword);
            document.querySelectorAll('.admin-tab').forEach(tab => { tab.addEventListener('click', () => switchAdminTab(tab.dataset.tab)); });
            document.getElementById('addGameForm').addEventListener('submit', addNewGame);
            document.getElementById('addGamepassForm').addEventListener('submit', addNewGamepass);
            document.getElementById('addPromoForm').addEventListener('submit', addNewPromoCode);
            document.getElementById('saveRobuxBtn').addEventListener('click', saveRobuxAmount);
            document.getElementById('saveRobuxPackagesBtn').addEventListener('click', saveRobuxPackages);
            document.getElementById('clearStorage').addEventListener('click', clearAllData);
            document.getElementById('exportData').addEventListener('click', exportData);
            document.getElementById('importData').addEventListener('click', () => { document.getElementById('importFile').click(); });
            document.getElementById('importFile').addEventListener('change', importData);
            document.getElementById('deleteGameSelect').addEventListener('change', loadGamepassesForDeletion);
            document.getElementById('adminPassword').addEventListener('keypress', (e) => { if (e.key === 'Enter') { checkAdminPassword(); } });
        }

        function switchToRobuxPage() {
            document.querySelectorAll('.page').forEach(page => { page.style.display = 'none'; });
            document.querySelector('.step-indicator').style.display = 'none';
            document.getElementById('page5').style.display = 'block';
            selectedRobuxPackage = null;
            customRobuxAmount = 0;
            customRobuxPrice = 0;
            document.getElementById('youPayAmount').textContent = '0 Р';
            document.getElementById('youGetAmount').innerHTML = '0 <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" alt="Robux">';
            document.querySelectorAll('.robux-package').forEach(item => { 
                item.classList.remove('selected'); 
                item.style.borderColor = '#415a77';
            });
            document.getElementById('customRobuxInput').value = '';
            document.getElementById('customRobuxPrice').textContent = '0 Р';
            document.getElementById('customRobuxAmount').textContent = '0';
        }

        function switchToGamepasses() {
            document.querySelectorAll('.page').forEach(page => { page.style.display = 'none'; });
            document.querySelector('.step-indicator').style.display = 'flex';
            document.getElementById('page1').style.display = 'block';
            currentPage = 1;
            document.querySelectorAll('.step').forEach(step => { step.classList.remove('active'); });
            document.getElementById('step1').classList.add('active');
        }

        function searchUser() {
            const usernameInput = document.getElementById('usernameInput');
            if (!usernameInput) return;
            const username = usernameInput.value.trim();
            if (!username) { alert('Пожалуйста, введите ваш никнейм'); return; }
            const userResults = document.getElementById('userResults');
            if (!userResults) return;
            userResults.innerHTML = '';
            setTimeout(() => {
                const userItem = document.createElement('div');
                userItem.className = 'user-item selected';
                userItem.dataset.id = 1;
                const initials = username.substring(0, 2).toUpperCase();
                userItem.innerHTML = `
                    <div class="user-avatar">${initials}</div>
                    <div class="user-name">${username} (Это вы?)</div>
                `;
                userItem.addEventListener('click', () => selectUser(1, userItem));
                userResults.appendChild(userItem);
                document.getElementById('pdfUsername').textContent = username;
                document.getElementById('previewUsername').textContent = username;
                const toPage4Btn = document.getElementById('toPage4Btn');
                if (toPage4Btn) { toPage4Btn.disabled = false; }
            }, 500);
        }

        function selectUser(userId, element) {
            document.querySelectorAll('.user-item').forEach(item => { item.classList.remove('selected'); });
            element.classList.add('selected');
            selectedUser = userId;
        }

        function switchPage(pageNumber) {
            document.querySelectorAll('.page').forEach(page => { page.style.display = 'none'; });
            const pageElement = document.getElementById(`page${pageNumber}`);
            if (pageElement) { pageElement.style.display = 'block'; }
            document.querySelectorAll('.step').forEach(step => { step.classList.remove('active'); });
            for (let i = 1; i <= pageNumber; i++) {
                const stepElement = document.getElementById(`step${i}`);
                if (stepElement) { stepElement.classList.add('active'); }
            }
            currentPage = pageNumber;
            if (pageNumber === 4) {
                if (selectedGamepass && selectedGamepass.code) {
                    document.getElementById('gamepassCode').textContent = selectedGamepass.code;
                    document.getElementById('previewCode').textContent = selectedGamepass.code;
                }
                updatePDFInfo();
            }
        }

        function savePurchaseInfo() {
            const usernameInput = document.getElementById('usernameInput');
            const username = usernameInput ? usernameInput.value.trim() : 'Не указан';
            const code = selectedGamepass ? selectedGamepass.code : generateEnglishCode(5);
            const purchase = {
                id: Date.now(), code: code, game: selectedGame ? selectedGame.name : 'Не выбрана',
                gamepass: selectedGamepass ? selectedGamepass.name : 'Не выбран',
                robuxPrice: selectedGamepass ? selectedGamepass.price : '0',
                rublePrice: selectedGamepass ? selectedGamepass.cost : '0',
                username: username, date: new Date().toLocaleDateString('ru-RU'),
                time: new Date().toLocaleTimeString('ru-RU'), status: 'active',
                used: false, type: 'gamepass'
            };
            generatedCodes.push(purchase);
            localStorage.setItem('hubs_generated_codes', JSON.stringify(generatedCodes));
            if (document.getElementById('adminPanel').classList.contains('active')) {
                loadAdminCodes();
            }
        }

        function updatePDFInfo() {
            const now = new Date();
            document.getElementById('pdfDate').textContent = now.toLocaleDateString('ru-RU');
            document.getElementById('previewDate').textContent = now.toLocaleDateString('ru-RU');
            document.getElementById('previewPurchaseDate').textContent = now.toLocaleDateString('ru-RU');
            document.getElementById('previewGenerationTime').textContent = `${now.toLocaleDateString('ru-RU')} ${now.toLocaleTimeString('ru-RU', {hour: '2-digit', minute:'2-digit'})}`;
            if (selectedGame) {
                document.getElementById('pdfGameName').textContent = selectedGame.name;
                document.getElementById('previewGameName').textContent = selectedGame.name;
            }
        }

        async function generatePDF() {
            const { jsPDF } = window.jspdf;
            const pdf = new jsPDF('p', 'mm', 'a4');
            const pdfPreview = document.getElementById('pdfPreview');
            pdfPreview.style.display = 'block';
            try {
                const canvas = await html2canvas(pdfPreview, { scale: 2, useCORS: true, logging: false, backgroundColor: '#ffffff' });
                const imgData = canvas.toDataURL('image/png');
                const imgWidth = 190;
                const imgHeight = (canvas.height * imgWidth) / canvas.width;
                pdf.addImage(imgData, 'PNG', 10, 10, imgWidth, imgHeight);
                pdf.save(`HubsShop_Чек_${document.getElementById('gamepassCode').textContent}.pdf`);
            } catch (error) {
                console.error('Ошибка при генерации PDF:', error);
                alert('Произошла ошибка при генерации PDF. Пожалуйста, попробуйте сделать скриншот страницы.');
            } finally {
                pdfPreview.style.display = 'none';
            }
        }

        function buyRobux() {
            let robuxAmount, rublePrice;
            
            if (customRobuxAmount > 0) {
                robuxAmount = customRobuxAmount;
                rublePrice = customRobuxPrice;
            } else if (selectedRobuxPackage) {
                robuxAmount = selectedRobuxPackage.robux;
                rublePrice = selectedRobuxPackage.price;
            } else {
                alert('Пожалуйста, выберите пакет Robux или укажите свою сумму');
                return;
            }
            
            const promoCode = document.getElementById('promoCodeRobux').value;
            const robuxCode = generateEnglishCode(6);
            
            // Проверка промокода
            let finalPrice = rublePrice;
            let appliedPromo = promoCode || 'Не использовался';
            
            if (promoCode) {
                const promo = promoCodes.find(p => p.code === promoCode && !p.used && p.expiryDate > Date.now() && p.uses < p.maxUses);
                if (promo) {
                    finalPrice = Math.round(rublePrice * (1 - promo.discount / 100));
                    promo.uses++;
                    if (promo.uses >= promo.maxUses) {
                        promo.used = true;
                    }
                    localStorage.setItem('hubs_promo_codes', JSON.stringify(promoCodes));
                    appliedPromo = `${promoCode} (скидка ${promo.discount}%)`;
                }
            }
            
            // Создаем запись о покупке
            const purchase = {
                id: Date.now(), code: robuxCode, robuxAmount: robuxAmount,
                rublePrice: finalPrice, promoCode: appliedPromo,
                date: new Date().toLocaleDateString('ru-RU'), time: new Date().toLocaleTimeString('ru-RU'),
                status: 'active', used: false, type: 'robux'
            };
            
            generatedCodes.push(purchase);
            localStorage.setItem('hubs_generated_codes', JSON.stringify(generatedCodes));
            
            // Обновляем информацию в PDF для Robux
            document.getElementById('robuxPdfCode').textContent = robuxCode;
            document.getElementById('robuxPdfAmount').innerHTML = `${robuxAmount} <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" style="height:20px; vertical-align:middle;">`;
            document.getElementById('robuxPdfPrice').textContent = `${finalPrice} Р`;
            document.getElementById('robuxPdfPromo').textContent = appliedPromo;
            document.getElementById('robuxPdfActivationCode').textContent = robuxCode;
            
            const now = new Date();
            document.getElementById('robuxPdfDate').textContent = now.toLocaleDateString('ru-RU');
            document.getElementById('robuxPdfPurchaseDate').textContent = now.toLocaleDateString('ru-RU');
            document.getElementById('robuxPdfGenerationTime').textContent = `${now.toLocaleDateString('ru-RU')} ${now.toLocaleTimeString('ru-RU', {hour: '2-digit', minute:'2-digit'})}`;
            
            // Генерируем PDF
            generateRobuxPDF();
            
            alert(`Покупка Robux успешно оформлена! Код активации: ${robuxCode}\nСтоимость: ${finalPrice} Р`);
        }

        async function generateRobuxPDF() {
            const { jsPDF } = window.jspdf;
            const pdf = new jsPDF('p', 'mm', 'a4');
            const robuxPdfPreview = document.getElementById('robuxPdfPreview');
            robuxPdfPreview.style.display = 'block';
            try {
                const canvas = await html2canvas(robuxPdfPreview, { scale: 2, useCORS: true, logging: false, backgroundColor: '#ffffff' });
                const imgData = canvas.toDataURL('image/png');
                const imgWidth = 190;
                const imgHeight = (canvas.height * imgWidth) / canvas.width;
                pdf.addImage(imgData, 'PNG', 10, 10, imgWidth, imgHeight);
                pdf.save(`HubsShop_Robux_${document.getElementById('robuxPdfCode').textContent}.pdf`);
            } catch (error) {
                console.error('Ошибка при генерации PDF:', error);
                alert('Произошла ошибка при генерации PDF. Пожалуйста, попробуйте сделать скриншот страницы.');
            } finally {
                robuxPdfPreview.style.display = 'none';
            }
        }

        function applyPromoCode() {
            const promoCode = document.getElementById('promoCodeRobux').value;
            if (!promoCode) { alert('Введите промокод'); return; }
            
            const promo = promoCodes.find(p => p.code === promoCode && !p.used && p.expiryDate > Date.now() && p.uses < p.maxUses);
            
            if (!promo) {
                alert('Промокод не найден, истек или достиг лимита использований');
                return;
            }
            
            let currentPrice = 0;
            if (selectedRobuxPackage) {
                currentPrice = selectedRobuxPackage.price;
            } else if (customRobuxPrice > 0) {
                currentPrice = customRobuxPrice;
            }
            
            if (currentPrice === 0) {
                alert('Сначала выберите количество Robux');
                return;
            }
            
            const discountedPrice = Math.round(currentPrice * (1 - promo.discount / 100));
            document.getElementById('youPayAmount').textContent = `${discountedPrice} Р`;
            alert(`Промокод "${promoCode}" применен! Скидка ${promo.discount}%`);
        }

        function showPasswordModal() {
            document.getElementById('passwordModal').classList.add('active');
            document.getElementById('adminPassword').focus();
        }

        function hidePasswordModal() {
            document.getElementById('passwordModal').classList.remove('active');
            document.getElementById('adminPassword').value = '';
            document.getElementById('passwordError').textContent = '';
        }

        function checkAdminPassword() {
            const password = document.getElementById('adminPassword').value;
            const errorElement = document.getElementById('passwordError');
            if (password === ADMIN_PASSWORD) {
                hidePasswordModal();
                showAdminPanel();
            } else {
                errorElement.textContent = 'Неверный пароль!';
            }
        }

        function showAdminPanel() {
            document.getElementById('adminPanel').classList.add('active');
            loadAdminData();
            loadGamesForDeletion();
            loadGameSelectForDeletion();
            loadPromoCodes();
        }

        function hideAdminPanel() {
            document.getElementById('adminPanel').classList.remove('active');
        }

        function switchAdminTab(tabName) {
            document.querySelectorAll('.admin-content').forEach(content => { content.classList.remove('active'); });
            document.querySelectorAll('.admin-tab').forEach(tab => { tab.classList.remove('active'); });
            const tabElement = document.getElementById(`${tabName}Tab`);
            if (tabElement) { tabElement.classList.add('active'); }
            const activeTab = document.querySelector(`[data-tab="${tabName}"]`);
            if (activeTab) { activeTab.classList.add('active'); }
            if (tabName === 'codes') {
                loadAdminCodes();
            } else if (tabName === 'addGamepass') {
                loadGameSelect();
                document.getElementById('gamepassCodeDisplay').classList.remove('show');
            } else if (tabName === 'promocodes') {
                loadPromoCodes();
            } else if (tabName === 'manageRobux') {
                loadRobuxSettings();
            } else if (tabName === 'deleteItems') {
                loadGamesForDeletion();
                loadGameSelectForDeletion();
            } else if (tabName === 'manage') {
                loadStats();
            }
        }

        function loadAdminData() {
            loadAdminCodes();
            loadGameSelect();
            loadPromoCodes();
            loadStats();
        }

        function loadAdminCodes() {
            const codesList = document.getElementById('codesList');
            if (!codesList) return;
            if (generatedCodes.length === 0) {
                codesList.innerHTML = '<div class="empty-list">Нет сгенерированных кодов</div>';
                return;
            }
            codesList.innerHTML = '';
            const sortedCodes = [...generatedCodes].sort((a, b) => b.id - a.id);
            sortedCodes.forEach(code => {
                const codeItem = document.createElement('div');
                codeItem.className = 'code-item';
                const typeLabel = code.type === 'robux' ? 'Robux' : 'Геймпасс';
                const robuxDisplay = code.type === 'robux' ? 
                    `${code.robuxAmount} <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" style="height:16px; vertical-align:middle;">` : 
                    `${code.robuxPrice} <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" style="height:16px; vertical-align:middle;">`;
                
                codeItem.innerHTML = `
                    <div class="code-info">
                        <div class="code-value">${code.code}</div>
                        <div class="code-details">
                            ${typeLabel} | ${code.game || robuxDisplay} - ${code.gamepass || ''} | ${code.username || 'Не указан'} | ${code.date} ${code.time}
                        </div>
                    </div>
                    <div class="code-status ${code.used ? 'status-used' : 'status-active'}">
                        ${code.used ? 'ИСПОЛЬЗОВАН' : 'АКТИВЕН'}
                    </div>
                `;
                codeItem.addEventListener('dblclick', () => {
                    code.used = !code.used;
                    code.status = code.used ? 'used' : 'active';
                    localStorage.setItem('hubs_generated_codes', JSON.stringify(generatedCodes));
                    loadAdminCodes();
                    loadStats();
                });
                codesList.appendChild(codeItem);
            });
        }

        function loadPromoCodes() {
            const promoCodesList = document.getElementById('promoCodesList');
            if (!promoCodesList) return;
            if (promoCodes.length === 0) {
                promoCodesList.innerHTML = '<div class="empty-list">Нет созданных промокодов</div>';
                return;
            }
            promoCodesList.innerHTML = '';
            promoCodes.forEach(promo => {
                const promoItem = document.createElement('div');
                promoItem.className = 'promo-list-item';
                const expiryDate = new Date(promo.expiryDate).toLocaleDateString('ru-RU');
                const isExpired = promo.expiryDate < Date.now();
                const isUsed = promo.used || promo.uses >= promo.maxUses;
                
                promoItem.innerHTML = `
                    <div class="promo-list-info">
                        <div>
                            <div class="promo-code">${promo.code}</div>
                            <div class="promo-details">
                                Скидка: <span class="promo-discount">${promo.discount}%</span> | 
                                Использовано: ${promo.uses}/${promo.maxUses} | 
                                Действует до: ${expiryDate}
                            </div>
                        </div>
                        <div>
                            <span class="code-status ${isExpired || isUsed ? 'status-used' : 'status-active'}">
                                ${isExpired ? 'ИСТЕК' : isUsed ? 'ИСПОЛЬЗОВАН' : 'АКТИВЕН'}
                            </span>
                        </div>
                    </div>
                `;
                promoCodesList.appendChild(promoItem);
            });
        }

        function addNewPromoCode(e) {
            e.preventDefault();
            const promoCode = document.getElementById('promoCode').value.toUpperCase();
            const discount = parseInt(document.getElementById('promoDiscount').value);
            const days = parseInt(document.getElementById('promoDays').value);
            const maxUses = parseInt(document.getElementById('promoMaxUses').value);
            
            if (!promoCode || !discount || !days || !maxUses) {
                alert('Пожалуйста, заполните все поля');
                return;
            }
            
            if (discount < 1 || discount > 100) {
                alert('Скидка должна быть от 1% до 100%');
                return;
            }
            
            if (promoCodes.find(p => p.code === promoCode)) {
                alert('Промокод с таким кодом уже существует');
                return;
            }
            
            const expiryDate = Date.now() + (days * 24 * 60 * 60 * 1000);
            
            const newPromo = {
                id: Date.now(),
                code: promoCode,
                discount: discount,
                expiryDate: expiryDate,
                maxUses: maxUses,
                uses: 0,
                used: false,
                created: new Date().toLocaleDateString('ru-RU')
            };
            
            promoCodes.push(newPromo);
            localStorage.setItem('hubs_promo_codes', JSON.stringify(promoCodes));
            
            document.getElementById('addPromoForm').reset();
            loadPromoCodes();
            loadStats();
            
            alert(`Промокод "${promoCode}" успешно создан! Скидка: ${discount}%`);
        }

        function loadGameSelect() {
            const gameSelect = document.getElementById('gameSelect');
            if (!gameSelect) return;
            gameSelect.innerHTML = '<option value="">-- Выберите игру --</option>';
            games.forEach(game => {
                const option = document.createElement('option');
                option.value = game.id;
                option.textContent = game.name;
                gameSelect.appendChild(option);
            });
        }

        function loadGamesForDeletion() {
            const gamesList = document.getElementById('gamesList');
            if (!gamesList) return;
            gamesList.innerHTML = '';
            if (games.length === 0) {
                gamesList.innerHTML = '<div class="empty-list">Нет добавленных игр</div>';
                return;
            }
            games.forEach(game => {
                const listItem = document.createElement('div');
                listItem.className = 'list-item';
                listItem.innerHTML = `
                    <div class="list-item-info">
                        <div class="list-item-name">${game.name}</div>
                        <div class="list-item-details">ID: ${game.id} | ${game.rating}</div>
                    </div>
                    <button class="delete-btn" data-id="${game.id}" data-type="game">УДАЛИТЬ</button>
                `;
                gamesList.appendChild(listItem);
            });
            document.querySelectorAll('.delete-btn[data-type="game"]').forEach(btn => {
                btn.addEventListener('click', deleteGame);
            });
        }

        function loadGameSelectForDeletion() {
            const deleteGameSelect = document.getElementById('deleteGameSelect');
            if (!deleteGameSelect) return;
            deleteGameSelect.innerHTML = '<option value="">-- Выберите игру --</option>';
            games.forEach(game => {
                const option = document.createElement('option');
                option.value = game.id;
                option.textContent = game.name;
                deleteGameSelect.appendChild(option);
            });
        }

        function loadGamepassesForDeletion() {
            const gamepassesList = document.getElementById('gamepassesList');
            if (!gamepassesList) return;
            const gameId = parseInt(document.getElementById('deleteGameSelect').value);
            if (!gameId) {
                gamepassesList.innerHTML = '<div class="empty-list">Выберите игру для отображения геймпассов</div>';
                return;
            }
            const passes = gamepasses[gameId] || [];
            gamepassesList.innerHTML = '';
            if (passes.length === 0) {
                gamepassesList.innerHTML = '<div class="empty-list">У этой игры нет геймпассов</div>';
                return;
            }
            passes.forEach(pass => {
                const listItem = document.createElement('div');
                listItem.className = 'list-item';
                listItem.innerHTML = `
                    <div class="list-item-info">
                        <div class="list-item-name">${pass.name}</div>
                        <div class="list-item-details">${pass.price} <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" style="height:14px; vertical-align:middle;"> | ${pass.cost} Р | Код: ${pass.code}</div>
                    </div>
                    <button class="delete-btn" data-id="${pass.id}" data-gameid="${gameId}" data-type="gamepass">УДАЛИТЬ</button>
                `;
                gamepassesList.appendChild(listItem);
            });
            document.querySelectorAll('.delete-btn[data-type="gamepass"]').forEach(btn => {
                btn.addEventListener('click', deleteGamepass);
            });
        }

        function deleteGame(e) {
            const gameId = parseInt(e.target.dataset.id);
            if (confirm('Вы уверены, что хотите удалить эту игру? Все связанные геймпассы также будут удалены.')) {
                games = games.filter(game => game.id !== gameId);
                delete gamepasses[gameId];
                localStorage.setItem('hubs_games', JSON.stringify(games));
                localStorage.setItem('hubs_gamepasses', JSON.stringify(gamepasses));
                initGameCarousel();
                loadGamesForDeletion();
                loadGameSelect();
                loadGameSelectForDeletion();
                loadStats();
                alert('Игра успешно удалена!');
            }
        }

        function deleteGamepass(e) {
            const gamepassId = parseInt(e.target.dataset.id);
            const gameId = parseInt(e.target.dataset.gameid);
            if (confirm('Вы уверены, что хотите удалить этот геймпасс?')) {
                gamepasses[gameId] = gamepasses[gameId].filter(pass => pass.id !== gamepassId);
                if (gamepasses[gameId].length === 0) { delete gamepasses[gameId]; }
                localStorage.setItem('hubs_gamepasses', JSON.stringify(gamepasses));
                loadGamepassesForDeletion();
                loadStats();
                if (selectedGame && selectedGame.id === gameId) { loadGamepasses(gameId); }
                alert('Геймпасс успешно удален!');
            }
        }

        function loadRobuxSettings() {
            document.getElementById('robuxAmountInput').value = availableRobux;
            for (let i = 0; i < robuxPackages.length; i++) {
                if (i < 6) {
                    document.getElementById(`robux${i+1}`).value = robuxPackages[i].robux;
                    document.getElementById(`price${i+1}`).value = robuxPackages[i].price;
                }
            }
        }

        function saveRobuxAmount() {
            const robuxAmount = parseInt(document.getElementById('robuxAmountInput').value);
            if (isNaN(robuxAmount) || robuxAmount < 0) {
                alert('Пожалуйста, введите корректное количество Robux');
                return;
            }
            availableRobux = robuxAmount;
            localStorage.setItem('hubs_available_robux', availableRobux.toString());
            updateRobuxDisplay();
            alert('Количество Robux успешно обновлено!');
        }

        function saveRobuxPackages() {
            const newPackages = [];
            for (let i = 1; i <= 6; i++) {
                const robux = parseInt(document.getElementById(`robux${i}`).value);
                const price = parseInt(document.getElementById(`price${i}`).value);
                if (isNaN(robux) || robux < 0 || isNaN(price) || price < 0) {
                    alert(`Пожалуйста, введите корректные значения для пакета ${i}`);
                    return;
                }
                newPackages.push({ robux, price });
            }
            robuxPackages = newPackages;
            localStorage.setItem('hubs_robux_packages', JSON.stringify(robuxPackages));
            loadRobuxPackages();
            alert('Пакеты Robux успешно обновлены!');
        }

        function loadStats() {
            document.getElementById('statsGames').textContent = games.length;
            let totalGamepasses = 0;
            for (const gameId in gamepasses) { totalGamepasses += gamepasses[gameId].length; }
            document.getElementById('statsGamepasses').textContent = totalGamepasses;
            document.getElementById('statsCodes').textContent = generatedCodes.length;
            const activeCodes = generatedCodes.filter(code => !code.used).length;
            const usedCodes = generatedCodes.filter(code => code.used).length;
            document.getElementById('statsActiveCodes').textContent = activeCodes;
            document.getElementById('statsUsedCodes').textContent = usedCodes;
            document.getElementById('statsRobux').innerHTML = `${availableRobux.toLocaleString()} <img src="https://i.ibb.co/Bm8f0KB/Robux-Hubs.png" class="robux-icon">`;
            const activePromos = promoCodes.filter(p => !p.used && p.expiryDate > Date.now() && p.uses < p.maxUses).length;
            document.getElementById('statsPromoCodes').textContent = activePromos;
        }

        function addNewGame(e) {
            e.preventDefault();
            const gameName = document.getElementById('gameName').value;
            const gameImage = document.getElementById('gameImage').value;
            const gameRating = document.getElementById('gameRating').value;
            if (!gameName || !gameImage || !gameRating) { alert('Пожалуйста, заполните все поля'); return; }
            const newGame = { id: Date.now(), name: gameName, image: gameImage, rating: gameRating };
            games.push(newGame);
            localStorage.setItem('hubs_games', JSON.stringify(games));
            gamepasses[newGame.id] = [];
            localStorage.setItem('hubs_gamepasses', JSON.stringify(gamepasses));
            document.getElementById('addGameForm').reset();
            initGameCarousel();
            loadGameSelect();
            loadGamesForDeletion();
            loadGameSelectForDeletion();
            loadStats();
            alert(`Игра "${gameName}" успешно добавлена!`);
        }

        function addNewGamepass(e) {
            e.preventDefault();
            const gameId = parseInt(document.getElementById('gameSelect').value);
            const gamepassName = document.getElementById('gamepassName').value;
            const gamepassImage = document.getElementById('gamepassImage').value;
            const gamepassRobux = document.getElementById('gamepassRobux').value;
            const gamepassRubles = document.getElementById('gamepassRubles').value;
            if (!gameId || !gamepassName || !gamepassImage || !gamepassRobux || !gamepassRubles) {
                alert('Пожалуйста, заполните все поля'); return;
            }
            const gamepassCode = generateEnglishCode(5);
            const newGamepass = {
                id: Date.now(), name: gamepassName, price: gamepassRobux,
                cost: gamepassRubles, image: gamepassImage, code: gamepassCode
            };
            if (!gamepasses[gameId]) { gamepasses[gameId] = []; }
            gamepasses[gameId].push(newGamepass);
            localStorage.setItem('hubs_gamepasses', JSON.stringify(gamepasses));
            document.getElementById('newGamepassCode').textContent = gamepassCode;
            document.getElementById('gamepassCodeDisplay').classList.add('show');
            document.getElementById('addGamepassForm').reset();
            if (selectedGame && selectedGame.id === gameId) { loadGamepasses(gameId); }
            loadStats();
            loadGamepassesForDeletion();
            document.getElementById('gamepassCodeDisplay').scrollIntoView({ behavior: 'smooth' });
        }

        function clearAllData() {
            if (confirm('ВНИМАНИЕ! Вы действительно хотите удалить ВСЕ данные? Это действие нельзя отменить.')) {
                localStorage.clear();
                games = [...defaultGames];
                gamepasses = {...defaultGamepasses};
                generatedCodes = [];
                promoCodes = [];
                availableRobux = 1119300;
                robuxPackages = [...defaultRobuxPackages];
                localStorage.setItem('hubs_games', JSON.stringify(games));
                localStorage.setItem('hubs_gamepasses', JSON.stringify(gamepasses));
                localStorage.setItem('hubs_generated_codes', JSON.stringify(generatedCodes));
                localStorage.setItem('hubs_promo_codes', JSON.stringify(promoCodes));
                localStorage.setItem('hubs_available_robux', availableRobux.toString());
                localStorage.setItem('hubs_robux_packages', JSON.stringify(robuxPackages));
                initGameCarousel();
                updateRobuxDisplay();
                loadRobuxPackages();
                loadAdminCodes();
                loadPromoCodes();
                loadGameSelect();
                loadGamesForDeletion();
                loadGameSelectForDeletion();
                loadStats();
                alert('Все данные успешно очищены!');
            }
        }

        function exportData() {
            const data = {
                games: games, gamepasses: gamepasses, generatedCodes: generatedCodes,
                promoCodes: promoCodes, availableRobux: availableRobux, 
                robuxPackages: robuxPackages, exportDate: new Date().toISOString()
            };
            const dataStr = JSON.stringify(data, null, 2);
            const dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
            const exportFileDefaultName = `hubs_shop_backup_${new Date().toISOString().slice(0,10)}.json`;
            const linkElement = document.createElement('a');
            linkElement.setAttribute('href', dataUri);
            linkElement.setAttribute('download', exportFileDefaultName);
            linkElement.click();
        }

        function importData(e) {
            const file = e.target.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const data = JSON.parse(e.target.result);
                    if (!data.games || !data.gamepasses || !data.generatedCodes) {
                        throw new Error('Неверный формат файла');
                    }
                    if (confirm('Заменить текущие данные импортированными?')) {
                        games = data.games;
                        gamepasses = data.gamepasses;
                        generatedCodes = data.generatedCodes;
                        promoCodes = data.promoCodes || [];
                        availableRobux = data.availableRobux || 1119300;
                        robuxPackages = data.robuxPackages || defaultRobuxPackages;
                        localStorage.setItem('hubs_games', JSON.stringify(games));
                        localStorage.setItem('hubs_gamepasses', JSON.stringify(gamepasses));
                        localStorage.setItem('hubs_generated_codes', JSON.stringify(generatedCodes));
                        localStorage.setItem('hubs_promo_codes', JSON.stringify(promoCodes));
                        localStorage.setItem('hubs_available_robux', availableRobux.toString());
                        localStorage.setItem('hubs_robux_packages', JSON.stringify(robuxPackages));
                        initGameCarousel();
                        updateRobuxDisplay();
                        loadRobuxPackages();
                        loadAdminCodes();
                        loadPromoCodes();
                        loadGameSelect();
                        loadGamesForDeletion();
                        loadGameSelectForDeletion();
                        loadStats();
                        alert('Данные успешно импортированы!');
                    }
                } catch (error) {
                    alert('Ошибка при импорте данных: ' + error.message);
                }
            };
            reader.readAsText(file);
            e.target.value = '';
        }
    </script>
</body>
</html>
