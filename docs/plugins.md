# rEos Plugins

Plugins extend rEos without modifying the Kernel or Core.

## Rules

1. API-only interaction.
2. Own schema namespace (`plugin_id.*`).
3. Declare permissions in `manifest.json`.
4. Signed in production.
5. No direct writes to core tables.

## manifest.json

```json
{
  "identity": "reos.pharmacy",
  "version": "1.2.0",
  "dependencies": ["reos.core>=3.0 <4.0"],
  "permissions": ["pharmacy.dispense", "inventory.read"],
  "objects": ["PharmacyBatch"],
  "migrations": ["001_init.sql"],
  "commands": ["pharmacy.dispense"],
  "queries": ["pharmacy.stock_expiring"],
  "events": ["pharmacy.batch.expiring"],
  "ui": ["PharmacyWorkspace"],
  "translations": ["en", "ne"],
  "ai_tools": ["pharmacy.check_stock"],
  "tests": ["pharmacy_e2e"]
}
