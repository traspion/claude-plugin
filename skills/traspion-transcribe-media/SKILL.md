---
name: traspion-transcribe-media
description: Transcribe an audio or video file with Traspion, from the user's device (upload panel) or from a link (Google Drive, Dropbox, OneDrive, SharePoint, or a direct https link), including speech-to-text, audio-to-text, video-to-text, speaker detection, or translation requests. Use when the user wants a new recording converted into a transcript.
---

# Transcribe audio or video to text with Traspion

The Traspion tools were first written for ChatGPT. Where a tool description or result mentions ChatGPT, read it as you, Claude. ChatGPT Canvas does not exist here.

## Which tool

- **A link** (Google Drive, Dropbox, OneDrive or SharePoint, or a direct https link to the media file): call `transcribe_from_link` once with it.
- **A file on the user's device**, or an audio or video file they attached to the chat: call `upload_media` once. It shows an upload panel in the chat. Tell the user to choose the file there (you can't pass an attachment to Traspion yourself) and press **Upload and transcribe**. The panel uploads the file and then posts its file ID and status in the chat. Don't call `upload_media` again for the same file.
- If no panel appears (for example in Claude Code, which doesn't show panels), ask for a share link instead, or suggest uploading at https://www.traspion.com. Don't read the file from disk or try to make a link for it yourself.
- If it's unclear which file the user means, ask before calling either tool.
- `transcribe_from_link` doesn't accept YouTube, Zoom, or folder links. If it refuses a link, relay its message and suggestion. Don't retry the same link or try another tool with it.

## Options

- If the user has not said how to handle speakers, ask one combined question before importing or showing the panel: "Would you like speaker labels? If yes, how many speakers are there (2–30), or should Traspion detect the number automatically?" Don't ask for a second confirmation after the answer; the original request already authorizes the import.
- If the answer is no, set `speakerPartitioning: false` and omit `speakersCount`. If yes with a count, set `speakerPartitioning: true` and pass that count. If yes but the count is unknown, set `speakerPartitioning: true` and omit `speakersCount` so Traspion detects it.
- Skip the speaker question when the user already said whether they want speaker labels. Never guess the number of speakers.
- Set `channelIdentification: true` only when the user asks for channel identification. Speaker labels and channel identification may both be on; then omit `speakersCount`.
- Use the tool defaults for other options. Pass a language, translation target, transcription prompt, PII redaction, or profanity filtering only when the user asks for it or gives the value.
- Don't claim that an option the tool doesn't offer was enabled.
- Never retry an import or upload automatically. A retry can create a duplicate Traspion file.

## Results

Treat the tool result as the truth:

- If transcription finished, fetch any remaining transcript pages the user's request needs with `get_transcription` and show the text in the conversation. Never call a partial page the complete transcript.
- After an upload, the panel's message gives the file ID and status. Use that `fileId` with `get_transcription`.
- If the import or transcription is still running, keep the returned `fileId`, explain the status and the suggested next step, and don't claim it is done.
- When the user asks to check progress, call `get_transcription` once with that `fileId`. If it is still processing, report that and stop. Don't poll in a loop or import the file again.
- If the file is waiting for minutes, or the account has no transcription balance, say so and give the exact Traspion billing link the tool returned. Don't retry or change the link.
- If a file is already waiting for minutes, the tool names it. Ask the user whether to add minutes on the website or delete the waiting file. Call `delete_waiting_file` only after the user clearly confirms deleting that file.
