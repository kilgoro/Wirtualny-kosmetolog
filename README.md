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
