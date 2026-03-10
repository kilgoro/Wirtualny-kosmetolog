# Virtual Beautician 💆‍♀️

A WordPress plugin — an interactive cosmetology quiz with personalized treatment recommendations. Perfect for beauty salons, aesthetic clinics, and skincare studios.

---

## Features

- **5-Step Quiz** – guides the client through body part selection, specific concerns, and preferred treatment methods
- **4-Tab Admin Panel** – manage Paths, Welcome Screen, Photos, and Settings
- **Automatic Photo Matching** – matches images to treatments by filename (supports inflectional variants) or via manual override
- **Media Library Auto-Import** – automatically imports images from the `/treatments/` directory upon plugin activation
- **Customizable Colors** – set primary color, accent, gradient, and form button styles to match your brand
- **CF7 / Elementor Integration** – embed a consultation form at the end of the quiz
- **Splide Slider** – a smooth, responsive carousel on the results screen
- **Accessibility (a11y)** – built-in ARIA labels and roles for screen-reader compatibility
- **Security First** – CSRF nonces on all admin forms and full input sanitization

---

## Requirements

- WordPress 5.8+
- PHP 7.4+
- *(Optional)* Contact Form 7 or any shortcode-based form builder

---

## Installation

1. Download the repository or ZIP package.
2. Upload the `virtual-beautician` folder to `/wp-content/plugins/`.
3. Activate the plugin in WordPress Dashboard → **Plugins**.
4. Images from the `/treatments/` folder will be automatically imported into your Media Library.
5. Navigate to the **Virtual Beautician** menu and configure your paths, colors, and form settings.
6. Place the shortcode on any page:

```
[virtual_beautician_quiz]
```

---

## Configuration

### Paths (Tab: "Paths")

Define your logic tree: **Body Part → Concerns → Treatments**.  
Each concern can be linked to multiple treatments using a Select2 multi-select field.

### Photos (Tab: "Photos")

- **Automatic** – the system matches images to treatments based on the filename (handles linguistic variants, e.g. `body` / `bodies`).
- **Manual** – directly assign a specific Media Library image to a treatment.

### Settings (Tab: "Settings")

| Option | Description |
|---|---|
| Treatment Source | Post type to pull from (default: `page`) |
| Parent Category | Filter sub-pages by a specific parent page |
| Form Shortcode | Paste your CF7, Elementor, or WPForms shortcode here |
| Summary Field | The field name/ID where quiz results should be injected |
| Colors | Primary, gradient, accent, and button styling |
| Methods (Step 4) | Configurable list – one line per option |

### Parent Filter Keywords

Enter keywords (one per line) to narrow the list of parent pages shown in settings. Leave blank to show all.

---

## Shortcode

```php
[virtual_beautician_quiz]
```

No attributes — everything is configured from the admin panel.

---

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
```

---

## External Dependencies (CDN)

| Library | Version | Usage |
|---|---|---|
| [Splide](https://splidejs.com/) | 4.1.4 | Recommendation slider |
| [Select2](https://select2.org/) | 4.1.0-rc.0 | Multi-select in the admin panel |

Both are enqueued conditionally — only on pages where they're needed.

---

## Security

- Every admin form is protected by nonces (`wp_nonce_field` / `check_admin_referer`)
- Input data is sanitized via `sanitize_text_field`, `wp_kses_post`, `intval`, and `sanitize_hex_color`
- AJAX handlers are protected by `check_ajax_referer` and `current_user_can('manage_options')` capability checks
- Scripts and styles are loaded only on pages containing the shortcode

---

## Author

**Patryk Łyjak**

---

## License

Copyright © 2024 Patryk Łyjak. All rights reserved.

The source code is visible for inspection but is **not open-source software**. Viewing the code does not grant any rights to use, copy, modify, or distribute it without the express written consent of the author.
