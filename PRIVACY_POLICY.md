# Privacy Policy for ezy Youtube Video Control

**Last updated: August 11, 2026**

## 1. Scope

This Privacy Policy explains how the Chrome extension **ezy Youtube Video Control** ("the extension") handles information while providing its YouTube viewing, player-control, navigation, and page-layout features.

The extension is independently developed and is not affiliated with, endorsed by, or sponsored by YouTube or Google.

## 2. Information the Extension Handles

The extension handles only information needed for its user-facing features:

- **Saved preferences:** aspect ratio, flips, filters, focus mode, playback and wheel settings, preferred quality, Theater Mode, Auto PiP, chapter-dot and video-summary settings, list-view and Shorts settings, video-list filters, caption language, playlist controls, and keyboard shortcuts. This includes any channel names, handles, or title keywords the user enters into exclusion fields.
- **Current YouTube page and website content:** the current URL and video identifier; player and page state; visible title, channel, view-count, duration, upload-time, watched, live, and upcoming indicators used by list filters; caption/player information; chapter titles and times; and, when Video Summary is enabled, the answer returned in YouTube's native Ask panel.
- **Limited YouTube Ask conversation text:** when Video Summary is enabled and the native Ask panel already contains a conversation, the extension checks existing user turns for the fixed localized summary wording and finds the latest completed summary answer. This is used only to avoid sending a duplicate request and to reuse an existing summary. Non-summary turns are not copied or retained by the extension.
- **Feature interactions:** relevant keyboard, mouse-wheel, click, scroll, and playback events are processed in real time to perform the action the user selected. They are not logged as an activity history.
- **Optional Google account authorization:** only when the user selects **Connect Google account**, the browser's Identity web-auth flow opens Google's account chooser for the Google Drive `appDataFolder` scope. After connection, the extension reads the connected Drive user's display name and email address through the Drive `about` resource so the popup can identify which account is connected. It does not request separate email/profile OAuth scopes, contacts, or general Drive files. To confirm app-data access, it may also read the ID, name, MIME type, creation/modification time, and version metadata of files already present in the extension's hidden app-only folder.
- **Optional settings synchronization and backups:** when the user enables settings sync or requests a backup, the extension stores synchronized preference values, per-setting modification timestamps, a randomly generated device identifier, schema/revision metadata, and up to five settings backup snapshots in its hidden Google Drive `appDataFolder`.
- **Optional channel-folder management:** when the user enables Channel Folders, the extension stores user-created folder names and order, channel IDs, channel titles, channel-page URLs, thumbnail URLs, folder assignments, ordering, modification metadata, and deletion markers locally. If channel sync is enabled, the same channel-library document is stored in the hidden Google Drive `appDataFolder`. When the user explicitly connects the YouTube subscription list, the extension uses the YouTube Data API to read the user's subscription IDs and the subscribed channels' IDs, titles, URLs, and thumbnails. It does not create a viewing history.
- **Optional YouTube subscription removal:** only after the user selects one or more subscribed channels, presses the separate unsubscribe control, and confirms the warning, the extension sends the selected subscription IDs to the YouTube Data API for removal. Moving a channel between extension folders, moving it to Unassigned, or deleting an extension folder does not unsubscribe the user from YouTube.

The extension does not create or retain a history of videos or pages the user visits.

## 3. How Information Is Used and Stored

- Saved preferences are stored locally on the current browser profile with Chrome's `chrome.storage.local` API. The current version does not transmit new preference changes through Chrome Sync. On the first run after upgrading from an earlier version, the extension copies its existing preference keys from legacy `chrome.storage.sync` storage into local storage. It temporarily leaves the legacy synchronized copy unchanged for rollback compatibility and does not continue writing new changes to it. Google Drive synchronization remains off by default; only after the user enables it are non-device-local settings exchanged with `appDataFolder` approximately every two minutes and shortly after local changes.
- Current YouTube page content, page state, chapter data, and interaction events are processed temporarily in the current browser tab only to provide the selected features. They are not sent to the developer and are not stored by the extension as a browsing or viewing history.
- Google account connection is optional. An interactive Google account chooser opens only after an explicit button click. A previously authorized connection may be checked or renewed without a visible prompt. OAuth access tokens are held only in the background service worker and in-memory `chrome.storage.session`; they are never written to persistent `chrome.storage.local`/`sync` storage or exposed to the popup or YouTube page. The display name is returned temporarily to the popup and is not stored. While connected, the email address is stored locally as a Google OAuth `login_hint` so silent token renewal stays bound to the selected account; it is removed when the user disconnects.
- Settings synchronization is local-first and optional. When enabled, the extension uploads and downloads `settings.json`, merges changes using per-setting timestamps and the random device identifier, and checks for remote changes at startup, when the popup is opened, on browser activity, and approximately every two minutes. Manual and automatic safety backups are stored as separate JSON files, with only the five newest backups retained. Turning sync off stops uploads and downloads but does not delete existing Drive data.
- Channel-folder management is off by default and local-first. When enabled, the extension replaces YouTube's native subscription section only after its own Channel Folders section has mounted successfully; disabling the feature or failing to mount restores YouTube's native section. Folder selection and expansion are device-local UI state. Channel-library synchronization is separately optional and exchanges `channel-library.json` with `appDataFolder` approximately every two minutes when enabled.
- Access to the YouTube subscription list is requested incrementally from Google's OAuth screen only after the user explicitly chooses to connect the list in the channel manager. Subscription data is kept in a short in-memory cache and normalized into the local channel library for the feature. Unsubscribe requests are never run on a schedule or as a consequence of folder editing.
- The developer does not operate a data-collection server and does not receive extension preferences, page content, prompts, summary responses, analytics, or telemetry from the extension.

## 4. Video Summary: YouTube Ask Processing

Video Summary is experimental and **off by default**. If the user enables it:

1. On each eligible YouTube watch page, the extension opens YouTube's native Ask panel and selects a summary suggestion when available. If no summary suggestion is available, it automatically inserts and submits one fixed localized prompt, such as **“Summarize this video”** in English or **“동영상을 요약해 줘”** in Korean.
2. The intended recipient is **YouTube Ask**. The request is handled in the current YouTube page by Google/YouTube. Google/YouTube may process the prompt, current video, account, and page context according to the user's Google/YouTube settings and Google's policies.
3. The extension reads the returned answer from the native Ask panel and keeps a cloned copy only in the current tab's memory so it can be displayed beside the player. The extension discards that copy when the feature is disabled, the page navigates, or the tab reloads.
4. The developer does not receive the prompt, video context, or answer. YouTube may retain the native Ask conversation according to its own service behavior and policies; the extension does not control or delete YouTube's copy.

If the native Ask panel already contains a conversation, the extension reads existing turn text only to determine whether the same summary was previously requested. If so, it reuses the latest completed answer; otherwise, it stops without adding a new question. It does not store unrelated conversation turns.

If YouTube Ask is unavailable for the account, region, or video, the feature stops without sending a request through any alternate service.

## 5. Sharing and Service Providers

The developer does not sell, rent, share, or transfer user information. The only external processing connected to the extension's features is:

- **Legacy Google Chrome Sync storage:** an earlier version may have synchronized saved preferences. The current version reads those existing extension preference keys once for local migration and leaves the legacy copy unchanged; it does not send new preference changes through Chrome Sync.
- **Google/YouTube Ask:** processes the fixed summary request and relevant current-video context only when the user has enabled Video Summary and YouTube Ask is available.
- **Google OAuth web authorization and Google Drive API:** the browser's Identity web-auth flow opens Google's account chooser independently of the browser profile. The Drive API provides access to this extension's hidden `appDataFolder`, returns the current Drive user's display name and email address for account identification, and—only when the user enables sync or requests backup/restore—stores and retrieves the extension's settings and backup JSON documents.
- **YouTube Data API:** only after the user explicitly connects the subscription list, reads the user's current subscriptions and limited channel metadata for Channel Folders. It removes subscriptions only after a separate selection and confirmation flow. Google/YouTube processes these requests under the user's Google account and policies; the developer does not receive them.

The extension does not share data with advertising networks, analytics providers, data brokers, or developer-operated services.

## 6. Permissions

- **`storage`:** saves preferences, synchronization metadata, a random device identifier, and the connected-account email renewal hint locally and, during the one-time upgrade migration, reads this extension's legacy synchronized preference keys.
- **`identity`:** opens the browser's OAuth web-auth flow and receives the approved redirect after an explicit action. Initial Google Drive connection requests `https://www.googleapis.com/auth/drive.appdata`. If the user later selects **Connect subscription list** in Channel Folders, the extension incrementally requests `https://www.googleapis.com/auth/youtube` to view and manage the user's YouTube account, including current subscriptions and user-confirmed unsubscription. No separate email/profile OAuth scope is requested. The Drive API's `about` resource provides the connected user's display name and email address under the Drive scope.
- **`alarms`:** schedules the optional settings synchronization check approximately every two minutes and provides a fallback for deferred local-change uploads while the background service worker is suspended.
- **`https://www.youtube.com/*` (host access):** runs packaged scripts and styles on YouTube pages so the extension can apply the selected player, layout, list-filter, chapter, summary, caption, playlist, recommendation, and Shorts features.
- **`https://www.googleapis.com/*` (host access):** calls the Google Drive API to verify access and manage user-enabled app-only settings/channel data, and calls the YouTube Data API after explicit subscription-list connection to read subscriptions or perform user-confirmed unsubscription.
- **`https://oauth2.googleapis.com/*` (host access):** requests revocation of the current OAuth access token when the user disconnects the account.

The extension does not request `identity.email`, `tabs`, `activeTab`, `scripting`, browsing-history, cookies, or web-request permissions.

## 7. Advertising, Analytics, and Remote Code

- The extension contains no advertising, analytics, tracking, or telemetry.
- The extension does not download or execute remote code. All executable logic is included in the extension package.
- Interacting with YouTube's existing page and native Ask service does not download executable logic into the extension.

## 8. Retention and User Control

- Local preferences remain in Chrome storage until the user resets or removes the extension or clears its storage. A legacy synchronized copy from an earlier version may remain in Chrome Sync temporarily for rollback compatibility until the user removes synchronized data or a later migration explicitly cleans it up. The developer cannot access or delete either copy because the developer never receives it.
- Current page state, chapter data, interaction events, and the extension's temporary summary copy are discarded when no longer needed, including on navigation, reload, tab closure, or feature disablement as applicable.
- Google OAuth access tokens remain only in service-worker memory and `chrome.storage.session` until they expire, the browser session or extension is restarted, or the user selects **Disconnect**. Short-lived tokens are silently renewed when Google still permits it. The locally stored email renewal hint remains only while connected. Disconnecting disables settings sync, clears the hint and session token, and requests Google token revocation, but does not delete data already stored in `appDataFolder`.
- Cloud `settings.json` and the five newest backup snapshots remain in `appDataFolder` when sync is turned off or the account is disconnected so that another connected device or a later reconnection can restore them. Restoring a backup creates a safety backup of the current settings first. A separate cloud-data deletion control must be used when that feature is provided; sync OFF and Disconnect do not imply deletion.
- Local channel folders and channel assignments remain until the user edits/resets them, removes the extension, or clears its storage. If channel sync is enabled, `channel-library.json` remains in `appDataFolder` when sync is turned off or the account is disconnected. The extension's subscription-list cache expires after approximately five minutes. A subscription removed through the confirmed YouTube API action is controlled by YouTube and is not restored by reconnecting or restoring extension folder data.
- Legacy data retained by Chrome Sync and data retained by YouTube are controlled by Google and the user's Google/Chrome settings and are subject to Google's policies.

## 9. Limited Use

Information is handled only to provide or improve the extension's disclosed single purpose and user-facing features. It is not used for advertising, creditworthiness, unrelated analytics, or sale to third parties, and the developer does not permit humans to read it.

The use of information received from Google APIs will adhere to the Chrome Web Store User Data Policy, including the Limited Use requirements.

## 10. Changes to This Policy

If the extension's information-handling practices change, this policy, the Chrome Web Store disclosures, and any required in-product disclosure will be updated before the changed practice takes effect.

## 11. Contact

Questions about this policy may be sent to `ohnagi@gmail.com`.

---

## 한국어 요약

- 확장 프로그램은 기능 제공에 필요한 설정, 사용자가 입력한 제외 채널·키워드, 현재 YouTube URL·페이지 요소·플레이어 상태·목록 메타데이터·챕터 정보와 관련 입력 이벤트를 처리합니다. 현재 탭에서 일시 처리하며 방문·시청 기록을 만들지 않습니다.
- 동영상 요약을 켠 상태에서 YouTube 질문하기에 기존 대화가 있으면, 중복 질문 방지를 위해 기존 사용자 턴에 고정 요약 문구가 있는지 확인하고 마지막 완료 요약을 찾습니다. 관련 없는 대화는 복사·저장하지 않습니다.
- 설정은 현재 브라우저 프로필의 `chrome.storage.local`에 저장되며 새 설정 변경은 Chrome 동기화로 전송하지 않습니다. 이전 버전에서 업데이트한 첫 실행에는 기존 `chrome.storage.sync` 설정을 로컬로 한 번 복사하고, 롤백 호환성을 위해 기존 동기화 사본은 당분간 변경하지 않은 채 유지합니다. 개발자는 어느 사본도 받지 않습니다. Google Drive 설정 동기화는 기본 OFF이며 사용자가 켠 경우에만 기기 로컬 UI 상태를 제외한 설정, 키별 수정 시각과 임의 기기 ID를 앱 전용 폴더에서 약 2분 간격으로 교환합니다.
- 대화형 Google 계정 선택창은 사용자가 연결 버튼을 누른 경우에만 열립니다. 기존 승인 상태는 화면 없이 확인·갱신될 수 있습니다. 별도의 이메일·프로필·연락처·일반 Drive 파일 권한은 요청하지 않고 `drive.appdata` 범위만 요청합니다. 연결 후에는 Drive `about`에서 현재 사용자의 표시 이름과 이메일 주소를 읽습니다. 표시 이름은 팝업에 일시 표시하고 저장하지 않으며, 이메일은 선택한 계정으로 무음 재인증하기 위한 `login_hint`로 연결 해제 전까지 로컬에 보관합니다. 액세스 토큰은 background service worker와 메모리형 `chrome.storage.session`에서만 다루며 영구 저장소, 팝업, YouTube 페이지에는 전달하지 않습니다.
- 사용자가 동기화를 켜거나 백업/복원을 실행하면 `settings.json`과 최대 5개의 백업 JSON을 Drive `appDataFolder`에 저장합니다. 동기화 OFF와 연결 해제는 클라우드 파일을 삭제하지 않으며, 복원 전에는 현재 설정을 자동 안전 백업합니다.
- 채널 폴더 기능은 기본 OFF입니다. 켜면 사용자가 만든 최대 2단계 폴더, 채널 ID·이름·페이지 URL·썸네일 URL, 폴더 배치·정렬·수정/삭제 메타데이터를 로컬에 저장하고, 채널 동기화를 별도로 켠 경우 `channel-library.json`을 Drive 앱 전용 폴더에서 약 2분 간격으로 교환합니다. 좌측 폴더 선택·접기 상태는 현재 기기에만 저장됩니다.
- 사용자가 채널 관리 화면에서 구독 목록 연결을 명시적으로 누른 경우에만 YouTube 관리 범위를 증분 요청하고, YouTube Data API에서 현재 구독 ID와 제한된 채널 정보를 읽습니다. 폴더 삭제·미분류 이동은 실제 구독에 영향을 주지 않습니다. 별도 빨간 구독 해제 버튼과 대상 수·영향 경고를 확인한 경우에만 선택한 실제 YouTube 구독을 해제합니다.
- 동영상 요약은 기본 OFF입니다. 켜면 지원되는 각 영상에서 고정된 로케일 요약 문구(한국어: “동영상을 요약해 줘”)가 YouTube 질문하기에 한 번 자동 전송됩니다. Google/YouTube가 현재 영상·계정·페이지 문맥과 함께 처리할 수 있으며, 개발자는 요청이나 답변을 받지 않습니다.
- 요약 답변 복제본은 현재 탭 메모리에만 유지되고 이동·새로고침·기능 해제 시 폐기됩니다. YouTube 네이티브 대화의 보존은 Google/YouTube 정책과 서비스 동작을 따릅니다.
- 광고·분석·추적·개발자 운영 서버·원격 코드가 없습니다. 계정 연결과 앱 전용 Drive 설정/채널 동기화, 사용자가 요청한 YouTube 구독 목록 조회·해제를 위해 `identity`, `storage`, `alarms`, `https://www.googleapis.com/*`, `https://oauth2.googleapis.com/*`를 사용합니다. 별도 이메일·프로필 OAuth 범위는 요청하지 않으며 YouTube 관리 범위는 채널 관리 화면의 명시적 연결 동작에서만 증분 요청합니다.
- 문의: `ohnagi@gmail.com`
