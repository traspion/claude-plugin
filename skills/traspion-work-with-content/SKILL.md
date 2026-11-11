---
name: traspion-work-with-content
description: Find, retrieve, translate, edit, save, rename, or export an existing Traspion speech-to-text transcript. Use when the user wants to work with audio-to-text or video-to-text content already stored in Traspion.
---

# Work with Traspion content

The Traspion tools were first written for ChatGPT. Where a tool description or result mentions ChatGPT, read it as you, Claude. ChatGPT Canvas does not exist here: show text in the conversation.

## Find the file

- Reuse a `fileId` already returned for the file the user clearly means.
- Otherwise call `list_files`, using its filename, date, or status filters when the user gave those details. If several files could match, ask the user to choose; don't guess an ID. A request for the latest file may use the most recent matching result.
- Show files from `list_files` as a Markdown table with row number, filename, upload time, and status, in the returned order. Use the row number to resolve a follow-up choice. Don't show internal IDs or a pagination cursor unless the next page needs it.
- Call `get_transcription` for every request to see a transcript, including when the user switches to another file later.

## Read and translate

- Use the returned pagination flags and next offsets when more of the transcript is needed. Stop when the task has enough content or the whole requested transcript is retrieved.
- Mark partial results clearly. Never call a truncated transcript complete. If a complete transcript is too long to show, say it is partial and offer `export_transcript`.
- Follow the returned `presentationMode`. When both speaker and channel identification are on, show each segment once, for example `[00:00–00:08] Channel 1 · Speaker A: text`. Keep the returned labels and timestamps, drop a label only when it is missing, and don't repeat the content as plain text unless asked.
- For a translation, call `get_translation` first, because Traspion may have stored one during transcription. If it is still processing, report that and stop.
- If `get_translation` returns `TRANSLATION_NOT_REQUESTED`, tell the user: "You didn't opt for translation while transcribing, so I'll translate the transcription myself." Retrieve the complete transcription and translate it into the requested language.
- Present that translation under **Transcript translation**. Translate faithfully, keeping meaning, paragraphs, speaker labels and timestamps. Don't summarize, polish, or add commentary, and don't claim Traspion made or stored it.
- Never save a translation you produced to Traspion, even if asked. Tell the user to copy it if they want to keep it.
- For a stored translation, follow `nextTextOffset` until the text is complete. Use `export_transcript` when a complete stored file is too large to show.

## Edit and save

- Retrieve the current stored content and its revision before editing. Edits stay in the conversation until the user explicitly approves saving the complete revised content to Traspion.
- Show the proposed content, and call `save_content` only after the user approves saving it. Pass the revision returned by `get_transcription` or `get_translation`. If the content changed since it was read, ask the user to reopen and review it instead of overwriting.
- Keep the resolved `fileId` and pick the content type that matches what is being saved.
- Never overwrite stored content with a partial or paginated fragment.
- Call `save_content` once. If it fails, report the error; don't claim the edit was saved.

## Rename and export

- Use `rename_file` only when the file and the new name are clear.
- For export, settle the format (`pdf`, `txt`, `docx`, or `json`) and whether the user wants the transcription, stored translation, speaker-labelled transcript, or channel-identified transcript. Ask when either is unclear.
- Use `type: speaker-labelling` only when the file was transcribed with speaker labels, and `type: channel-identification` only when channel identification was on. If the requested output wasn't enabled, say it's unavailable instead of exporting something else.
- Copy the exact Markdown download link returned by `export_transcript` and say that the link is temporary. Never rewrite, shorten, or omit it.

## Limits

- Deleting files (other than a file waiting for minutes, after the user confirms) and billing changes are only on the Traspion website.
