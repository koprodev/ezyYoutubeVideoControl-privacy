# Privacy Policy for ezy Youtube Video Control

**Last updated: August 6, 2026**

## 1. Scope

This Privacy Policy explains how the Chrome extension **ezy Youtube Video Control** ("the extension") handles information while providing its YouTube viewing and player-customization features.

The extension is independently developed and is not affiliated with, endorsed by, or sponsored by YouTube or Google.

## 2. Information the Extension Accesses

The extension accesses only the information required to provide its user-facing features:

- **Extension preferences:** aspect ratio, video flips and filters, Video Focus Mode, playback speed, mouse-wheel behavior, preferred quality, Theater Mode, Auto PiP, list-view and Shorts options, video-list filter settings (including any channel names or title keywords you type into the exclusion fields), caption language, playlist controls, and keyboard shortcuts.
- **Current YouTube page state:** the current YouTube URL and the page/player elements needed to apply the selected settings. This processing occurs inside the active YouTube page.

The extension does not record or build a history of the videos or pages you visit.

## 3. Collection, Use, and Storage

- The developer does **not** collect personal information, browsing history, video history, communications, authentication data, financial data, or location data.
- The extension does **not** transmit user information to the developer or to any developer-operated server.
- Extension preferences are stored with Chrome's `chrome.storage.sync` API solely to remember and synchronize the user's settings. When Chrome Sync is enabled, Chrome may synchronize those preferences through the user's Google account according to the user's Chrome settings and Google's privacy terms.
- Current YouTube page and player state is processed temporarily in the browser only to provide the extension's features. It is not retained or shared by the extension.

## 4. Permissions

- **`storage`:** Saves and synchronizes the user's extension preferences.
- **`https://www.youtube.com/*` (host access):** Runs the packaged content scripts and styles on YouTube pages so the extension can adjust the player, page layout, captions, playlists, recommendations, and Shorts behavior selected by the user.

The extension does not request the `tabs`, `activeTab`, `scripting`, browsing-history, identity, cookies, or web-request permissions.

## 5. Sharing, Advertising, and Remote Code

- No user information is sold, rented, shared, or transferred to third parties by the developer.
- The extension contains no advertising, analytics, or tracking technology.
- The extension does not download or execute remote code. All executable code is included in the extension package.
- The use of information received from Google APIs will adhere to the Chrome Web Store User Data Policy, including the Limited Use requirements.

## 6. Retention and User Control

Preferences remain in Chrome storage until the user resets the extension settings, removes the extension, clears the extension's stored data, or removes the synchronized data through Chrome. The developer cannot access or delete this data because it is never received by the developer.

## 7. Changes to This Policy

If the extension's information-handling practices change, this policy and any required in-product or store disclosures will be updated before the changed practice takes effect.

## 8. Contact

Questions about this policy may be sent to `ohnagi@gmail.com`.

---

## 한국어 요약

- 확장 프로그램은 기능 제공을 위해 현재 YouTube 페이지의 URL·플레이어 상태와 사용자가 선택한 설정(제외 채널·제외 키워드로 직접 입력한 문자열 포함)만 브라우저 안에서 처리합니다.
- 개인정보·시청 기록·브라우징 기록을 개발자가 수집하거나 외부 서버로 전송하지 않습니다.
- 설정은 `chrome.storage.sync`에 저장되며 Chrome 동기화가 켜진 경우 사용자의 Chrome 설정과 Google 정책에 따라 동기화될 수 있습니다.
- 광고·분석·추적·원격 코드가 없으며, 사용 권한은 `storage`와 `https://www.youtube.com/*`로 제한됩니다.
- 문의: `ohnagi@gmail.com`
