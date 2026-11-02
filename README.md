# code-box
Gives students a place to write code, then copy/paste it into your LMS for quiz/exam questions.
The webpage will just be a full page textbox, set up to be good for writing simple code.
The textbox should include the following:
- monospace font
- tab for indentation
- shift-tab for unindentation
- no autocomplete
- no syntax highlighting
- line numbers on the left side
There should also be a "Copy Code" button that selects all the code in the textbox and copies it to the clipboard to make pasting it into the LMS easy.

Optional: prefill the textbox with starter code or comments via the URL, e.g. `?code=%23%20Write%20a%20function` (`starter` also works). Use URL-encoded text; a literal `\n` becomes a newline.
