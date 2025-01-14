# Capacitor WebViewCache Plugin

The native Android `WebView` caches images. If images are replaced on the server but keep the same filename, the `WebView` still shows the cached images. This plugin makes it possible to clear the `WebView` cache and control cache behavior.

## Features

- Clear WebView cache completely
- Control cache mode behavior
- Thread-safe implementation with proper error handling

## Install

```bash
npm install capacitor-plugin-webview-cache-extended
npx cap sync
```

## Usage

```typescript
import { WebViewCache, WebViewCacheMode } from 'capacitor-plugin-webview-cache-extended';

// Clear cache
await WebViewCache.clearCache();

// Set cache mode
await WebViewCache.setCacheMode({
  mode: WebViewCacheMode.LOAD_NO_CACHE
});
```

## Cache Modes

The plugin supports several cache modes through `WebViewCacheMode`:

- `LOAD_DEFAULT`: Uses cached resources when available and not expired, otherwise loads from network
- `LOAD_CACHE_ELSE_NETWORK`: Uses cached resources even if expired, falls back to network if not in cache
- `LOAD_NO_CACHE`: Always loads from network, bypassing cache
- `LOAD_CACHE_ONLY`: Only uses cached resources, never accesses network

## API

### clearCache()
Clears the WebView cache and deletes all cache files.

```typescript
await WebViewCache.clearCache();
```

### setCacheMode(options)
Sets how the WebView should use its cache.

```typescript
await WebViewCache.setCacheMode({
  mode: WebViewCacheMode.LOAD_NO_CACHE
});
```

The method returns the current cache mode after setting it:
```typescript
const result = await WebViewCache.setCacheMode({
  mode: WebViewCacheMode.LOAD_CACHE_ELSE_NETWORK
});
console.log(result.currentMode); // 'LOAD_CACHE_ELSE_NETWORK'
```
