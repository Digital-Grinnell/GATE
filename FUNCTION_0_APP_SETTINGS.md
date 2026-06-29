# Function 0: App Settings

## Purpose
Open the application settings file in the selected working/output directory and edit values using popup text input fields.
This includes selecting and persisting the GCCB CollectionBuilder deployment URL used for ingest preparation.

## Security Note
**Sensitive fields are encrypted** (`api_key`, `api_secret`, `password`). You enter and see them as plain text in the editor, but they are automatically encrypted when saved to `gate_settings.json`. This makes it safe to commit your settings file to version control (GitHub, etc.) without exposing credentials.

The encryption key is stored separately in `~/.GATE-data/encryption_key` with restricted permissions.

## Current Settings
- **auto_save_enabled**: When `true`, enables automatic saving of output from functions. **[BOOLEAN]**
- **auto_save_format**: Default output format for autosave files (e.g., `txt`, `csv`, `json`, etc.)
- **api_key**: Your API key for external services. **[ENCRYPTED]**
- **api_secret**: Your API secret for external services. **[ENCRYPTED]**
- **password**: General password field for application use. **[ENCRYPTED]**
- **gccb_deployment_url**: HTTPS URL for the selected GCCB CollectionBuilder deployment

## Requirements
- A **Working/Output Directory** must be selected first.

## Usage
1. Set **Working/Output Directory**.
2. Select **0: App Settings** from the function list.
3. Edit values in the text input fields.
4. Enter or update **gccb_deployment_url**.
5. Click **Save**.

## URL Validation
- `gccb_deployment_url` must be a valid URL with:
  - `https://` scheme
  - A host value (for example `*.azurestaticapps.net`)
- Invalid URLs are rejected with an error message.

## Settings File
- File name: `gate_settings.json`
- Location: Inside the selected working/output directory

## Accepted Boolean Values
For `auto_save_enabled`, you can enter:
- true/false
- yes/no
- 1/0
- on/off

## Notes
- Settings are specific to each working/output directory
- The settings file is created automatically with defaults if it doesn't exist
- Sensitive fields (marked **[ENCRYPTED]**) are stored encrypted in the JSON file
- The deployment URL can also be managed from the main **CollectionBuilder Deployment** section in the app UI
- You can customize the sensitive fields list and default settings in `app.py`

## Example Settings File (stored encrypted)
```json
{
  "auto_save_enabled": false,
  "auto_save_format": "txt",
  "api_key": "gAAAAABk...[encrypted]",
  "api_secret": "gAAAAABk...[encrypted]",
  "password": "gAAAAABk...[encrypted]",
  "gccb_deployment_url": "https://black-sky-0a5891010.7.azurestaticapps.net/"
}
```

## Customization
To add your own settings:
1. Edit `DEFAULT_APP_SETTINGS` in `app.py`
2. Add new fields to the Function 0 dialog
3. Mark sensitive fields in `SENSITIVE_FIELDS` list for encryption
4. Update this documentation
