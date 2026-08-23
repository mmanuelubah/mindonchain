# PDF Vault — Canonical Data Schema (Merged v2)

> **This file is the handshake between the infrastructure agent (Opus) and the content-extraction pipeline agent (Gemini).** Both agents build against this contract. If either needs to change it, stop and flag to Emmanuel — do not silently modify.

## Schema

```json
{
  "source_document": {
    "doc_id": "string (slug)",
    "filename": "string",
    "category": "locksmithing | ecu_programming | ecu_pinout",
    "title": "string",
    "car_brand": "string",
    "car_model": "string",
    "ecu_number": "string (as labeled on/for the ECU module)",
    "storage": {
      "drive_file_id": "string"
    }
  },
  "ecu_family": {
    "ecu_id": "string (slug)",
    "ecu_manufacturer": "string (e.g. Bosch, Denso, Continental)",
    "ecu_model": "string (e.g. ME7.9.7)",
    "ecu_number": "string",
    "family_group": "string",
    "car_brand": "string",
    "car_model": "string",
    "year_start": "int",
    "year_end": "int",
    "vehicle_compatibility": [
      { "make": "string", "model": "string", "year_start": "int", "year_end": "int" }
    ],
    "pinout_images": [
      { "image_id": "string", "drive_file_id": "string", "source_doc_id": "string", "page_number": "int", "verified": "boolean" }
    ],
    "source_doc_id": "string",
    "verified": "boolean",
    "review_flag": "none | needs_review",
    "review_reason": "string|null"
  },
  "key_programming_record": {
    "record_id": "string",
    "car_brand": "string",
    "car_model": "string",
    "year": "int or range",
    "ecu_id": "string (fk -> ecu_family.ecu_id)",
    "method": "obd | bench",
    "obd_steps": ["string"],
    "bench_required_tool": "string|null",
    "bench_steps": ["string"],
    "safety_notes": ["string"],
    "source_doc_id": "string",
    "source_page": "int",
    "verified": "boolean",
    "review_flag": "none | needs_review",
    "review_reason": "string|null"
  }
}
```

## Enforcement Rules

- **Never render** any record where `verified` is `false` or `review_flag` is `needs_review` — not in the public catalog, not via a direct/guessed URL.
- This is how the content pipeline's human-review requirement gets enforced at the infrastructure level.

## Storage

- **Google Drive** holds the originals (private, never linked publicly).
- Documents are embedded via Google Drive preview iframe: `https://drive.google.com/file/d/{drive_file_id}/preview`
- In Drive sharing settings: set to "Anyone with the link" → "Viewer", and uncheck "Viewers and commenters can see the option to download, print, and copy".
