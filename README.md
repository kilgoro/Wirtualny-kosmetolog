# Wirtualny Kosmetolog 💆‍♀️

Wtyczka WordPress – interaktywny quiz kosmetologiczny z rekomendacjami zabiegów. Idealna dla gabinetów kosmetycznych i studiów urody.

## Funkcje

- **Quiz 5-krokowy** – prowadzi klientkę przez wybór partii ciała, problemów i stosowanych metod
- **Panel admina** z 4 zakładkami: Ścieżki, Powitanie, Zdjęcia, Ustawienia
- **Automatyczne dopasowanie zdjęć** do zabiegów (po nazwie pliku lub ręcznie)
- **Import zdjęć** z katalogu `/treatments/` do biblioteki mediów przy aktywacji
- **Konfigurowalne kolory** – paleta główna, akcent, gradient, kolor przycisku formularza
- **Integracja z CF7 / Elementor** – formularz konsultacji na końcu quizu
- **Slider Splide** na ekranie wyników
- **ARIA + role** – dostępność (a11y) wbudowana w HTML
- **Bezpieczeństwo** – nonce CSRF na wszystkich formularzach admina, pełna sanityzacja danych

## Wymagania

- WordPress 5.8+
- PHP 7.4+
- *(Opcjonalnie)* Contact Form 7 lub dowolny shortcode formularza

## Instalacja

1. Pobierz repozytorium lub paczkę ZIP.
2. Wgraj folder `wirtualny-kosmetolog` do `/wp-content/plugins/`.
3. Aktywuj wtyczkę w panelu WordPress → **Wtyczki**.
4. Zdjęcia z katalogu `/treatments/` zostaną automatycznie zaimportowane do biblioteki mediów.
5. Wejdź w menu **Wirtualny Kosmetolog** i skonfiguruj ścieżki, kolory oraz formularz.
6. Umieść shortcode na wybranej stronie:

```
[virtual_beautician_quiz]
```

## Konfiguracja

### Ścieżki (zakładka „Ścieżki")

Definiujesz drzewo: **Część ciała → Problemy → Zabiegi**.  
Każdy problem może mieć przypisanych wiele zabiegów (multi-select z Select2).

### Zdjęcia (zakładka „Zdjęcia")

- **Automatyczne** – system dopasowuje zdjęcia do zabiegów po nazwie pliku (obsługa wariantów fleksyjnych, np. `cialo` / `ciala`).
- **Ręczne** – bezpośrednie przypisanie zdjęcia do konkretnego zabiegu.

### Ustawienia (zakładka „Ustawienia")

| Opcja | Opis |
|---|---|
| Źródło zabiegów | Post type (domyślnie `page`) |
| Rodzic kategorii | Filtrowanie podstron po rodzicu |
| Shortcode formularza | CF7, Elementor itp. |
| Pole podsumowania | Nazwa pola w formularzu na podsumowanie quizu |
| Kolory | Główny, gradient, akcent, przycisk formularza |
| Metody (krok 4) | Konfigurowalna lista – jedna linia = jedna opcja |

### Frazy filtrowania rodziców

Wpisz słowa kluczowe (każde w nowej linii) aby zawęzić listę stron nadrzędnych w ustawieniach. Zostaw puste, żeby widzieć wszystkie.

## Shortcode

```php
[virtual_beautician_quiz]
```

Nie przyjmuje atrybutów – całość konfigurowana z panelu admina.

## Struktura plików

```
wirtualny-kosmetolog/
├── virtual-beautician.php        # Główny plik wtyczki
├── inc/
│   ├── admin-panel.php           # Panel admina (4 zakładki)
│   └── shortcodes.php            # Logika quizu + helper do jasności kolorów
├── assets/
│   ├── css/
│   │   └── frontend-quiz.css     # Style quizu (CSS custom properties)
│   └── js/
│       ├── frontend-quiz.js      # Logika quizu (vanilla JS + jQuery)
│       └── admin-settings.js     # JS panelu admina (color picker, media)
└── treatments/                   # Zdjęcia zabiegów (importowane przy aktywacji)
    ├── hifu.webp
    ├── kriolipoliza.webp
    └── ...
```

## Zewnętrzne zależności (CDN)

| Biblioteka | Wersja | Użycie |
|---|---|---|
| [Splide](https://splidejs.com/) | 4.1.4 | Slider rekomendacji |
| [Select2](https://select2.org/) | 4.1.0-rc.0 | Multi-select w panelu admina |

Obie ładowane tylko tam, gdzie są potrzebne (warunkowe `wp_enqueue`).

## Bezpieczeństwo

- Każdy formularz admina zabezpieczony nonce (`wp_nonce_field` / `check_admin_referer`)
- Dane wejściowe sanityzowane przez `sanitize_text_field`, `wp_kses_post`, `intval`, `sanitize_hex_color`
- AJAX handler chroniony przez `check_ajax_referer` i sprawdzenie `current_user_can('manage_options')`
- Skrypty i style ładowane tylko na stronach ze shortcodem

## Autor

**Patryk Łyjak**

## Licencja

Copyright © 2024 Patryk Łyjak. Wszelkie prawa zastrzeżone.

Kod źródłowy jest widoczny, ale **nie jest oprogramowaniem open source**. Przeglądanie kodu nie nadaje żadnych praw do jego używania, kopiowania, modyfikowania ani dystrybucji bez pisemnej zgody autora.

The user just wants the README text translated to English — they're not asking for a file. The document already contains an English version at the bottom. I'll provide a clean, complete English-only README.
Here's the full README rewritten in English:

Virtual Beautician 💆‍♀️
A WordPress plugin — an interactive cosmetology quiz with personalized treatment recommendations. Perfect for beauty salons, aesthetic clinics, and skincare studios.
Features

5-Step Quiz – guides the client through body part selection, specific concerns, and preferred treatment methods
4-Tab Admin Panel – manage Paths, Welcome Screen, Photos, and Settings
Automatic Photo Matching – matches images to treatments by filename (supports inflectional variants) or via manual override
Media Library Auto-Import – automatically imports images from the /treatments/ directory upon plugin activation
Customizable Colors – set primary color, accent, gradient, and form button styles to match your brand
CF7 / Elementor Integration – embed a consultation form at the end of the quiz
Splide Slider – a smooth, responsive carousel on the results screen
Accessibility (a11y) – built-in ARIA labels and roles for screen-reader compatibility
Security First – CSRF nonces on all admin forms and full input sanitization

Requirements

WordPress 5.8+
PHP 7.4+
(Optional) Contact Form 7 or any shortcode-based form builder

Installation

Download the repository or ZIP package.
Upload the virtual-beautician folder to /wp-content/plugins/.
Activate the plugin in WordPress Dashboard → Plugins.
Images from the /treatments/ folder will be automatically imported into your Media Library.
Navigate to the Virtual Beautician menu and configure your paths, colors, and form settings.
Place the shortcode on any page:

[virtual_beautician_quiz]
Configuration
Paths (Tab: "Paths")
Define your logic tree: Body Part → Concerns → Treatments.
Each concern can be linked to multiple treatments using a Select2 multi-select field.
Photos (Tab: "Photos")

Automatic – the system matches images to treatments based on the filename (handles linguistic variants, e.g. body / bodies).
Manual – directly assign a specific Media Library image to a treatment.

Settings (Tab: "Settings")
OptionDescriptionTreatment SourcePost type to pull from (default: page)Parent CategoryFilter sub-pages by a specific parent pageForm ShortcodePaste your CF7, Elementor, or WPForms shortcode hereSummary FieldThe field name/ID where quiz results should be injectedColorsPrimary, gradient, accent, and button stylingMethods (Step 4)Configurable list – one line per option
Parent Filter Keywords
Enter keywords (one per line) to narrow the list of parent pages shown in settings. Leave blank to show all.
Shortcode
php[virtual_beautician_quiz]
```

No attributes — everything is configured from the admin panel.

## File Structure
```
virtual-beautician/
├── virtual-beautician.php        # Main plugin file
├── inc/
│   ├── admin-panel.php           # Admin UI (4 tabs)
│   └── shortcodes.php            # Quiz logic + color brightness helpers
├── assets/
│   ├── css/
│   │   └── frontend-quiz.css     # Quiz styling (CSS custom properties)
│   └── js/
│       ├── frontend-quiz.js      # Quiz logic (Vanilla JS + jQuery)
│       └── admin-settings.js     # Admin JS (color picker, media library)
└── treatments/                   # Treatment images (imported on activation)
    ├── hifu.webp
    ├── cryolipolysis.webp
    └── ...
External Dependencies (CDN)
LibraryVersionUsageSplide4.1.4Recommendation sliderSelect24.1.0-rc.0Multi-select in the admin panel
Both are enqueued conditionally — only on pages where they're needed.
Security

Every admin form is protected by nonces (wp_nonce_field / check_admin_referer)
Input data is sanitized via sanitize_text_field, wp_kses_post, intval, and sanitize_hex_color
AJAX handlers are protected by check_ajax_referer and current_user_can('manage_options') capability checks
Scripts and styles are loaded only on pages containing the shortcode

Author
Patryk Łyjak
License
Copyright © 2024 Patryk Łyjak. All rights reserved.
The source code is visible for inspection but is not open-source software. Viewing the code does not grant any rights to use, copy, modify, or distribute it without the express written consent of the author.
