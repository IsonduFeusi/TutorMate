<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Perfil Educativo - Simulación Móvil</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    :root {
      /* Paleta de colores sofisticados */
      --primary-50: #eff6ff;
      --primary-100: #dbeafe;
      --primary-200: #bfdbfe;
      --primary-300: #93c5fd;
      --primary-400: #60a5fa;
      --primary-500: #3b82f6;
      --primary-600: #2563eb;
      --primary-700: #1d4ed8;
      --primary-800: #1e40af;
      --primary-900: #1e3a8a;
      /* Colores secundarios */
      --secondary-500: #10b981;
      --accent-500: #f59e0b;
      --purple-500: #8b5cf6;
      --error-500: #ef4444;
      /* Colores de texto */
      --text-primary: #1f2937;
      --text-secondary: #6b7280;
      --text-tertiary: #9ca3af;
      /* Colores de fondo */
      --bg-primary: #111827; /* Fondo negro profundo */
      --bg-secondary: #1f2937; /* Gris oscuro */
      --bg-card: #1e293b; /* Azul grisáceo oscuro */
      --bg-header: linear-gradient(135deg, var(--primary-800) 0%, var(--primary-900) 100%);
      /* Sombras y bordes */
      --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.3);
      --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.2);
      --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
      --border-color: #374151;
      /* Transiciones */
      --transition-fast: all 0.2s ease;
      --transition-medium: all 0.3s ease;
      --transition-slow: all 0.4s ease;
    }
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
      background-color: var(--bg-primary);
      color: #ffffff;
      line-height: 1.6;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
      overflow: hidden; /* Evita scroll temporal */
    }

    /* --- NUEVOS ESTILOS PANTALLA DE INICIO --- */
    .login-screen {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      background: var(--bg-secondary);
      z-index: 101; /* Por encima de todo */
      transition: opacity 0.8s cubic-bezier(.8,0,.2,1), transform 0.8s cubic-bezier(.8,0,.2,1);
      opacity: 1;
      transform: translateY(0);
    }

    .login-screen.hidden {
      opacity: 0;
      pointer-events: none; /* Deshabilita interacción */
      transform: translateY(20px); /* Animación de salida */
    }

    .login-card {
      background: var(--bg-card);
      border-radius: 1.5em;
      box-shadow: var(--shadow-lg);
      width: 90%;
      max-width: 340px;
      padding: 2em 1.5em;
      text-align: center;
      position: relative;
      border: 1px solid var(--border-color);
      overflow: hidden; /* Contiene el pseudo-elemento decorativo */
    }

    .login-card::before {
        content: '';
        position: absolute;
        top: -50%;
        left: -50%;
        width: 200%;
        height: 200%;
        background: radial-gradient(circle, rgba(59,130,246,0.1) 0%, transparent 70%);
        z-index: -1;
        animation: rotate 15s linear infinite; /* Animación de fondo */
    }

    @keyframes rotate {
        from { transform: rotate(0deg); }
        to { transform: rotate(360deg); }
    }

    .login-icon {
        font-size: 3.5rem;
        color: var(--primary-500);
        margin-bottom: 1em;
        animation: pulse 2s infinite; /* Pulsación sutil */
    }

    @keyframes pulse {
        0% { transform: scale(1); }
        50% { transform: scale(1.05); }
        100% { transform: scale(1); }
    }

    .login-title {
        font-size: 1.5rem;
        font-weight: 700;
        margin-bottom: 0.5em;
        color: #ffffff;
    }

    .login-subtitle {
        font-size: 0.9rem;
        color: var(--text-secondary);
        margin-bottom: 1.5em;
    }

    .input-group {
        margin-bottom: 1.2em;
        text-align: left;
    }

    .input-label {
        display: block;
        font-size: 0.85rem;
        color: var(--text-secondary);
        margin-bottom: 0.3em;
        font-weight: 500;
    }

    .input-field {
        width: 100%;
        padding: 0.8em 1em;
        border: 1px solid var(--border-color);
        border-radius: 0.8em;
        background: rgba(30, 41, 59, 0.7); /* Ligeramente transparente */
        color: #ffffff;
        font-size: 1rem;
        transition: var(--transition-fast);
    }

    .input-field:focus {
        outline: none;
        border-color: var(--primary-500);
        box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.2);
    }

    .login-button {
        width: 100%;
        padding: 0.9em;
        background: var(--primary-500);
        color: white;
        border: none;
        border-radius: 0.8em;
        font-size: 1rem;
        font-weight: 600;
        cursor: pointer;
        transition: var(--transition-fast);
        margin-top: 0.5em;
        box-shadow: var(--shadow-sm);
    }

    .login-button:hover {
        background: var(--primary-600);
        transform: translateY(-1px);
        box-shadow: var(--shadow-md);
    }

    .login-button:active {
        transform: translateY(0);
    }

    .login-footer {
        margin-top: 1.5em;
        font-size: 0.8rem;
        color: var(--text-secondary);
    }

    /* --- FIN NUEVOS ESTILOS PANTALLA DE INICIO --- */

    /* Mobile frame - Diseño Samsung */
    .mobile-frame {
      background: #151519;
      border: 4px solid #33343b;
      border-radius: 2.2em;
      width: 370px;
      height: 770px;
      max-width: 99vw;
      max-height: 99vh;
      box-shadow: 0 0 0 6px #232327, 0 4px 24px 0 #000b;
      position: relative;
      overflow: hidden;
      display: flex;
      flex-direction: column;
    }
    /* Notch tipo Samsung con bordes redondeados */
    .mobile-notch {
      position: absolute;
      top: 18px;
      left: 50%;
      transform: translateX(-50%);
      width: 140px;
      height: 25px;
      background: #101013;
      border-radius: 13px 13px 14px 14px;
      box-shadow: 0 1px 6px #0009;
      z-index: 3;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 18px;
      pointer-events: none;
    }
    .notch-dot {
      width: 16px; height: 16px; background: #19191b; border-radius: 50%; display: inline-block;
      border: 2px solid #222;
    }
    .notch-dot.small { width: 8px; height: 8px;}
    .notch-dot.cam { 
      width: 38px; 
      height: 12px; 
      border-radius: 7px; 
      background: #19191b;
      border: 1px solid #222;
    }
    /* Barra superior tipo Samsung */
    .mobile-topbar {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 44px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 19px;
      font-family: 'SF Pro Text', 'Segoe UI', Arial, sans-serif;
      font-size: 1.04em;
      font-weight: 500;
      letter-spacing: 0.01em;
      color: #fff;
      z-index: 5;
      pointer-events: none;
      user-select: none;
    }
    .mobile-topbar .status {
      display: flex;
      align-items: center;
      gap: 6px;
    }
    .mobile-topbar .status .icon {
      font-size: 1.13em;
    }
    /* Contenido de la app */
    .app-inside {
      position: absolute;
      left: 0; right: 0; top: 0; bottom: 0;
      z-index: 10;
      overflow-y: auto;
      background: var(--bg-secondary);
      pointer-events: auto;
      padding-top: 44px; /* Espacio para la barra superior */
      padding-bottom: 18px;
      height: 100%;
      width: 100%;
      box-sizing: border-box;
    }
    /* Botón Premium en la esquina superior derecha */
    .premium-button {
      position: absolute;
      top: 60px; /* Ajustado para que esté debajo de la barra superior */
      right: 12px; /* Margen derecho */
      background: var(--accent-500); /* Color amarillo del accent */
      color: var(--bg-secondary); /* Texto oscuro */
      border: none;
      border-radius: 12px; /* Bordes redondeados */
      padding: 6px 12px;
      font-size: 0.8rem; /* Tamaño de fuente pequeño */
      font-weight: 600;
      cursor: pointer;
      z-index: 20; /* Asegura que esté sobre otros elementos */
      display: flex;
      align-items: center;
      gap: 4px; /* Espacio entre ícono y texto */
      transition: var(--transition-fast);
      box-shadow: var(--shadow-sm);
    }
    .premium-button:hover {
      background: var(--accent-500); /* Mantiene el color principal */
      transform: translateY(-1px);
      box-shadow: var(--shadow-md);
    }
    .premium-button i {
      font-size: 0.9rem; /* Tamaño de ícono */
    }
    /* Loader */
    .loader-screen {
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      background: var(--bg-secondary);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      z-index: 100;
      transition: opacity 0.8s cubic-bezier(.8,0,.2,1);
    }
    .loader-dot {
      width: 18px; height: 18px;
      background: var(--primary-500);
      border-radius: 50%;
      margin: 0 auto 18px auto;
      animation: loader-bounce 1.5s cubic-bezier(.8,0,.2,1) infinite;
    }
    @keyframes loader-bounce {
      0%, 100% { transform: translateY(0);}
      44% { transform: translateY(-8px);}
      80% { transform: translateY(0);}
    }
    .loader-text {
      color: var(--text-secondary);
      font-size: 1.1em;
      font-weight: 500;
      letter-spacing: 0.01em;
      text-align: center;
    }
    /* Contenido principal */
    .container {
      max-width: 420px;
      margin: 0 auto;
      padding: 0 1em 2.3em 1em;
    }
    /* Header de perfil */
    header.profile-header {
      background: var(--bg-header);
      border-bottom-left-radius: 1.8em;
      border-bottom-right-radius: 1.8em;
      box-shadow: var(--shadow-md);
      padding: 2em 1em 1.5em 1em;
      text-align: center;
      position: relative;
      color: #fff;
      margin-bottom: 1.5em;
    }
    .avatar-wrapper { 
      position: relative; 
      display: flex; 
      justify-content: center; 
      align-items: center;
    }
    .avatar {
      width: 5.5em; 
      height: 5.5em; 
      border-radius: 50%;
      background: #fff; 
      border: 4px solid var(--primary-500);
      display: flex; 
      align-items: center; 
      justify-content: center;
      font-size: 2.5em; 
      box-shadow: 0 0 0 6px rgba(59,130,246,0.14);
      margin: 0 auto;
      transition: var(--transition-fast);
      overflow: hidden; /* Asegura que la imagen no se desborde */
    }
    .avatar img {
      width: 100%;
      height: 100%;
      object-fit: cover; /* Ajusta la imagen para cubrir el contenedor */
    }
    .avatar:hover {
      transform: scale(1.05);
    }
    .badge-nivel {
      position: absolute; 
      right: 0.3em; 
      bottom: 0.2em;
      background: #fff; 
      color: var(--primary-800);
      border: 2px solid var(--primary-500); 
      border-radius: 2em;
      padding: 0.14em 0.8em 0.14em 0.6em; 
      font-size: 0.96em;
      font-weight: 700; 
      display: flex; 
      align-items: center;
      box-shadow: var(--shadow-md); 
      z-index: 2; 
      gap: 0.23em;
    }
    .badge-nivel-emoji { 
      font-size: 1em; 
      margin-right: 0.2em;
    }
    .profile-info { 
      margin-top: 1em; 
      margin-bottom: 1.1em;
    }
    .profile-info h1 { 
      font-size: 1.18em; 
      font-weight: 700; 
      margin: 0 0 0.35em 0; 
      color: #fff;
    }
    .profile-info .email, 
    .profile-info .university { 
      font-size: 0.93em; 
      color: rgba(255,255,255,0.78); 
      margin: 0.07em 0; 
      font-weight: 400; 
    }
    .xp-bar-container { 
      margin-top: 1em; 
      text-align: left; 
      width: 100%; 
      max-width: 300px; 
      margin-left: auto; 
      margin-right: auto;
    }
    .xp-bar-labels { 
      display: flex; 
      justify-content: space-between; 
      font-size: 0.86em; 
      margin-bottom: 0.14em; 
      color: #fff; 
      opacity: 0.93; 
      font-weight: 500;
    }
    .xp-bar-bg { 
      width: 100%; 
      height: 1em; 
      background: rgba(245, 158, 11, 0.13); 
      border-radius: 1em; 
      overflow: hidden; 
      position: relative;
    }
    .xp-bar-fill { 
      height: 100%; 
      background: var(--accent-500); 
      border-radius: 1em 0 0 1em; 
      width: 0; 
      transition: width 1s cubic-bezier(.65,.01,.21,1); 
      position: relative;
    }
    .xp-bar-percent { 
      text-align: right; 
      padding-top: 0.13em; 
      font-size: 0.83em; 
      font-weight: 600; 
      color: var(--accent-500);
    }
    /* Grid de estadísticas */
    .stats-grid { 
      display: grid; 
      grid-template-columns: repeat(2, 1fr); 
      gap: 1em; 
      margin-top: 1.3em;
    }
    @media (max-width: 400px) {
      .stats-grid { 
        grid-template-columns: 1fr; 
      } 
    }
    .stat-card {
      background: var(--bg-card); 
      border-radius: 1em;
      box-shadow: var(--shadow-sm); 
      display: flex; 
      align-items: center;
      padding: 0.8em 1em; 
      gap: 0.8em;
      transition: var(--transition-medium);
      cursor: pointer; 
      min-width: 0; 
      min-height: 3.7em; 
      outline: none;
      border: 1px solid var(--border-color);
    }
    .stat-card:hover { 
      box-shadow: var(--shadow-md); 
      transform: translateY(-2px) scale(1.012);
      border-color: var(--primary-200);
    }
    .stat-icon { 
      width: 2.2em; 
      height: 2.2em; 
      display: flex; 
      align-items: center; 
      justify-content: center; 
      border-radius: 50%; 
      font-size: 1.1em;
    }
    .stat-blue { 
      color: var(--primary-800); 
      background: rgba(30, 64, 175, 0.1);
    }
    .stat-green { 
      color: var(--secondary-500); 
      background: rgba(16, 185, 129, 0.1);
    }
    .stat-yellow { 
      color: var(--accent-500); 
      background: rgba(245, 158, 11, 0.1);
    }
    .stat-purple { 
      color: var(--purple-500); 
      background: rgba(139, 92, 246, 0.1);
    }
    .stat-details { 
      min-width: 0; 
      flex: 1; 
    }
    .stat-value { 
      font-size: 1.04em; 
      font-weight: 700; 
      margin-bottom: 0.09em;
      color: #ffffff;
    }
    .stat-label { 
      font-size: 0.87em; 
      color: var(--text-secondary);
    }
    .section-title { 
      font-size: 1.04em; 
      font-weight: 600; 
      margin: 1.6em 0 0.6em 0; 
      color: #ffffff;
      position: relative;
      padding-bottom: 0.5em;
    }
    .section-title::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 40px;
      height: 2px;
      background: var(--primary-500);
      border-radius: 1px;
    }
    /* Lista de actividades */
    .activity-list { 
      list-style: none; 
      padding: 0; 
      margin: 0; 
      display: flex; 
      flex-direction: column; 
      gap: 0.6em;
    }
    .activity-item {
      background: var(--bg-card); 
      border-radius: 1em; 
      box-shadow: var(--shadow-sm);
      display: flex; 
      align-items: center; 
      padding: 0.7em 1em; 
      gap: 0.7em; 
      transition: var(--transition-medium);
      cursor: pointer; 
      outline: none;
      border: 1px solid var(--border-color);
    }
    .activity-item:hover { 
      box-shadow: var(--shadow-md); 
      transform: translateY(-1px) scale(1.008);
      border-color: var(--primary-200);
    }
    .activity-icon { 
      width: 1.75em; 
      height: 1.75em; 
      border-radius: 50%; 
      display: flex; 
      align-items: center; 
      justify-content: center; 
      font-size: 1em;
    }
    .activity-yellow { 
      color: var(--accent-500); 
      background: rgba(245, 158, 11, 0.1);
    }
    .activity-green { 
      color: var(--secondary-500); 
      background: rgba(16, 185, 129, 0.1);
    }
    .activity-purple { 
      color: var(--purple-500); 
      background: rgba(139, 92, 246, 0.1);
    }
    .activity-details { 
      flex: 1; 
      min-width: 0; 
    }
    .activity-desc { 
      font-size: 0.93em; 
      font-weight: 500; 
      color: #ffffff;
    }
    .activity-meta { 
      font-size: 0.83em; 
      color: var(--text-secondary);
    }
    .activity-xp { 
      margin-left: 0.4em; 
      font-size: 0.91em; 
      font-weight: 700; 
      color: var(--accent-500);
    }
    /* Lista de logros */
    .achievements-list { 
      list-style: none; 
      padding: 0; 
      margin: 0; 
      display: flex; 
      flex-direction: column; 
      gap: 0.7em;
    }
    .achievement-item {
      background: var(--bg-card); 
      border-radius: 1em; 
      box-shadow: var(--shadow-sm);
      padding: 0.7em 1em; 
      transition: var(--transition-medium);
      cursor: pointer; 
      opacity: 1; 
      outline: none; 
      display: flex; 
      flex-direction: column; 
      gap: 0.35em; 
      min-width: 0;
      border: 1px solid var(--border-color);
    }
    .achievement-item:hover { 
      box-shadow: var(--shadow-md); 
      transform: translateY(-1px) scale(1.008);
      border-color: var(--primary-200);
    }
    .achievement-disabled { 
      opacity: 0.67; 
      filter: grayscale(0.10); 
      cursor: not-allowed;
    }
    .achievement-row { 
      display: flex; 
      justify-content: space-between; 
      align-items: center;
    }
    .achievement-label { 
      font-weight: 600; 
      font-size: 0.93em; 
      display: flex; 
      align-items: center; 
      gap: 0.2em;
    }
    .achievement-status { 
      font-size: 0.87em; 
      color: var(--text-secondary); 
      font-weight: 600; 
      white-space: nowrap; 
      min-width: 1em;
    }
    .achievement-description { 
      font-size: 0.89em; 
      color: var(--text-secondary);
    }
    .achievement-progress-bar { 
      width: 100%; 
      background: #374151; 
      border-radius: 1em; 
      height: 0.42em; 
      margin-top: 0.25em; 
      overflow: hidden; 
      position: relative;
    }
    .achievement-progress-fill { 
      background: var(--primary-500); 
      height: 100%; 
      border-radius: 1em 0 0 1em; 
      width: 0; 
      transition: width 1s cubic-bezier(.65,.01,.21,1); 
      position: absolute; 
      top: 0; 
      left: 0;
    }
    /* Menú de configuración */
    nav.menu-section { 
      margin-top: 1.8em;
    }
    .menu-list { 
      list-style: none; 
      margin: 0; 
      padding: 0; 
      display: flex; 
      flex-direction: column; 
      gap: 0.5em;
    }
    .menu-item {
      background: var(--bg-card); 
      border-radius: 1em; 
      box-shadow: var(--shadow-sm);
      padding: 0.7em 1em; 
      display: flex; 
      align-items: center; 
      gap: 0.7em; 
      font-size: 0.95em; 
      font-weight: 500; 
      color: #ffffff;
      cursor: pointer; 
      border: none; 
      outline: none; 
      transition: var(--transition-medium); 
      text-align: left;
      border: 1px solid var(--border-color);
    }
    .menu-item:hover { 
      box-shadow: var(--shadow-md); 
      background: var(--primary-50); 
      color: var(--primary-800);
      border-color: var(--primary-200);
    }
    .menu-icon { 
      width: 1.6em; 
      height: 1.6em; 
      display: flex; 
      align-items: center; 
      justify-content: center; 
      border-radius: 50%; 
      font-size: 1em; 
      background: rgba(30, 64, 175, 0.1); 
      flex-shrink: 0; 
      color: var(--primary-800); 
      margin-right: 0.2em;
    }
    .menu-green { 
      color: var(--secondary-500); 
      background: rgba(16, 185, 129, 0.1);
    }
    .menu-purple { 
      color: var(--purple-500); 
      background: rgba(139, 92, 246, 0.1);
    }
    .menu-red { 
      color: var(--error-500); 
      background: rgba(239, 68, 68, 0.1);
    }
    .menu-item.menu-logout { 
      color: var(--error-500); 
      font-weight: 700;
    }
    .menu-item.menu-logout:hover { 
      background: #fee2e2; 
      color: var(--error-500);
    }
    /* Barra de navegación inferior */
    .bottom-nav {
      position: fixed;
      bottom: 0;
      left: 0;
      right: 0;
      background: var(--bg-card);
      border-top: 1px solid var(--border-color);
      padding: 12px 20px;
      display: flex;
      justify-content: space-around;
      align-items: center;
      z-index: 100;
      box-shadow: 0 -4px 12px rgba(0, 0, 0, 0.05);
      max-width: 370px;
      margin: 0 auto;
    }
    .nav-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 8px;
      border-radius: 12px;
      transition: var(--transition-fast);
      cursor: pointer;
      width: 100%;
      text-align: center;
    }
    .nav-item:hover {
      background: var(--primary-50);
    }
    .nav-item.active {
      background: var(--primary-100);
      color: var(--primary-800);
    }
    .nav-icon {
      font-size: 1.2rem;
      margin-bottom: 4px;
    }
    .nav-label {
      font-size: 0.75rem;
      font-weight: 500;
    }
    /* Estilos para secciones dinámicas */
    .section-content {
      display: none;
    }
    .section-content.active {
      display: block;
      animation: fadeIn 0.3s ease-in-out;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    /* Estilos para materia de biblioteca */
    .subject-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 16px;
      margin-top: 20px;
    }
    .subject-item {
      background: var(--bg-card);
      border: 1px solid var(--border-color);
      border-radius: 16px;
      padding: 16px;
      transition: var(--transition-medium);
      cursor: pointer;
    }
    .subject-item:hover {
      background: var(--primary-50);
      transform: translateY(-2px);
      box-shadow: var(--shadow-md);
      border-color: var(--primary-200);
    }
    .subject-item.active {
      background: var(--primary-100);
      border-color: var(--primary-500);
      box-shadow: 0 4px 12px rgba(59, 130, 246, 0.15);
    }
    .subject-title {
      font-weight: 600;
      color: var(--primary-800);
      margin-bottom: 8px;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .subject-subtitle {
      font-size: 0.85rem;
      color: var(--text-secondary);
      margin-bottom: 8px;
    }
    .subject-stats {
      display: flex;
      justify-content: space-between;
      font-size: 0.85rem;
      color: var(--text-secondary);
    }
    .subject-stat {
      display: flex;
      align-items: center;
      gap: 4px;
    }
    .subject-stat i {
      font-size: 0.8rem;
    }
    /* Estilos para materia específica */
    .advanced-materias {
      display: grid;
      grid-template-columns: 1fr;
      gap: 16px;
      margin-top: 20px;
    }
    .materia-item {
      background: var(--bg-card);
      border: 1px solid var(--border-color);
      border-radius: 16px;
      padding: 16px;
      transition: var(--transition-medium);
      cursor: pointer;
    }
    .materia-item:hover {
      background: var(--primary-50);
      transform: translateY(-2px);
      box-shadow: var(--shadow-md);
      border-color: var(--primary-200);
    }
    .materia-item.active {
      background: var(--primary-100);
      border-color: var(--primary-500);
      box-shadow: 0 4px 12px rgba(59, 130, 246, 0.15);
    }
    .materia-title {
      font-weight: 600;
      color: var(--primary-800);
      margin-bottom: 8px;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .materia-subtitle {
      font-size: 0.85rem;
      color: var(--text-secondary);
      margin-bottom: 8px;
    }
    .materia-stats {
      display: flex;
      justify-content: space-between;
      font-size: 0.85rem;
      color: var(--text-secondary);
    }
    .materia-stat {
      display: flex;
      align-items: center;
      gap: 4px;
    }
    .materia-stat i {
      font-size: 0.8rem;
    }
    /* Estilos para cards sofisticadas */
    .sophisticated-card {
      background: var(--bg-card);
      border: 1px solid var(--border-color);
      border-radius: 16px;
      padding: 20px;
      box-shadow: var(--shadow-sm);
      transition: var(--transition-medium);
      margin-bottom: 20px;
    }
    .sophisticated-card:hover {
      box-shadow: var(--shadow-md);
      transform: translateY(-2px);
    }
    .sophisticated-header {
      background: var(--bg-header);
      color: white;
      padding: 20px;
      border-radius: 16px 16px 0 0;
      margin: -20px -20px 20px -20px;
    }
    .sophisticated-title {
      font-size: 1.2rem;
      font-weight: 700;
      margin-bottom: 8px;
    }
    .sophisticated-subtitle {
      font-size: 0.9rem;
      opacity: 0.9;
    }
    /* Botón de volver */
    .back-button {
      display: flex;
      align-items: center;
      gap: 8px;
      background: var(--primary-50);
      color: var(--primary-800);
      border: 1px solid var(--primary-200);
      border-radius: 8px;
      padding: 8px 12px;
      font-size: 0.9rem;
      cursor: pointer;
      transition: var(--transition-fast);
      margin-bottom: 16px;
      width: fit-content;
    }
    .back-button:hover {
      background: var(--primary-100);
      transform: translateY(-1px);
    }
    /* Indicador de carga */
    .loading-indicator {
      display: none;
      text-align: center;
      padding: 20px;
    }
    .loading-indicator.active {
      display: block;
    }
    .loading-spinner {
      width: 24px;
      height: 24px;
      border: 3px solid var(--primary-100);
      border-top: 3px solid var(--primary-500);
      border-radius: 50%;
      animation: spin 1s linear infinite;
      margin: 0 auto 10px;
    }
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
    /* Estilos para el modo oscuro */
    .dark-mode {
      --bg-primary: #0f172a;
      --bg-secondary: #1e293b;
      --bg-card: #1e293b;
      --text-primary: #ffffff;
      --text-secondary: #94a3b8;
      --border-color: #334155;
    }
    /* Toggle switch mejorado */
    .toggle-switch {
      position: relative;
      display: inline-block;
      width: 48px;
      height: 24px;
    }
    .toggle-switch input {
      opacity: 0;
      width: 0;
      height: 0;
    }
    .slider {
      position: absolute;
      cursor: pointer;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: #374151;
      transition: .4s;
      border-radius: 24px;
    }
    .slider:before {
      position: absolute;
      content: "";
      height: 16px;
      width: 16px;
      left: 4px;
      bottom: 4px;
      background-color: white;
      transition: .4s;
      border-radius: 50%;
    }
    input:checked + .slider {
      background-color: var(--primary-500);
    }
    input:checked + .slider:before {
      transform: translateX(24px);
    }
    /* Estilos para la configuración */
    .settings-grid {
      display: grid;
      gap: 16px;
    }
    .setting-item {
      padding: 16px;
      background: var(--bg-card);
      border-radius: 12px;
      border: 1px solid var(--border-color);
      transition: all 0.2s ease;
    }
    .setting-item:hover {
      background: var(--primary-50);
      border-color: var(--primary-200);
    }
    .setting-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 8px;
    }
    .setting-title {
      font-weight: 600;
      color: #ffffff;
    }
    /* Estilos para profesores */
    .professors-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 16px;
      margin-top: 20px;
    }
    .professor-item {
      background: var(--bg-card);
      border: 1px solid var(--border-color);
      border-radius: 16px;
      padding: 16px;
      transition: var(--transition-medium);
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 16px;
    }
    .professor-item:hover {
      background: var(--primary-50);
      transform: translateY(-2px);
      box-shadow: var(--shadow-md);
      border-color: var(--primary-200);
    }
    .professor-avatar {
      width: 50px;
      height: 50px;
      border-radius: 50%;
      background: var(--primary-100);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.2rem;
      color: var(--primary-800);
      font-weight: bold;
    }
    .professor-info {
      flex: 1;
    }
    .professor-name {
      font-weight: 600;
      color: var(--primary-800);
      margin-bottom: 4px;
    }
    .professor-specialty {
      font-size: 0.85rem;
      color: var(--text-secondary);
      margin-bottom: 8px;
    }
    .professor-rating {
      display: flex;
      align-items: center;
      gap: 4px;
      font-size: 0.85rem;
      color: var(--text-secondary);
    }
    .professor-rating i {
      color: gold;
    }
    /* Estilos para videos */
    .videos-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 16px;
      margin-top: 20px;
    }
    .video-item {
      background: var(--bg-card);
      border: 1px solid var(--border-color);
      border-radius: 16px;
      padding: 16px;
      transition: var(--transition-medium);
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 16px;
    }
    .video-item:hover {
      background: var(--primary-50);
      transform: translateY(-2px);
      box-shadow: var(--shadow-md);
      border-color: var(--primary-200);
    }
    .video-thumbnail {
      width: 80px;
      height: 60px;
      background: var(--primary-100);
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--primary-800);
      font-size: 1.5rem;
    }
    .video-info {
      flex: 1;
    }
    .video-title {
      font-weight: 600;
      color: var(--primary-800);
      margin-bottom: 4px;
    }
    .video-duration {
      font-size: 0.85rem;
      color: var(--text-secondary);
      margin-bottom: 8px;
    }
    .video-stats {
      display: flex;
      gap: 16px;
      font-size: 0.85rem;
      color: var(--text-secondary);
    }
    .video-stat {
      display: flex;
      align-items: center;
      gap: 4px;
    }
    .video-stat i {
      font-size: 0.8rem;
    }
    /* Estilos para la búsqueda */
    .search-container {
      position: relative;
      margin-bottom: 20px;
    }
    .search-input {
      width: 100%;
      padding: 12px 16px;
      border: 1px solid var(--border-color);
      border-radius: 12px;
      background: var(--bg-card);
      color: #ffffff;
      font-size: 0.95em;
      transition: var(--transition-fast);
    }
    .search-input:focus {
      outline: none;
      border-color: var(--primary-200);
      box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.1);
    }
    .search-icon {
      position: absolute;
      right: 16px;
      top: 50%;
      transform: translateY(-50%);
      color: var(--text-secondary);
    }
    /* Estilos para los filtros */
    .filters-container {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin-bottom: 20px;
    }
    .filter-tag {
      padding: 6px 12px;
      background: var(--primary-50);
      color: var(--primary-800);
      border-radius: 20px;
      font-size: 0.85rem;
      cursor: pointer;
      transition: var(--transition-fast);
    }
    .filter-tag:hover {
      background: var(--primary-100);
      transform: translateY(-1px);
    }
    .filter-tag.active {
      background: var(--primary-100);
      color: var(--primary-800);
    }
    /* Estilos para la barra de progreso del video */
    .video-progress {
      width: 100%;
      height: 4px;
      background: #374151;
      border-radius: 2px;
      margin-top: 8px;
      overflow: hidden;
    }
    .video-progress-fill {
      height: 100%;
      background: var(--primary-500);
      width: 60%;
      transition: width 0.5s ease;
    }
    /* Estilos para el botón de ver video */
    .watch-video-btn {
      display: flex;
      align-items: center;
      gap: 8px;
      background: var(--primary-500);
      color: white;
      border: none;
      border-radius: 8px;
      padding: 8px 16px;
      font-size: 0.9rem;
      cursor: pointer;
      transition: var(--transition-fast);
      margin-top: 8px;
    }
    .watch-video-btn:hover {
      background: var(--primary-600);
      transform: translateY(-1px);
    }
    /* Estilos para el estado de video completado */
    .video-completed {
      display: flex;
      align-items: center;
      gap: 8px;
      color: var(--secondary-500);
      font-size: 0.85rem;
      margin-top: 8px;
    }
    .video-completed i {
      color: var(--secondary-500);
    }
    /* Estilos para el modal de Premium */
    .modal-overlay {
      display: none; /* Oculto por defecto */
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.7); /* Fondo semi-transparente */
      z-index: 1000; /* Asegura que esté encima de todo */
      align-items: center;
      justify-content: center;
    }
    .modal-content {
      background-color: var(--bg-card);
      border: 1px solid var(--border-color);
      border-radius: 16px;
      padding: 24px;
      width: 90%;
      max-width: 320px;
      box-shadow: var(--shadow-lg);
      text-align: center;
      position: relative;
      transform: scale(0.95); /* Efecto de entrada */
      opacity: 0;
      transition: transform 0.3s ease, opacity 0.3s ease;
    }
    .modal-content.show {
      transform: scale(1);
      opacity: 1;
    }
    .modal-close {
      position: absolute;
      top: 12px;
      right: 12px;
      background: none;
      border: none;
      font-size: 1.2rem;
      color: var(--text-tertiary);
      cursor: pointer;
      transition: var(--transition-fast);
    }
    .modal-close:hover {
      color: #ffffff;
    }
    .modal-icon {
      font-size: 2.5rem;
      color: var(--accent-500);
      margin-bottom: 16px;
    }
    .modal-title {
      font-size: 1.4rem;
      font-weight: 700;
      color: #ffffff;
      margin-bottom: 8px;
    }
    .modal-price {
      font-size: 1.8rem;
      font-weight: 700;
      color: var(--secondary-500);
      margin-bottom: 16px;
    }
    .modal-features {
      list-style: none;
      padding: 0;
      margin: 0 0 20px 0;
      text-align: left;
    }
    .modal-features li {
      padding: 8px 0;
      display: flex;
      align-items: center;
      gap: 8px;
      color: var(--text-secondary);
    }
    .modal-features li i {
      color: var(--secondary-500);
    }
    .modal-button {
      display: block;
      width: 100%;
      padding: 14px;
      background: var(--secondary-500);
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 1rem;
      font-weight: 600;
      cursor: pointer;
      transition: var(--transition-fast);
    }
    .modal-button:hover {
      background: #059669; /* Verde más oscuro */
      transform: translateY(-1px);
    }
  </style>
</head>
<body>
  <!-- NUEVA PANTALLA DE INICIO -->
  <div class="login-screen" id="login-screen">
      <div class="login-card">
          <i class="fas fa-graduation-cap login-icon"></i>
          <h1 class="login-title">Bienvenido de Nuevo</h1>
          <p class="login-subtitle">Inicia sesión para continuar tu viaje de aprendizaje</p>
          <form id="login-form">
              <div class="input-group">
                  <label for="nombre" class="input-label">Nombre Completo</label>
                  <input type="text" id="nombre" class="input-field" placeholder="Ej: María González" required>
              </div>
              <div class="input-group">
                  <label for="gmail" class="input-label">Correo Electrónico</label>
                  <input type="email" id="gmail" class="input-field" placeholder="tu@email.com" required>
              </div>
              <div class="input-group">
                  <label for="institucion" class="input-label">Universidad / Colegio</label>
                  <input type="text" id="institucion" class="input-field" placeholder="Ej: Universidad Nacional" required>
              </div>
              <button type="submit" class="login-button">Siguiente</button> <!-- Cambiado el texto -->
          </form>
          <p class="login-footer">Al iniciar sesión, aceptas nuestros Términos de Uso y Política de Privacidad.</p>
      </div>
  </div>
  <!-- FIN NUEVA PANTALLA DE INICIO -->

  <div class="mobile-frame">
    <div class="mobile-topbar">
      <span>9:41</span>
      <span class="status"><span class="icon">🟢</span> <span class="icon">📶</span> <span class="icon">Wi-Fi</span> <span class="icon">🔋</span></span>
    </div>
    <div class="mobile-notch">
      <span class="notch-dot"></span>
      <span class="notch-dot cam"></span>
      <span class="notch-dot small"></span>
    </div>
    <div class="app-inside" id="app-inside" tabindex="0">
      <!-- Botón Premium -->
      <button class="premium-button" id="premium-button">
        <i class="fas fa-crown"></i> <!-- Ícono de corona -->
        Cambiate a Premium
      </button>
      <!-- Loader -->
      <div class="loader-screen" id="loader-screen">
        <div class="loader-dot"></div>
        <div class="loader-text">Cargando...</div>
      </div>
      <main class="container" id="profile-content" style="opacity:0;pointer-events:none;">
        <!-- Encabezado -->
        <header class="profile-header" role="banner" aria-label="Encabezado de perfil">
          <div class="avatar-wrapper">
            <div class="avatar" aria-label="Avatar de María González" role="img">
              <img src="https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1887&q=80" alt="María González">
            </div>
            <div class="badge-nivel" title="Nivel actual">
              <span class="badge-nivel-emoji">🏅</span>
              Nivel 8
            </div>
          </div>
          <div class="profile-info">
            <h1 id="display-nombre">María González</h1> <!-- ID agregado -->
            <div class="email" id="display-email">maria.gonzalez@universidad.edu</div> <!-- ID agregado -->
            <div class="university" id="display-institucion">Universidad Nacional • Ingeniería</div> <!-- ID agregado -->
          </div>
          <div class="xp-bar-container" aria-label="Barra de progreso de experiencia">
            <div class="xp-bar-labels">
              <span>XP</span>
              <span id="xp-label">2,340 / 3,000 XP</span>
            </div>
            <div class="xp-bar-bg">
              <div class="xp-bar-fill" id="xp-bar"></div>
            </div>
            <div class="xp-bar-percent" id="xp-percent">78%</div>
          </div>
        </header>
        <!-- Estadísticas -->
        <section>
          <div class="stats-grid" role="region" aria-label="Estadísticas">
            <div class="stat-card" tabindex="0">
              <div class="stat-icon stat-blue" aria-hidden="true">🎯</div>
              <div class="stat-details">
                <div class="stat-value">47</div>
                <div class="stat-label">Retos Completados</div>
              </div>
            </div>
            <div class="stat-card" tabindex="0">
              <div class="stat-icon stat-green" aria-hidden="true">⏰</div>
              <div class="stat-details">
                <div class="stat-value">23.5</div>
                <div class="stat-label">Horas Estudiadas</div>
              </div>
            </div>
            <div class="stat-card" tabindex="0">
              <div class="stat-icon stat-yellow" aria-hidden="true">⭐</div>
              <div class="stat-details">
                <div class="stat-value">2,340</div>
                <div class="stat-label">XP Total</div>
              </div>
            </div>
            <div class="stat-card" tabindex="0">
              <div class="stat-icon stat-purple" aria-hidden="true">📈</div>
              <div class="stat-details">
                <div class="stat-value">5 días</div>
                <div class="stat-label">Racha Actual</div>
              </div>
            </div>
          </div>
        </section>
        <!-- Actividad reciente -->
        <section>
          <h2 class="section-title">Actividad reciente</h2>
          <ul class="activity-list">
            <li class="activity-item" tabindex="0">
              <div class="activity-icon activity-yellow" aria-hidden="true">🏆</div>
              <div class="activity-details">
                <div class="activity-desc">Completaste "Domina las derivadas"</div>
                <div class="activity-meta">Hace 2 horas</div>
              </div>
              <div class="activity-xp">+50 XP</div>
            </li>
            <li class="activity-item" tabindex="0">
              <div class="activity-icon activity-green" aria-hidden="true">📅</div>
              <div class="activity-details">
                <div class="activity-desc">Sesión con Dr. Roberto Martínez</div>
                <div class="activity-meta">Ayer</div>
              </div>
              <div class="activity-xp">+75 XP</div>
            </li>
            <li class="activity-item" tabindex="0">
              <div class="activity-icon activity-purple" aria-hidden="true">📖</div>
              <div class="activity-details">
                <div class="activity-desc">Leíste "Guía de Integrales"</div>
                <div class="activity-meta">Hace 3 días</div>
              </div>
              <div class="activity-xp">+25 XP</div>
            </li>
          </ul>
        </section>
        <!-- Logros -->
        <section>
          <h2 class="section-title">Logros</h2>
          <ul class="achievements-list">
            <li class="achievement-item" tabindex="0">
              <div class="achievement-row">
                <span class="achievement-label">🔥 Racha de Fuego</span>
                <span class="achievement-status" style="color:var(--secondary-500)">Obtenido</span>
              </div>
              <div class="achievement-description">Completa retos 7 días seguidos</div>
            </li>
            <li class="achievement-item" tabindex="0">
              <div class="achievement-row">
                <span class="achievement-label">📐 Maestro del Cálculo</span>
                <span class="achievement-status" style="color:var(--secondary-500)">Obtenido</span>
              </div>
              <div class="achievement-description">Completa 50 retos de Cálculo I</div>
            </li>
            <li class="achievement-item achievement-disabled" tabindex="0" aria-disabled="true">
              <div class="achievement-row">
                <span class="achievement-label">⭐ Estudiante Estrella</span>
                <span class="achievement-status">8/10 progreso</span>
              </div>
              <div class="achievement-description">Alcanza el top 10% en tu universidad</div>
              <div class="achievement-progress-bar">
                <div class="achievement-progress-fill" style="background:var(--accent-500)" id="achieve-estrella"></div>
              </div>
            </li>
            <li class="achievement-item achievement-disabled" tabindex="0" aria-disabled="true">
              <div class="achievement-row">
                <span class="achievement-label">👨‍🏫 Tutor Favorito</span>
                <span class="achievement-status">12/20 progreso</span>
              </div>
              <div class="achievement-description">Completa 20 sesiones con tutores</div>
              <div class="achievement-progress-bar">
                <div class="achievement-progress-fill" style="background:var(--purple-500)" id="achieve-tutor"></div>
              </div>
            </li>
          </ul>
        </section>
        <!-- Menú de configuración -->
        <nav class="menu-section" aria-label="Menú de configuración">
          <ul class="menu-list">
            <li>
              <button class="menu-item" tabindex="0" data-section="inicio">
                <span class="menu-icon" aria-hidden="true">🏠</span>
                Inicio
              </button>
            </li>
            <li>
              <button class="menu-item" tabindex="0" data-section="biblioteca">
                <span class="menu-icon" aria-hidden="true">📚</span>
                Biblioteca
              </button>
            </li>
            <li>
              <button class="menu-item" tabindex="0" data-section="videos">
                <span class="menu-icon" aria-hidden="true">🎬</span>
                Videos
              </button>
            </li>
            <li>
              <button class="menu-item" tabindex="0" data-section="profesores">
                <span class="menu-icon menu-green" aria-hidden="true">👨‍🏫</span>
                Profesores
              </button>
            </li>
            <li>
              <button class="menu-item" tabindex="0" data-section="progreso">
                <span class="menu-icon menu-purple" aria-hidden="true">📊</span>
                Mi Progreso
              </button>
            </li>
            <li>
              <button class="menu-item" tabindex="0" data-section="configuracion">
                <span class="menu-icon menu-purple" aria-hidden="true">⚙️</span>
                Configuración
              </button>
            </li>
            <li>
              <button class="menu-item menu-logout" tabindex="0" data-section="logout">
                <span class="menu-icon menu-red" aria-hidden="true">🚪</span>
                Cerrar Sesión
              </button>
            </li>
          </ul>
        </nav>
        <!-- Secciones dinámicas -->
        <div id="section-content">
          <!-- Sección de materias de biblioteca -->
          <div class="section-content" id="materias-section">
            <div class="sophisticated-card">
              <div class="sophisticated-header">
                <div class="sophisticated-title">📚 Biblioteca de Materias</div>
                <div class="sophisticated-subtitle">Selecciona una materia para ver sus recursos</div>
              </div>
              <div class="subject-grid">
                <div class="subject-item" data-materia="calculo">
                  <div class="subject-title">
                    <i class="fas fa-calculator"></i>
                    Cálculo
                  </div>
                  <div class="subject-subtitle">Fundamentos de cálculo diferencial e integral</div>
                  <div class="subject-stats">
                    <div class="subject-stat"><i class="fas fa-book"></i> 12 recursos</div>
                    <div class="subject-stat"><i class="fas fa-star"></i> 4.8/5</div>
                  </div>
                </div>
                <div class="subject-item" data-materia="ecuaciones">
                  <div class="subject-title">
                    <i class="fas fa-equation"></i>
                    Ecuaciones Diferenciales
                  </div>
                  <div class="subject-subtitle">Solución de ecuaciones diferenciales ordinarias</div>
                  <div class="subject-stats">
                    <div class="subject-stat"><i class="fas fa-book"></i> 8 recursos</div>
                    <div class="subject-stat"><i class="fas fa-star"></i> 4.7/5</div>
                  </div>
                </div>
                <div class="subject-item" data-materia="avanzadas">
                  <div class="subject-title">
                    <i class="fas fa-graduation-cap"></i>
                    Materias Avanzadas
                  </div>
                  <div class="subject-subtitle">Cursos de nivel superior y especializados</div>
                  <div class="subject-stats">
                    <div class="subject-stat"><i class="fas fa-book"></i> 15 recursos</div>
                    <div class="subject-stat"><i class="fas fa-star"></i> 4.9/5</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <!-- Sección de materias específicas -->
          <div class="section-content" id="calculo-section">
            <div class="back-button" id="back-calculo">
              <i class="fas fa-arrow-left"></i>
              Volver a materias
            </div>
            <div class="sophisticated-card">
              <div class="sophisticated-header">
                <div class="sophisticated-title">🔢 Cálculo</div>
                <div class="sophisticated-subtitle">Fundamentos de cálculo diferencial e integral</div>
              </div>
              <div class="advanced-materias">
                <div class="materia-item">
                  <div class="materia-title">
                    <i class="fas fa-calculator"></i>
                    Cálculo I
                  </div>
                  <div class="materia-subtitle">Límites, continuidad y derivadas</div>
                  <div class="materia-stats">
                    <div class="materia-stat"><i class="fas fa-book"></i> 5 recursos</div>
                    <div class="materia-stat"><i class="fas fa-clock"></i> 12h</div>
                  </div>
                </div>
                <div class="materia-item">
                  <div class="materia-title">
                    <i class="fas fa-calculator"></i>
                    Cálculo II
                  </div>
                  <div class="materia-subtitle">Integrales y aplicaciones</div>
                  <div class="materia-stats">
                    <div class="materia-stat"><i class="fas fa-book"></i> 4 recursos</div>
                    <div class="materia-stat"><i class="fas fa-clock"></i> 10h</div>
                  </div>
                </div>
                <div class="materia-item">
                  <div class="materia-title">
                    <i class="fas fa-calculator"></i>
                    Cálculo III
                  </div>
                  <div class="materia-subtitle">Cálculo multivariable y vectores</div>
                  <div class="materia-stats">
                    <div class="materia-stat"><i class="fas fa-book"></i> 3 recursos</div>
                    <div class="materia-stat"><i class="fas fa-clock"></i> 8h</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="section-content" id="ecuaciones-section">
            <div class="back-button" id="back-ecuaciones">
              <i class="fas fa-arrow-left"></i>
              Volver a materias
            </div>
            <div class="sophisticated-card">
              <div class="sophisticated-header">
                <div class="sophisticated-title">🔄 Ecuaciones Diferenciales</div>
                <div class="sophisticated-subtitle">Solución de ecuaciones diferenciales ordinarias</div>
              </div>
              <div class="advanced-materias">
                <div class="materia-item">
                  <div class="materia-title">
                    <i class="fas fa-equation"></i>
                    Ecuaciones Diferenciales I
                  </div>
                  <div class="materia-subtitle">Ecuaciones de primer orden</div>
                  <div class="materia-stats">
                    <div class="materia-stat"><i class="fas fa-book"></i> 3 recursos</div>
                    <div class="materia-stat"><i class="fas fa-clock"></i> 8h</div>
                  </div>
                </div>
                <div class="materia-item">
                  <div class="materia-title">
                    <i class="fas fa-equation"></i>
                    Ecuaciones Diferenciales II
                  </div>
                  <div class="materia-subtitle">Ecuaciones de segundo orden</div>
                  <div class="materia-stats">
                    <div class="materia-stat"><i class="fas fa-book"></i> 3 recursos</div>
                    <div class="materia-stat"><i class="fas fa-clock"></i> 8h</div>
                  </div>
                </div>
                <div class="materia-item">
                  <div class="materia-title">
                    <i class="fas fa-equation"></i>
                    Sistemas de Ecuaciones Diferenciales
                  </div>
                  <div class="materia-subtitle">Sistemas lineales y no lineales</div>
                  <div class="materia-stats">
                    <div class="materia-stat"><i class="fas fa-book"></i> 2 recursos</div>
                    <div class="materia-stat"><i class="fas fa-clock"></i> 6h</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="section-content" id="avanzadas-section">
            <div class="back-button" id="back-avanzadas">
              <i class="fas fa-arrow-left"></i>
              Volver a materias
            </div>
            <div class="sophisticated-card">
              <div class="sophisticated-header">
                <div class="sophisticated-title">🎓 Materias Avanzadas</div>
                <div class="sophisticated-subtitle">Cursos de nivel superior y especializados</div>
              </div>
              <div class="advanced-materias">
                <div class="materia-item">
                  <div class="materia-title">
                    <i class="fas fa-graduation-cap"></i>
                    Análisis Numérico
                  </div>
                  <div class="materia-subtitle">Métodos numéricos para resolver problemas matemáticos</div>
                  <div class="materia-stats">
                    <div class="materia-stat"><i class="fas fa-book"></i> 4 recursos</div>
                    <div class="materia-stat"><i class="fas fa-clock"></i> 10h</div>
                  </div>
                </div>
                <div class="materia-item">
                  <div class="materia-title">
                    <i class="fas fa-graduation-cap"></i>
                    Álgebra Lineal Avanzada
                  </div>
                  <div class="materia-subtitle">Espacios vectoriales y transformaciones lineales</div>
                  <div class="materia-stats">
                    <div class="materia-stat"><i class="fas fa-book"></i> 3 recursos</div>
                    <div class="materia-stat"><i class="fas fa-clock"></i> 9h</div>
                  </div>
                </div>
                <div class="materia-item">
                  <div class="materia-title">
                    <i class="fas fa-graduation-cap"></i>
                    Teoría de Probabilidades
                  </div>
                  <div class="materia-subtitle">Conceptos avanzados de probabilidad y estadística</div>
                  <div class="materia-stats">
                    <div class="materia-stat"><i class="fas fa-book"></i> 3 recursos</div>
                    <div class="materia-stat"><i class="fas fa-clock"></i> 9h</div>
                  </div>
                </div>
                <div class="materia-item">
                  <div class="materia-title">
                    <i class="fas fa-graduation-cap"></i>
                    Optimización
                  </div>
                  <div class="materia-subtitle">Métodos de optimización y programación matemática</div>
                  <div class="materia-stats">
                    <div class="materia-stat"><i class="fas fa-book"></i> 3 recursos</div>
                    <div class="materia-stat"><i class="fas fa-clock"></i> 8h</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <!-- Sección de configuración -->
          <div class="section-content" id="configuracion-section">
            <div class="sophisticated-card">
              <div class="sophisticated-header">
                <div class="sophisticated-title">⚙️ Configuración</div>
                <div class="sophisticated-subtitle">Personaliza tu experiencia de aprendizaje</div>
              </div>
              <div class="settings-grid">
                <div class="setting-item">
                  <div class="setting-header">
                    <span class="setting-title">Notificaciones Push</span>
                    <label class="toggle-switch">
                      <input type="checkbox" checked>
                      <span class="slider"></span>
                    </label>
                  </div>
                  <p>Recibe notificaciones sobre nuevos contenidos y recordatorios</p>
                </div>
                <div class="setting-item">
                  <div class="setting-header">
                    <span class="setting-title">Modo Oscuro</span>
                    <label class="toggle-switch">
                      <input type="checkbox" id="dark-mode-toggle">
                      <span class="slider"></span>
                    </label>
                  </div>
                  <p>Activa el tema oscuro para reducir la fatiga visual</p>
                </div>
                <div class="setting-item">
                  <div class="setting-header">
                    <span class="setting-title">Recordatorios Diarios</span>
                    <label class="toggle-switch">
                      <input type="checkbox" checked>
                      <span class="slider"></span>
                    </label>
                  </div>
                  <p>Recibe recordatorios para tus sesiones de estudio programadas</p>
                </div>
                <div class="setting-item">
                  <div class="setting-header">
                    <span class="setting-title">Sincronización en la Nube</span>
                    <label class="toggle-switch">
                      <input type="checkbox" checked>
                      <span class="slider"></span>
                    </label>
                  </div>
                  <p>Sincroniza tu progreso y configuración en todos tus dispositivos</p>
                </div>
              </div>
            </div>
          </div>
          <!-- Sección de videos -->
          <div class="section-content" id="videos-section">
            <div class="sophisticated-card">
              <div class="sophisticated-header">
                <div class="sophisticated-title">🎬 Videos Educativos</div>
                <div class="sophisticated-subtitle">Clases cortas, explicaciones visuales y tutoriales por tema</div>
              </div>
              <!-- Búsqueda -->
              <div class="search-container">
                <input type="text" class="search-input" placeholder="Buscar videos...">
                <i class="fas fa-search search-icon"></i>
              </div>
              <!-- Filtros -->
              <div class="filters-container">
                <div class="filter-tag active">Todos</div>
                <div class="filter-tag">Matemáticas</div>
                <div class="filter-tag">Física</div>
                <div class="filter-tag">Biología</div>
                <div class="filter-tag">Literatura</div>
              </div>
              <!-- Lista de videos -->
              <div class="videos-grid">
                <div class="video-item">
                  <div class="video-thumbnail">
                    <i class="fas fa-play"></i>
                  </div>
                  <div class="video-info">
                    <div class="video-title">Domina las derivadas</div>
                    <div class="video-duration">12:30 min</div>
                    <div class="video-stats">
                      <div class="video-stat"><i class="fas fa-eye"></i> 2.5K vistas</div>
                      <div class="video-stat"><i class="fas fa-thumbs-up"></i> 98%</div>
                    </div>
                    <div class="video-progress">
                      <div class="video-progress-fill"></div>
                    </div>
                    <div class="video-completed">
                      <i class="fas fa-check-circle"></i>
                      Completado
                    </div>
                  </div>
                </div>
                <div class="video-item">
                  <div class="video-thumbnail">
                    <i class="fas fa-play"></i>
                  </div>
                  <div class="video-info">
                    <div class="video-title">Integrales básicas</div>
                    <div class="video-duration">15:45 min</div>
                    <div class="video-stats">
                      <div class="video-stat"><i class="fas fa-eye"></i> 1.8K vistas</div>
                      <div class="video-stat"><i class="fas fa-thumbs-up"></i> 95%</div>
                    </div>
                    <div class="video-progress">
                      <div class="video-progress-fill" style="width: 75%"></div>
                    </div>
                    <button class="watch-video-btn">
                      <i class="fas fa-play"></i>
                      Ver Video
                    </button>
                  </div>
                </div>
                <div class="video-item">
                  <div class="video-thumbnail">
                    <i class="fas fa-play"></i>
                  </div>
                  <div class="video-info">
                    <div class="video-title">Resolución de ecuaciones diferenciales</div>
                    <div class="video-duration">20:15 min</div>
                    <div class="video-stats">
                      <div class="video-stat"><i class="fas fa-eye"></i> 3.2K vistas</div>
                      <div class="video-stat"><i class="fas fa-thumbs-up"></i> 97%</div>
                    </div>
                    <div class="video-progress">
                      <div class="video-progress-fill" style="width: 40%"></div>
                    </div>
                    <button class="watch-video-btn">
                      <i class="fas fa-play"></i>
                      Ver Video
                    </button>
                  </div>
                </div>
                <div class="video-item">
                  <div class="video-thumbnail">
                    <i class="fas fa-play"></i>
                  </div>
                  <div class="video-info">
                    <div class="video-title">Teorema fundamental del cálculo</div>
                    <div class="video-duration">18:20 min</div>
                    <div class="video-stats">
                      <div class="video-stat"><i class="fas fa-eye"></i> 2.1K vistas</div>
                      <div class="video-stat"><i class="fas fa-thumbs-up"></i> 96%</div>
                    </div>
                    <div class="video-progress">
                      <div class="video-progress-fill" style="width: 0%"></div>
                    </div>
                    <button class="watch-video-btn">
                      <i class="fas fa-play"></i>
                      Ver Video
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <!-- Sección de profesores -->
          <div class="section-content" id="profesores-section">
            <div class="sophisticated-card">
              <div class="sophisticated-header">
                <div class="sophisticated-title">👨‍🏫 Profesores</div>
                <div class="sophisticated-subtitle">Elige un profesor para recibir clases personalizadas</div>
              </div>
              <!-- Búsqueda -->
              <div class="search-container">
                <input type="text" class="search-input" placeholder="Buscar profesores...">
                <i class="fas fa-search search-icon"></i>
              </div>
              <!-- Filtros -->
              <div class="filters-container">
                <div class="filter-tag active">Todos</div>
                <div class="filter-tag">Matemáticas</div>
                <div class="filter-tag">Física</div>
                <div class="filter-tag">Biología</div>
                <div class="filter-tag">Literatura</div>
              </div>
              <!-- Lista de profesores -->
              <div class="professors-grid">
                <div class="professor-item">
                  <div class="professor-avatar">RM</div>
                  <div class="professor-info">
                    <div class="professor-name">Dr. Roberto Martínez</div>
                    <div class="professor-specialty">Matemáticas - Cálculo</div>
                    <div class="professor-rating">
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star-half-alt"></i>
                      <span>4.5/5</span>
                    </div>
                  </div>
                </div>
                <div class="professor-item">
                  <div class="professor-avatar">LC</div>
                  <div class="professor-info">
                    <div class="professor-name">Dra. Laura Contreras</div>
                    <div class="professor-specialty">Física - Mecánica</div>
                    <div class="professor-rating">
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <span>5.0/5</span>
                    </div>
                  </div>
                </div>
                <div class="professor-item">
                  <div class="professor-avatar">JP</div>
                  <div class="professor-info">
                    <div class="professor-name">Dr. Juan Pérez</div>
                    <div class="professor-specialty">Biología - Genética</div>
                    <div class="professor-rating">
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star-half-alt"></i>
                      <span>4.5/5</span>
                    </div>
                  </div>
                </div>
                <div class="professor-item">
                  <div class="professor-avatar">MS</div>
                  <div class="professor-info">
                    <div class="professor-name">Dra. María Sánchez</div>
                    <div class="professor-specialty">Literatura - Clásicos</div>
                    <div class="professor-rating">
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <span>5.0/5</span>
                    </div>
                  </div>
                </div>
                <div class="professor-item">
                  <div class="professor-avatar">AG</div>
                  <div class="professor-info">
                    <div class="professor-name">Dr. Alejandro Gómez</div>
                    <div class="professor-specialty">Química - Orgánica</div>
                    <div class="professor-rating">
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star"></i>
                      <i class="fas fa-star-half-alt"></i>
                      <span>4.5/5</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <!-- Sección de progreso -->
          <div class="section-content" id="progreso-section">
            <div class="sophisticated-card">
              <div class="sophisticated-header">
                <div class="sophisticated-title">📊 Mi Progreso</div>
                <div class="sophisticated-subtitle">Seguimiento de tu avance en diferentes áreas de estudio</div>
              </div>
              <div class="progress-container">
                <div class="progress-item">
                  <div class="progress-header">
                    <span class="progress-title">Matemáticas</span>
                    <span class="progress-percentage">75%</span>
                  </div>
                  <div class="progress-bar">
                    <div class="progress-fill" style="width: 75%"></div>
                  </div>
                </div>
                <div class="progress-item">
                  <div class="progress-header">
                    <span class="progress-title">Física</span>
                    <span class="progress-percentage">60%</span>
                  </div>
                  <div class="progress-bar">
                    <div class="progress-fill" style="width: 60%"></div>
                  </div>
                </div>
                <div class="progress-item">
                  <div class="progress-header">
                    <span class="progress-title">Biología</span>
                    <span class="progress-percentage">85%</span>
                  </div>
                  <div class="progress-bar">
                    <div class="progress-fill" style="width: 85%"></div>
                  </div>
                </div>
                <div class="progress-item">
                  <div class="progress-header">
                    <span class="progress-title">Literatura</span>
                    <span class="progress-percentage">45%</span>
                  </div>
                  <div class="progress-bar">
                    <div class="progress-fill" style="width: 45%"></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </main>
    </div>
    <!-- Barra de navegación inferior -->
    <div class="bottom-nav" id="bottom-nav">
      <div class="nav-item active" data-section="inicio">
        <div class="nav-icon"><i class="fas fa-home"></i></div>
        <div class="nav-label">Inicio</div>
      </div>
      <div class="nav-item" data-section="biblioteca">
        <div class="nav-icon"><i class="fas fa-book"></i></div>
        <div class="nav-label">Biblioteca</div>
      </div>
      <div class="nav-item" data-section="progreso">
        <div class="nav-icon"><i class="fas fa-chart-line"></i></div>
        <div class="nav-label">Progreso</div>
      </div>
      <div class="nav-item" data-section="perfil">
        <div class="nav-icon"><i class="fas fa-user"></i></div>
        <div class="nav-label">Perfil</div>
      </div>
    </div>
    <!-- Modal de Premium -->
    <div class="modal-overlay" id="premium-modal">
      <div class="modal-content">
        <button class="modal-close" id="close-modal">&times;</button>
        <div class="modal-icon">
          <i class="fas fa-crown"></i>
        </div>
        <h2 class="modal-title">¡Mejora tu experiencia!</h2>
        <div class="modal-price">$10 / mes</div>
        <ul class="modal-features">
          <li><i class="fas fa-check-circle"></i> Sesiones 1:1 privadas con docentes</li>
          <li><i class="fas fa-check-circle"></i> Apuntes y recursos en alta calidad</li>
          <li><i class="fas fa-check-circle"></i> Contenido exclusivo</li>
          <li><i class="fas fa-check-circle"></i> Sin anuncios</li>
          <li><i class="fas fa-check-circle"></i> Acceso anticipado a nuevas funciones</li>
        </ul>
        <button class="modal-button" id="subscribe-button">Suscribirse Ahora</button>
      </div>
    </div>
  </div>
  <script>
    // Simula loader y animación
    const xpActual = 2340;
    const xpTotal = 3000;
    const xpPorcentaje = Math.round((xpActual / xpTotal) * 100);
    window.addEventListener('DOMContentLoaded', function() {
      // --- CÓDIGO PARA LOGIN ---
      const loginScreen = document.getElementById('login-screen');
      const loginForm = document.getElementById('login-form');
      const displayNombre = document.getElementById('display-nombre');
      const displayEmail = document.getElementById('display-email');
      const displayInstitucion = document.getElementById('display-institucion');

      // Manejar el envío del formulario de login
      loginForm.addEventListener('submit', function(e) {
          e.preventDefault(); // Evita el envío por defecto del formulario

          // Obtener valores del formulario
          const nombre = document.getElementById('nombre').value;
          const email = document.getElementById('gmail').value;
          const institucion = document.getElementById('institucion').value;

          // Simular validación (puedes reemplazar con lógica real)
          if (nombre && email && institucion) {
              // Actualizar datos del perfil con los valores del login
              displayNombre.textContent = nombre;
              displayEmail.textContent = email;
              displayInstitucion.textContent = `${institucion} • Ingeniería`; // Asumiendo una carrera fija por simplicidad

              // Ocultar pantalla de login con animación
              loginScreen.classList.add('hidden');

              // Simular el loader y mostrar el perfil (código original)
              setTimeout(() => {
                document.getElementById('loader-screen').style.opacity = '0';
                setTimeout(() => {
                  document.getElementById('loader-screen').style.display = 'none';
                  const main = document.getElementById('profile-content');
                  main.style.opacity = '1';
                  main.style.pointerEvents = 'auto';
                  // Barra XP
                  const xpBar = document.getElementById('xp-bar');
                  if (xpBar) { setTimeout(() => { xpBar.style.width = xpPorcentaje + '%'; }, 100);}
                  const xpPercent = document.getElementById('xp-percent');
                  if (xpPercent) { xpPercent.textContent = xpPorcentaje + '%'; }
                  // Progreso de logros
                  const estrella = document.getElementById('achieve-estrella');
                  if (estrella) { setTimeout(() => { estrella.style.width = (8/10 * 100) + '%'; }, 250);}
                  const tutor = document.getElementById('achieve-tutor');
                  if (tutor) { setTimeout(() => { tutor.style.width = (12/20 * 100) + '%'; }, 300);}
                }, 840);
              }, 1200);
          } else {
              alert('Por favor, completa todos los campos.');
          }
      });
      // --- FIN CÓDIGO PARA LOGIN ---

      // Accesibilidad: teclas para tarjetas y menú
      const focusables = document.querySelectorAll('.stat-card, .activity-item, .achievement-item, .menu-item');
      focusables.forEach(el => {
        el.addEventListener('keydown', function(e) {
          if (e.key === "Enter" || e.key === " ") { e.preventDefault(); el.click && el.click(); }
        });
      });
      // Cerrar sesión demo
      document.querySelector('.menu-logout').addEventListener('click', function() {
        if (confirm('¿Estás seguro que deseas cerrar sesión?')) {
          // Volver a mostrar la pantalla de login
          document.getElementById('profile-content').style.opacity = '0';
          document.getElementById('profile-content').style.pointerEvents = 'none';
          document.getElementById('loader-screen').style.display = 'flex';
          document.getElementById('loader-screen').style.opacity = '1';
          setTimeout(() => {
            loginScreen.classList.remove('hidden');
            document.getElementById('loader-screen').style.display = 'none';
          }, 800);
        }
      });
      // Sistema de navegación
      const menuItems = document.querySelectorAll('.menu-item');
      const navItems = document.querySelectorAll('.nav-item');
      const subjectItems = document.querySelectorAll('.subject-item');
      const backButtons = document.querySelectorAll('.back-button');
      const darkModeToggle = document.getElementById('dark-mode-toggle');
      // Función para mostrar sección
      function showSection(sectionId) {
        // Ocultar todas las secciones
        document.querySelectorAll('.section-content').forEach(section => {
          section.classList.remove('active');
        });
        // Mostrar la sección seleccionada
        const targetSection = document.getElementById(`${sectionId}-section`);
        if (targetSection) {
          targetSection.classList.add('active');
        }
        // Actualizar menú activo
        menuItems.forEach(item => {
          item.classList.remove('active');
          if (item.getAttribute('data-section') === sectionId) {
            item.classList.add('active');
          }
        });
        // Actualizar navegación inferior
        navItems.forEach(item => {
          item.classList.remove('active');
          if (item.getAttribute('data-section') === sectionId) {
            item.classList.add('active');
          }
        });
      }
      // Eventos para menú lateral
      menuItems.forEach(item => {
        item.addEventListener('click', function() {
          const section = this.getAttribute('data-section');
          if (section === 'logout') {
            if (confirm('¿Estás seguro que deseas cerrar sesión?')) {
              // Volver a mostrar la pantalla de login
              document.getElementById('profile-content').style.opacity = '0';
              document.getElementById('profile-content').style.pointerEvents = 'none';
              document.getElementById('loader-screen').style.display = 'flex';
              document.getElementById('loader-screen').style.opacity = '1';
              setTimeout(() => {
                loginScreen.classList.remove('hidden');
                document.getElementById('loader-screen').style.display = 'none';
              }, 800);
            }
          } else if (section === 'biblioteca') {
            showSection('materias');
          } else {
            showSection(section);
          }
        });
      });
      // Eventos para navegación inferior
      navItems.forEach(item => {
        item.addEventListener('click', function() {
          const section = this.getAttribute('data-section');
          if (section === 'biblioteca') {
            showSection('materias');
          } else {
            showSection(section);
          }
        });
      });
      // Eventos para materias de biblioteca
      subjectItems.forEach(item => {
        item.addEventListener('click', function() {
          const materia = this.getAttribute('data-materia');
          showSection(materia);
        });
      });
      // Eventos para botones de volver
      backButtons.forEach(button => {
        button.addEventListener('click', function() {
          showSection('materias');
        });
      });
      // Evento para modo oscuro
      if (darkModeToggle) {
        darkModeToggle.addEventListener('change', function() {
          if (this.checked) {
            document.body.classList.add('dark-mode');
          } else {
            document.body.classList.remove('dark-mode');
          }
        });
      }
      // Eventos para filtros
      const filterTags = document.querySelectorAll('.filter-tag');
      filterTags.forEach(tag => {
        tag.addEventListener('click', function() {
          filterTags.forEach(t => t.classList.remove('active'));
          this.classList.add('active');
        });
      });
      // --- Código nuevo para el modal Premium ---
      const premiumButton = document.getElementById('premium-button');
      const modal = document.getElementById('premium-modal');
      const closeModal = document.getElementById('close-modal');
      const subscribeButton = document.getElementById('subscribe-button');
      // Abrir modal
      premiumButton.addEventListener('click', function() {
        modal.style.display = 'flex';
        setTimeout(() => {
          document.querySelector('.modal-content').classList.add('show');
        }, 10); // Pequeño delay para que funcione la animación
      });
      // Cerrar modal (X y overlay)
      function closePremiumModal() {
         document.querySelector('.modal-content').classList.remove('show');
         setTimeout(() => {
            modal.style.display = 'none';
         }, 300); // Espera a que termine la animación
      }
      closeModal.addEventListener('click', closePremiumModal);
      modal.addEventListener('click', function(e) {
        if (e.target === modal) { // Si se hace click en el overlay
          closePremiumModal();
        }
      });
      // Botón de suscripción (simulado)
      subscribeButton.addEventListener('click', function() {
        alert('¡Gracias por tu interés! Redirigiendo al proceso de pago...');
        // Aquí iría la lógica real de pago
        closePremiumModal(); // Cierra el modal después de hacer clic
      });
      // --- Fin del código nuevo ---
    });
  </script>
</body>
</html>
