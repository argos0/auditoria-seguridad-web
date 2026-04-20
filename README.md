# 🛡️ Auditoría de Seguridad Web — WordPress Site
### Proyecto de Portafolio | Ethical Hacking & Penetration Testing

---

![Kali Linux](https://img.shields.io/badge/Kali_Linux-2026-blue?style=for-the-badge&logo=kalilinux&logoColor=white)
![WordPress](https://img.shields.io/badge/WordPress-Security_Audit-21759B?style=for-the-badge&logo=wordpress&logoColor=white)
![WPScan](https://img.shields.io/badge/WPScan-Vulnerability_Scanner-red?style=for-the-badge)
![OWASP](https://img.shields.io/badge/OWASP-Testing_Guide_v4.2-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Estado-Completado-green?style=for-the-badge)

---

## 📋 Descripción del Proyecto

Auditoría de seguridad web completa realizada a un sitio WordPress de un cliente real con autorización expresa. El proyecto siguió las fases estándar de la metodología **OWASP Testing Guide v4.2** desde el reconocimiento inicial hasta la verificación de correcciones.

> ⚠️ **Nota ética:** Este proyecto fue realizado con autorización escrita del propietario del sitio. Todos los datos identificativos del cliente han sido anonimizados para proteger su privacidad y confidencialidad, conforme a las buenas prácticas de la industria de ciberseguridad.

---

## 🎯 Resultados Principales

| Métrica | Antes | Después |
|---------|-------|---------|
| Vulnerabilidades **Críticas** | 🔴 3 | ✅ 0 |
| Vulnerabilidades **Altas** | 🟠 8 | ✅ 0 |
| Vulnerabilidades **Medias** | 🟡 9 | ✅ Reducidas |
| API REST usuarios expuesta | ❌ Sí | ✅ Bloqueada |
| Cabeceras HTTP seguridad | ❌ 3 faltantes | ✅ 5 configuradas |
| Firewall WAF | ❌ No tenía | ✅ Activo |
| Malware detectado | ⚠️ Sin verificar | ✅ Sitio limpio |
| CVEs activos en plugins | ❌ 40+ | ✅ 0 |

---

## 🔧 Herramientas Utilizadas

| Herramienta | Propósito | Fase |
|-------------|-----------|------|
| **Kali Linux** | Sistema operativo de seguridad | Todo el proyecto |
| **Wappalyzer** | Identificación de tecnologías | Reconocimiento |
| **WhatWeb** | Fingerprinting desde terminal | Reconocimiento |
| **WHOIS** | Información del dominio | Reconocimiento |
| **DIG** | Análisis de registros DNS | Reconocimiento |
| **nslookup** | Verificación DNS | Reconocimiento |
| **Nmap** | Escaneo de puertos y servicios | Escaneo |
| **curl** | Análisis de cabeceras HTTP | Escaneo |
| **SSLScan** | Auditoría de certificado TLS | Escaneo |
| **WPScan** | Vulnerabilidades WordPress | Análisis |
| **Wordfence** | Escaneo de malware y WAF | Remediación |
| **Code Snippets** | Implementación de correcciones | Remediación |

---

## 📐 Metodología

```
┌─────────────────────────────────────────────────────────┐
│              OWASP Testing Guide v4.2                   │
├──────────┬──────────┬──────────┬──────────┬────────────┤
│  FASE 1  │  FASE 2  │  FASE 3  │  FASE 4  │   FASE 5  │
│Reconoci- │ Escaneo  │Análisis  │Remedia-  │Verificación│
│ miento   │ Activo   │  Vulns   │  ción    │            │
│ Pasivo   │          │          │          │            │
├──────────┼──────────┼──────────┼──────────┼────────────┤
│Wappalyzer│  Nmap    │ WPScan   │ Snippets │  WPScan   │
│ WhatWeb  │  curl    │ curl API │Wordfence │   curl    │
│  WHOIS   │ SSLScan  │ Headers  │.htaccess │    dig    │
│   DIG    │          │          │  DNS     │           │
└──────────┴──────────┴──────────┴──────────┴────────────┘
```

---

## 🚨 Hallazgos Principales

### 🔴 Críticos (3 encontrados → 0 después)

**1. Exposición de usuario administrador via API REST**
- La API REST de WordPress devolvía nombre de usuario, ID y metadatos del administrador sin autenticación
- Vector de ataque: fuerza bruta dirigida al panel de administración
- Corrección: Filtro PHP que elimina el endpoint `/wp/v2/users`

**2. Subida arbitraria de archivos — CVE-2025-13065**
- Plugin Starter Templates permitía subir archivos PHP maliciosos al servidor
- Vector de ataque: webshell → control total del servidor
- Corrección: Actualización del plugin a versión 4.4.42+

**3. Authentication Bypass — Plugin Elementor Addons**
- Permitía acceso al panel de administración sin contraseña
- Vector de ataque: acceso directo a wp-admin sin credenciales
- Corrección: Actualización del plugin + instalación de Wordfence

### 🟠 Altos (8 encontrados → 0 después)

- Sin registros SPF/DMARC/DKIM → Email Spoofing posible
- Falta `X-Frame-Options` → Clickjacking
- Falta `Strict-Transport-Security` → SSL Stripping
- Tema Astra con 3 CVEs de XSS almacenado
- Plugin Header Footer Elementor con 12 CVEs de XSS
- Plugin WPForms con 15 CVEs incluyendo exposición de datos

---

## ✅ Correcciones Implementadas

```
1. ✅ API REST de usuarios bloqueada via Code Snippets PHP
2. ✅ 40+ vulnerabilidades corregidas actualizando plugins y temas
3. ✅ Archivos readme.html y licencia.txt eliminados del servidor
4. ✅ Cabeceras HTTP configuradas en .htaccess:
       - X-Frame-Options: SAMEORIGIN
       - X-Content-Type-Options: nosniff
       - Strict-Transport-Security: max-age=31536000
       - Referrer-Policy: strict-origin-when-cross-origin
       - Permissions-Policy configurado
5. ✅ Versiones PHP y WordPress ocultadas del código público
6. ✅ Registro SPF configurado en DNS para protección de correo
7. ✅ Wordfence Security instalado:
       - Firewall WAF activo
       - Límite de intentos de login: 3
       - Bloqueo automático: 30 minutos
       - Escaneo de malware: 23,244 archivos — LIMPIO
8. ✅ Generator tags de versiones eliminados del HTML
9. ✅ Autor ocultado en feed RSS
```

---

## 📁 Estructura del Repositorio

```
📁 auditoria-seguridad-web/
│
├── 📄 README.md
│
├── 📁 reportes/
│   ├── Reporte1_Vulnerabilidades_Auditoria_Web.pdf
│   └── Reporte2_Correcciones_Verificacion.pdf
│
├── 📁 evidencias/
│   ├── 📁 F1_reconocimiento/
│   │   ├── wappalyzer_tecnologias.png
│   │   ├── whatweb_resultado.png
│   │   ├── whois_dominio.png
│   │   ├── dig_registros_dns.png
│   │   └── nslookup_ips.png
│   │
│   ├── 📁 F2_escaneo/
│   │   ├── nmap_puertos.png
│   │   ├── curl_cabeceras_http.png
│   │   └── sslscan_certificado.png
│   │
│   ├── 📁 F3_vulnerabilidades/
│   │   ├── wpscan_plugins_vulnerables.png
│   │   ├── api_rest_usuarios_expuesta.png
│   │   └── archivos_sensibles_expuestos.png
│   │
│   └── 📁 F4_verificacion/
│       ├── api_rest_bloqueada.png
│       ├── cabeceras_http_corregidas.png
│       ├── wordfence_escaneo_limpio.png
│       └── wpscan_post_correcciones.png
│
└── 📁 recursos/
    └── checklist_seguridad_wordpress.md
```

---

## 📊 Tecnologías del Sitio Auditado

- **CMS:** WordPress 6.9.4
- **Constructor:** Elementor 4.0.0
- **Tema:** Astra 4.12.6
- **Lenguaje:** PHP 8.3.30
- **Base de datos:** MySQL
- **Hosting:** CDN con Nginx reverse proxy
- **Certificado:** TLS 1.2/1.3 — RSA 4096 bits

---

## 🎓 Aprendizajes del Proyecto

- Aplicación práctica de la metodología OWASP en un entorno real
- Uso profesional de herramientas de seguridad en Kali Linux
- Análisis e interpretación de vulnerabilidades CVE
- Redacción de reportes de seguridad profesionales con evidencias
- Implementación de correcciones de seguridad en WordPress
- Configuración de cabeceras HTTP y registros DNS de seguridad
- Ciclo completo: reconocimiento → análisis → remediación → verificación

---

## 👨‍💻 Autor

**David**
Estudiante de Ciberseguridad | Querétaro, México

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Conectar-blue?style=flat&logo=linkedin)](https://linkedin.com/in/tu-perfil)

---

## ⚖️ Aviso Legal

Este proyecto fue realizado con **autorización expresa y escrita** del propietario del sitio web auditado. Toda la información sensible del cliente ha sido anonimizada. Este repositorio tiene fines exclusivamente educativos y de portafolio profesional.

**Realizar pruebas de seguridad sin autorización es ilegal. Siempre obtén permiso por escrito antes de auditar cualquier sistema.**

---

*Proyecto completado: Abril 2026 | Metodología: OWASP Testing Guide v4.2*
