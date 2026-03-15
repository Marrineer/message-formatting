# Message Formatting Context

A reusable **message style guide** extracted from `messages_en.properties` for consistent message generation across plugins and tools.

---

## What Is This?

`context.json` describes **how messages are formatted** in this project — colors, icons, layouts, and rules — so that AI agents or other tools can generate new messages that match the existing style automatically.

Think of it as a **design system for Minecraft chat messages**.

---

## Files

| File | Description |
|------|-------------|
| `messages_en.properties` | Original message file (EssentialsX Vietnamese config by © Earns) |
| `context.json` | Extracted formatting context — colors, icons, patterns, rules |
| `readme.md` | This file |

---

## Formatting System

| Property | Value |
|----------|-------|
| **Primary Format** | MiniMessage |
| **Legacy Support** | Yes — all colors include `&x` fallback codes |
| **Text Style** | Unicode small caps (ᴀʙᴄᴅᴇғ…) |
| **Language** | Vietnamese |

### MiniMessage Features Used

`<color:HEX>` · `<gradient>` · `<hover:show_text>` · `<click:run_command>` · `<click:open_url>` · `<bold>` · `<strikethrough>` · `<reset>`

---

## Color System

Every color includes three formats for cross-plugin compatibility:

```json
{
  "success": {
    "hex": "#99ff94",
    "minimessage": "<color:#99ff94>",
    "legacy": "&a"
  }
}
```

### Key Semantic Colors

| Role | Hex | MiniMessage | Legacy | Usage |
|------|-----|-------------|--------|-------|
| Success / Enabled | `#99ff94` | `<color:#99ff94>` | `&a` | ✔ confirmations |
| Error / Warning | `#ff7817→#ffc46b` | `<gradient:...>` | `&6` | Permission denials, errors |
| Disabled | `#ff7817` | `<color:#ff7817>` | `&6` | Toggled off states |
| Body Text | `#FFFFFF` | `<white>` | `&f` | All message body text |
| Separator | `#555555` | `<dark_gray>` | `&8` | ▪ between prefix and content |
| Money | `#ffc885` | `<color:#ffc885>` | `&6` | ⛃ economy messages |
| Teleport | `#52ffc2` | `<color:#52ffc2>` | `&b` | ⏩ tp requests |
| Home | `#cec2ff` | `<color:#cec2ff>` | `&d` | ⌂ home messages |
| Kit | `#ddb51e` | `<color:#ddb51e>` | `&6` | ⛏ kit messages |
| Mail | `#ffd978` | `<color:#ffd978>` | `&e` | ✉ mail messages |
| Discord | `#78d2ff` | `<color:#78d2ff>` | `&b` | ₪ discord integration |

> Full list with 24 semantic color roles available in `context.json`.

---

## Icons

Each module has a dedicated icon + color pair:

| Icon | Purpose | Color |
|------|---------|-------|
| ✔ | Success | `#99ff94` |
| ✖ | Failure / Disabled | red |
| ⛃ | Money | `#ffc885` |
| ⏩ | Teleport | `#52ffc2` |
| ⌂ | Home | `#cec2ff` |
| 🔱 | Warp | `#15edbe` |
| ⛏ | Kit | `#ddb51e` |
| ⚙ | System | `#ffdac4` |
| ✉ | Mail | `#ffd978` |
| 🗡 | Hypermode | `#a1ffd1` |
| 🔥 | Enchant | `#baa3ff` |
| ▪ | Separator | dark_gray |

> 35+ icons documented in `context.json`.

---

## Message Patterns

### Standard Message
```
<color:#ffc885>⛃</color> <white>ᴍᴏɴᴇʏ <dark_gray>▪ <white>message text
```
**Pattern:** `ICON` + `LABEL` + `▪` + `message`

### Success Message
```
<color:#99ff94>✔</color> <white>ᴛʜàɴʜ ᴄôɴɢ <dark_gray>▪ <white>message text
```

### Error Message
```
<gradient:#ff7817:#ffc46b>error text here.</gradient>
```
> No icon prefix — full gradient wrap.

### Notification Block (ban, mute, jail)
```
\n<gradient:#ffbaf4:#7dfdff>HEADER</gradient>\n
  type: <color:#e2ffc7>🛡 TYPE</color>
   <color:#e2d1ff>👤 </color>player: <color:#e2d1ff>VALUE</color>
   <color:#bcffa3>🪓 </color>by: <color:#bcffa3>VALUE</color>
```

---

## Consistency Rules

- Each module **always** uses the same icon + color pair
- Error gradient is **always** `#ff7817 → #ffc46b`
- Success icon is **always** `✔` with `#99ff94`
- Separator is **always** `▪` in `dark_gray`
- Body text is **always** `white`
- Enabled = `#99ff94` · Disabled = `#ff7817`
- Variables are highlighted in the category's accent color

---

## How to Use

### For AI Agents

Pass `context.json` as input when generating new messages. The agent should:

1. Match the **prefix pattern** for the relevant module
2. Use the correct **icon + color** pair
3. Apply the **error/success** convention
4. Highlight variables in the **accent color**
5. Use **Unicode small caps** for text content

### For Plugin Developers

Reference the `legacy` field when your plugin doesn't support MiniMessage:

```java
// MiniMessage
String msg = "<color:#99ff94>✔</color> <white>ᴛʜàɴʜ ᴄôɴɢ <dark_gray>▪ <white>Done!";

// Legacy fallback
String msg = "&a✔ &fᴛʜàɴʜ ᴄôɴɢ &8▪ &fDone!";
```

---

## Credits

**Config by:** © Earns
**Version:** v2.2 · 25/02/2025
