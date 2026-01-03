---
name: skill-telegram-bot
description: Best practices for Telegram Bot (aiogram) and Userbot (telethon/pyrogram) development.
---

# Telegram Bot & Userbot Expert

This guide covers engineering patterns for building robust, scalable, and safe Telegram integrations.

## 1. Bot Framework: aiogram (v3.x)

### Handler Organization
- **Use Routers**: Separate handlers by feature or domain (e.g., `start.py`, `admin.py`, `settings.py`).
- **Filters**: Keep business logic out of handlers by using custom filters.
- **Middleware**: Use for global tasks like auth, logging, or database session management.

### States & FSM
- Use `State` and `StatesGroup` for multi-step dialogs.
- **Always** provide a `cancel` command to reset the state.
- Prefer `Redis` or `PostgreSQL` for FSM storage in production.

### Callback Data
- Use `CallbackData` factory classes for structured data.
- Keep `callback_data` strings short (limit is 64 bytes).

---

## 2. Userbot Frameworks: Telethon / Pyrogram

Userbots act on behalf of a real user account. Use with caution.

### Security & Safety
- **Avoid Flood Waits**: Respect Telegram's rate limits. Do not spam.
- **Session Management**: Secure `.session` files. Never commit them to Git.
- **Error Handling**: Catch `FloodWaitError` and wait for the specified duration.

### Use Cases
- Exporting chat history (e.g., `import_history.py` patterns).
- Managing massive amount of chats.
- Automating personal account tasks.

---

## 3. General Best Practices

### Rate Limiting & Performance
- **Batching**: Group messages or media when possible (e.g., `MediaGroup`).
- **Async Everywhere**: Never use blocking calls (`time.sleep`, synchronous requests) in handlers.
- **Retry Logic**: Implement exponential backoff for API calls.

### User Experience (UX)
- Use `MarkdownV2` or `HTML` for rich text formatting.
- Always provide immediate feedback (e.g., "typing..." or "uploading...").
- Handle the case where the user blocked the bot (`BotBlocked`).

### Data Persistence
- Store `user_id` as `BIGINT` in your database.
- Archive messages if they are needed for analytics (e.g., Supabase storage).
