<img width="1649" height="1759" alt="image" src="https://github.com/user-attachments/assets/ab5f897d-80f1-4ba5-8d70-3f05fa75341f" /># LinkedIn Sora 2 Troll Extension

## Project Structure

Create a Chrome extension with the following files:

- `manifest.json` - Extension configuration with permissions for LinkedIn, context menus, clipboard
- `background.js` - Service worker for context menu and OpenAI API calls
- `content.js` - Extract LinkedIn post content from DOM
- `popup.html` - Display generated prompts
- `popup.js` - Handle popup interactions and clipboard copying
- `config.js` - API key configuration
- `styles.css` - Popup styling
- `README.md` - Setup instructions

## Implementation Details

### manifest.json

- Manifest V3 format
- Permissions: `contextMenus`, `activeTab`, `clipboardWrite`, `storage`
- Host permissions for `*://www.linkedin.com/*`
- Service worker: `background.js`
- Content script injected on LinkedIn pages

### background.js

- Create context menu item "Generate Sora 2 Prompt" on extension install
- Listen for context menu clicks
- Send message to content script to extract post content
- Call OpenAI API (GPT-5-thinking) with system prompt instructing it to:
- Analyze the LinkedIn post
- Generate a hysterical, trolling Sora 2 video prompt
- Make it funny and absurd while relating to the post content
- Store result in chrome.storage for popup to retrieve

### content.js

- Listen for messages from background script
- Find the closest LinkedIn post element from right-click position
- Extract post text, author info, and context
- Send extracted data back to background script

### popup.html/popup.js

- Display the generated Sora 2 prompt in a readable format
- Show loading state while generating
- Auto-copy to clipboard on display
- Manual copy button as backup
- Show success notification when copied

### config.js

- Store OpenAI API key (user needs to add their own key)
- Configuration for model selection (gpt-5-thinking)

## Key Features

- Context menu integration on LinkedIn posts only
- Intelligent post extraction (handles various LinkedIn post formats)
- GPT-5-thinking for high-quality, creative trolling prompts
- Auto-copy to clipboard + manual copy option
- Clean, modern popup UI
- Error handling for API failures
