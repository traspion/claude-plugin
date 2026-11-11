# Traspion for Claude

Transcribe audio and video with [Traspion](https://www.traspion.com) without leaving Claude. Works in Claude Code, the Claude desktop app, Cowork and claude.ai.

## What you can do

- **Transcribe a recording from a link.** Share a Google Drive, Dropbox, OneDrive or SharePoint link, or a direct https link to an audio or video file. Choose speaker labels, language, translation, PII redaction and profanity filtering.
- **Read your transcripts and translations**, with speaker labels and timestamps.
- **Translate** a transcript, using the stored Traspion translation when you asked for one at upload.
- **Edit and save** a transcript back to Traspion after you approve the changes.
- **Rename and export** files as PDF, TXT, DOCX or JSON.
- **Check your account:** plan, minutes left, billing history, custom vocabulary and spelling replacements.

You need a Traspion account. Sign up at [traspion.com](https://www.traspion.com).

## Install

In Claude Code:

```
/plugin marketplace add traspion/claude-plugin
/plugin install traspion@traspion
```

Then run `/mcp`, choose **plugin:traspion:traspion**, and sign in with your Traspion account.

In claude.ai or the Claude desktop app, go to **Customize → Plugins → Add → Add marketplace**, enter `traspion/claude-plugin`, install **Traspion**, and connect it when asked.

## Try asking

- "Transcribe this recording: <Google Drive link>. There are 2 speakers."
- "Show the transcript of my latest Traspion file."
- "Translate my latest transcript into Spanish."
- "Export my interview transcript as a Word document."
- "How many Traspion minutes do I have left?"

## Good to know

- **Links only.** Claude can't send an attached file to Traspion. Share the file as a link, or upload it at [traspion.com](https://www.traspion.com).
- **Your files stay in your account.** Traspion only reads files in the account you sign in with.
- **Some things stay on the website:** buying minutes, changing your plan, and deleting files. The one exception is a file waiting for minutes, which Claude can delete after you confirm.
- Claude never saves a translation it made itself to Traspion, and never re-uploads a file on its own.

## Help

- Support: [traspion.com/contact](https://traspion.com/contact) or support@traspion.com
- [Privacy policy](https://traspion.com/privacy) · [Terms of service](https://traspion.com/terms)

## License

The plugin files in this repository are released under the [MIT License](LICENSE). The Traspion service itself is proprietary and covered by its [terms of service](https://traspion.com/terms).

"Traspion" and the Traspion logo are trademarks of Traspion. They are not licensed under the MIT License. See [NOTICE](NOTICE).
