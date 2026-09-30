# Qnox PII Shield Privacy Policy

Effective date: September 12, 2026

Qnox PII Shield helps users mask personal or sensitive information locally before handing a prompt to an AI chat site.

## Summary

- Qnox does not operate a server or analytics service.
- Qnox does not sell, rent, or share user data.
- Detection, masking, preview, and token resolution run inside the browser.
- Qnox does not load remote executable code.
- Qnox requests access only to the AI chat hosts listed in its manifest.

## Data processed

Qnox may process the following information locally:

- Text entered in the popup redactor, inline/full masking editors, or token resolver.
- Text in a focused supported-site composer, analyzed locally to show a sensitive-data indicator. This check does not save originals or change the site's draft.
- A copy of a native AI-site draft after the user explicitly opens a Qnox editor or turns on Open quick masking automatically.
- User-entered prompt-level and universal custom mask terms.
- Newly rendered AI response text when the optional sensitive-response warning is enabled.
- Qnox tokens in sent messages and replies when restoring a conversation, plus its URL identity and display preference.
- Attachment names and extensions when the optional attachment warning is enabled.
- Local settings and supported-site status needed to operate the extension.

Qnox does not read attachment contents. Unless a user turns on Open quick masking automatically, it does not intercept native paste, drop, Enter, or send-button actions. Qnox never clicks the site's Send control. Text typed directly into an AI site's composer is processed by that site under its own privacy policy.

## Storage

Qnox encrypts persistent preferences before saving them in `chrome.storage.local`, including composer modes, enabled detector categories, universal custom masks, display preferences, Remember originals mode, and optional warning settings.

Prompt-level custom terms are transient and are not persisted as settings. Qnox does not intentionally store complete prompt bodies. Qnox does not use `chrome.storage.sync`.

Remember originals is enabled by default. Users can disable it, which clears saved originals and prevents new mappings from being stored. While it is enabled, Qnox saves token-to-original mappings, conversation identifiers, and each conversation's Restore text / Show tokens choice in `chrome.storage.local`. This lets the same conversation be restored after a reload, tab closure, or browser restart. Local storage access is restricted to trusted extension contexts before original mappings are read or written. Qnox encrypts these records with AES-256-GCM before writing them to disk-backed extension storage. Conversation identifiers, display choices, saved originals, pending draft mappings, and persistent upgrade backups are covered. Each encryption uses a fresh random initialization value and authenticates the storage record type. A randomly generated, non-extractable Web Crypto key is retained in the extension's IndexedDB database so records remain readable after a browser restart. The key is local to the browser profile and is not protected by a user password. Someone controlling that profile, the running browser, or the device may still access the key through the browser or read decrypted values in use.

Saved originals are limited to 100 conversations, 200 mappings per conversation, and a 4 MiB decoded-record budget; encrypted encoding adds storage overhead. Conversations unused for 30 days are removed on the next storage operation. Capacity limits may remove older records sooner. Turning Remember originals off clears saved originals and prevents new mappings from being stored. Delete saved originals also removes saved mappings and display choices. Numeric token counters remain so old placeholders are not assigned to new values.

Existing plaintext records from earlier versions are migrated to encrypted records when the background worker starts or the records are next accessed. Qnox does not fall back to plaintext writes if encryption fails. Damaged ciphertext or a missing key produces a storage error rather than silently replacing retained data. Delete saved originals can remove inaccessible original-mapping records. Migration and deletion update the current extension storage; they do not guarantee erasure of previous disk remnants or external backups.

Temporary tab bookkeeping and unclaimed session-only legacy mappings use `chrome.storage.session`, which is memory-backed for the browser session. New draft mappings that have not yet been associated with a saved conversation remain in the bounded local vault across tab closure, extension reload, and browser restart. They share the same 30-inactive-day expiry and storage limits as saved conversations, and are associated when their matching tokens first appear in a supported conversation. Older session-only mappings retain their original 24-hour expiry and are cleared when their original tab closes. A local upgrade backup, when present, is restricted to trusted extension contexts, keeps that original expiry, and is consumed only when matching tokens are associated with the same origin and original tab.

Restore text changes actual text nodes in ordinary messages. For supported writing drafts, it displays a selectable, read-only HTML version beside the hidden original editor so the provider's editor model keeps its protected tokens. The site's scripts can read these original values, and the remembered choice reapplies them when the conversation is reopened. Show tokens reverses Qnox's displayed replacements. Restoring text does not submit a message or dispatch an edit to the provider's editor, but Qnox cannot prevent the site from collecting or transmitting restored page text.

Universal custom masks are stored locally until the user removes them or resets settings. Users should avoid saving a universal mask phrase that they would not want retained as a local preference.

## Clipboard

The popup redactor writes masked text to the clipboard only after a user action. Token resolution can write resolved text to the clipboard only after a user action. Clipboard content is not sent to Qnox.

## Network

Qnox does not make outbound requests for detection, masking, resolving, settings, or diagnostics.

AI chat sites and other pages visited by the user make their own network requests. Those requests are outside Qnox's control. Site scripts can read text inserted into the native composer immediately and can read originals restored in a conversation. Qnox leaves the site's Send action to the user.

## Permissions

- `storage`: saves local settings and, when enabled, bounded conversation-scoped mappings and display choices.
- Targeted supported-site access: injects Qnox launch controls, inline/full masking editors, conversation restoration, and optional local warnings on the AI chat hosts listed in the manifest.

Qnox does not request `<all_urls>`, remote-code permissions, or `chrome.storage.sync`.

## User controls

Users can:

- Review and ignore individual detections.
- Enable or disable Quick masking button, Extra editor launcher, and Open quick masking automatically.
- Enable or disable detector categories.
- Add or remove prompt-level and universal custom masks.
- Hide detected values in Qnox review chips.
- Enable or disable readable token labels.
- Enable or disable Remember originals and toggle Restore text / Show tokens in a conversation.
- Enable or disable attachment and response warnings.
- Delete all saved originals or clear the popup workspace's originals.
- Disable Qnox's in-page UI while continuing to use the popup redactor.

Disabled detector categories can leave matching values unmasked. Qnox shows sanitized counts and requires acknowledgement before that handoff. Values manually ignored by the user also remain unmasked.

## Limitations

Qnox uses local patterns and heuristics and can produce false positives or false negatives. Users remain responsible for reviewing every masked or original handoff.

Qnox cannot hide text already typed into an AI site's native composer, prevent native site sends, control another extension, or guarantee compatibility after a supported site changes its interface.

## Limited Use

Qnox's use and transfer of user data follows the Chrome Web Store Limited Use requirements. Data is used only for the disclosed review, masking, warning, and restoration features. It is not sold, used for advertising, or used to determine creditworthiness or lending eligibility. The publisher does not receive prompt text or saved original mappings.

## Policy updates

Review this policy before each release and whenever permissions, storage behavior, supported hosts, network behavior, or user-visible data handling changes.
