
# AnkiConnect [Custom Build for Kardenwort]

[![Build](https://img.shields.io/badge/build-custom-blue)](https://github.com/voothi/20251110002755-anki-ankiconnect)  [![License: GPL v3](https://img.shields.io/badge/License-GPL_v3-yellow.svg)](https://www.gnu.org/licenses/gpl-3.0)

This is a custom build of the official **AnkiConnect** add-on, extended with a new API action to enable deeper integration with external tools, specifically the **[Kardenwort](https://github.com/kardenwort/20250913122858-kardenwort)** language learning ecosystem.

The primary purpose of this fork is to add a single, powerful feature: the ability for an application to programmatically set or update the description field for any Anki deck. While all original AnkiConnect functionality remains intact, this build is essential for unlocking the full potential of Kardenwort's deck management features.

## Table of Contents
- [AnkiConnect \[Custom Build for Kardenwort\]](#ankiconnect-custom-build-for-kardenwort)
  - [Table of Contents](#table-of-contents)
  - [The Core Enhancement: Programmatic Deck Descriptions](#the-core-enhancement-programmatic-deck-descriptions)
    - [New API Action: `setDeckDescription`](#new-api-action-setdeckdescription)
  - [Purpose \& Integration with Kardenwort](#purpose--integration-with-kardenwort)
  - [Installation](#installation)
  - [Important Notes \& Disclaimer](#important-notes--disclaimer)
  - [Kardenwort Ecosystem](#kardenwort-ecosystem)
  - [License and Acknowledgements](#license-and-acknowledgements)

---

## The Core Enhancement: Programmatic Deck Descriptions

This build introduces one new API action to the standard AnkiConnect feature set, detailed below.

| Action | Description | Parameters |
| :--- | :--- | :--- |
| `setDeckDescription` | Sets or updates the description text for a specified Anki deck. | `deck` (string), `description` (string) |

### New API Action: `setDeckDescription`

This action allows an external client to set the description for a given deck. The description content supports standard text and Markdown formatting, just like Anki's native editor. If the specified deck does not exist, the action will return an error.

**Request:**

```json
{
    "action": "setDeckDescription",
    "version": 6,
    "params": {
        "deck": "My Awesome Deck::Chapter 1",
        "description": "This is the full text of Chapter 1, which provides context for all the cards within this subdeck."
    }
}
```

**Parameters:**

*   `deck` (string, required): The full, case-sensitive name of the target deck, including any parent decks separated by `::`.
*   `description` (string, required): The text content to set as the deck's description.

**Successful Response:**

```json
{
    "result": true,
    "error": null
}
```

**Error Response (e.g., if the deck does not exist):**

```json
{
    "result": null,
    "error": "deck was not found: My Awesome Deck::Non-Existent Chapter"
}
```

[Return to Top](#table-of-contents)

## Purpose & Integration with Kardenwort

This custom build was created specifically to enable the `--anki-deck-content` feature in the **Kardenwort** project.

When you use Kardenwort to generate Anki cards, it can also create a companion `.json` file containing the full source text or translations. The `kardenwort-anki-csv-importer` script then reads this file and uses the `setDeckDescription` action provided by this add-on to automatically populate the description fields of the relevant Anki decks.

This creates a seamless workflow where your Anki decks are not just containers for cards but also hold the complete contextual information from which those cards were derived.

[Return to Top](#table-of-contents)

## Installation

To use this feature, you must replace your existing AnkiConnect add-on with this version.

1.  **Open Anki** on your desktop.
2.  Navigate to **Tools > Add-ons**.
3.  In the add-on list, find your existing **AnkiConnect** installation (its add-on code is `2055492159`).
4.  Select it and click the **"View Files"** button on the right side of the window. This will open your Anki add-ons folder.
5.  Locate the folder named `2055492159`.
6.  **Important**: **Delete** this folder or rename it (e.g., to `2055492159.bak`) to disable the official version.
7.  Clone or download this repository into your add-ons folder, ensuring the final folder name is correct. The easiest way is to use Git from your terminal:
    ```bash
    # Navigate to your Anki add-ons folder first
    cd /path/to/your/Anki2/addons21

    # Clone the repository and name the folder correctly
    git clone https://github.com/voothi/20251110002755-anki-ankiconnect.git 2055492159
    ```
8.  **Restart Anki**.

The new `setDeckDescription` action will now be available to any client application.

[Return to Top](#table-of-contents)

## Important Notes & Disclaimer

⚠️ **This is not the official AnkiConnect add-on.** It is a feature-specific fork maintained to support the Kardenwort ecosystem.

*   **No Automatic Updates:** This build will not receive automatic updates from the official AnkiConnect repository.
*   **Manual Merging:** To incorporate future updates and bug fixes from the official project, you will need to manually merge them into this fork.
*   **Intended Use:** This build is recommended only for users who need the `setDeckDescription` functionality. For all other purposes, the official AnkiConnect add-on is sufficient.

[Return to Top](#table-of-contents)

## Kardenwort Ecosystem

This project is part of the **[Kardenwort](https://github.com/kardenwort)** environment, designed to create a focused and efficient learning ecosystem.

[Return to Top](#table-of-contents)

## License and Acknowledgements

This project is a fork of the official [AnkiConnect](https://github.com/FooSoft/anki-connect) add-on and is therefore licensed under the **GNU General Public License v3.0**.

The `setDeckDescription` modification was created by **Denis Novikov (voothi)**.

All credit for the original AnkiConnect add-on, its architecture, and its extensive feature set goes to its original author, **Alex Yatskov**, and its contributors.

[Return to Top](#table-of-contents)
