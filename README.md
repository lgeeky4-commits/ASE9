# ASE / Crimson Chat — Version 2.5

This ZIP is the **complete website project**, not a standalone offline HTML page. It includes all earlier features and wallpapers. Deploy it as a Node.js + Socket.IO web service on HTTPS; you do not need to install an app on your phone.

## What's new

1. **Sharper, square-edged interface:** crisp borders, no unnecessary rounded corners or blurred panels. The push-to-talk **🎙 RADIO** button is now much bigger (and turns to **● LIVE** only while transmitting).
2. **Unstretched call cameras:** removed the old 36% vertical distortion. Video uses its natural aspect ratio with black space if necessary instead of pulling people out of proportion.
3. **Safer minimized calls:** the X on the full call minimizes it to a draggable small window while preserving the video elements and connection. The small window has **Restore** and a clearly labeled **END** button—minimizing never sends a hangup command. Double-tap the miniature call to restore. Phone browsers can still interrupt WebRTC when the entire tab is backgrounded, which the site cannot override.
4. **`//CODETERMINAL`:** type this *exactly* in the message composer and send. It opens a **different, landscape-oriented imaging console** from `//CODEMENU`: big map left, status/filter and contacts on the top-right, chat on the bottom-right. `//CODEMENU` is still available and keeps its earlier layout. Retype the code or press Exit to return.
5. **Display simulations:** the new console has Normal, Heat, Thermal, and Night display filters for your **fixed picture-based map**, grid, and targeting lines. These are cosmetic color effects—not real heat sensing, infrared camera measurements, or true night vision.
6. **Timed reports:** the new console can show all map reports or only ones uploaded during the last 15 minutes, hour, or day. Report list entries show relative ages; choosing a report displays its date/time.
7. **Take a photo or video without leaving the browser:** Map → Photo or Video → **Browser Camera**; allow camera permission, then snap a photo or record/stop a short **silent** clip. You can reverse cameras. The media remains local until you place it on the map and save it. In-browser recording stops at 12 seconds and supports video WebM or MP4 where the browser allows; Choose File remains a fallback.
8. **CCTV map-report treatment:** map photos and video playback appear **black-and-white** with an **ASE/date/time overlay at bottom-left**. Browser-captured photos have that treatment burned into the JPEG; browser-recorded videos are encoded from the treated canvas. Uploaded files are treated visually in the report viewer, and their label says **ADDED**, not a guessed capture date. This does not create a separately downloadable edited copy of externally uploaded videos.

## Deploy / update

1. Extract the ZIP. It contains `server.js`, `package.json`, `README.md`, and `public` (including `public/map-image.png` and the 40 wallpaper SVGs).
2. Upload the extracted files and folders to the **root** of your GitHub project, replacing older copies. Don't upload only the ZIP and don't place everything inside an extra nested folder.
3. On Render, connect the repository as a Web Service with **Build Command** `npm install` and **Start Command** `npm start` (Node runtime). Deploy it.
4. Open the HTTPS Render website in mobile Chrome/Safari. Camera and microphone must be allowed. Use landscape orientation for either terminal.

## Limits / testing

- Local tests: JS syntax, HTML control-ID integrity, CODETERMINAL controls, mode switching, report time filter, staged in-browser photo/video capture with a simulated camera stream, and call minimize → restore → explicit end passed in Chromium. **These are not equivalent to complete phone-to-phone deployment tests.**
- We could not install Express/Socket.IO packages in this workspace because the npm registry was unreachable, so a real multiplayer server + two-phone WebRTC call test **has not been run here**. Actual recording codecs and camera permission handling must be tested on your deployed HTTPS site.
- Calls are browser WebRTC; on some networks a TURN relay is needed. Calls and reports are stored only in memory until permanent storage is added. Public/private room access checks in the existing server remain in place.
- Photo/video source timestamps are informational and cannot certify the actual moment a previously uploaded file was originally recorded.
- Emergency alerts are in-app notifications only, not emergency services. They never auto-answer another person's microphone or camera.

---

## Previous version notes (for reference)

# ASE / Crimson Chat — Version 2.4

## New in 2.4

- Radio FX dropdown in each chat: Clean, Walkie-talkie, Bass, Bright, Robot, Echo, Tunnel, Crunch, Muffled, and Distant. The selected effect processes transmitted voice audio. Pick the effect **before holding the radio button**; selecting another effect mid-transmission applies next time.
- Optional **Beeps** toggle adds short push-to-talk start/end chirps (also on received transmissions). Voice effects and beeps can be turned off; preferences are saved in the current browser.
- Radio: hold the on-screen 🎙 button; release to stop. With a physical computer keyboard, hold **R** while outside text fields to talk; release R to stop. Space/Enter work when the radio button has focus.
- Experimental: if a rare browser delivers both Volume Up `keydown` and `keyup` events to webpages, holding Volume Up uses radio. **Most Android/iPhone browsers do not permit a website to capture the phone's physical volume buttons**, so this is not a reliable phone shortcut. A 12-second failsafe cuts the radio off if the release event is missing. The regular on-screen button is the recommended phone control.
- Private call videos are drawn 36% taller (`scaleY(1.36)`) on your screen, with their containers clipping overflow to prevent spill. This is a visual stretch, not a change to captured/transmitted camera resolution; it may crop part of the picture.

## Notes

Requires HTTPS for microphone and camera. No automatic microphone access. Chat privacy still enforced server-side as in previous version. Messages/media stored temporarily in memory; no permanent database. Streaming/calling needs network testing between separate phones.

---

# Crimson Chat ASE — v2.3

All features from v2.2 are included, plus:

- **Hold-to-talk radio** in public and private chats: press and hold the microphone beside the message input. Releasing stops microphone capture. Receivers in that conversation can hear speech live; private transmissions stay in that pair. A speaker occupies the radio in a room until release. Audio is not recorded or saved. **Tap `🔊 audio` if your browser prevents incoming audio playback**. HTTPS and microphone permission are required.
- **Tap your small self-camera preview** in a private video call to make it the large view on your screen; tap the other small video to switch back. This does not change anyone else’s layout.
- **Camera color filters** apply to your outgoing camera as before and additionally to **the other caller’s video as displayed on your device only**. The other caller’s original video is not modified.
- **Exit Fullscreen** button appears inside the fullscreen video area, so you can leave fullscreen even when the call toolbar is hidden. The original entire-app fullscreen toggle remains available.
- **Rear camera** request uses an explicit rear-facing camera constraint (with device-label fallback), instead of merely suggesting it. On a device without a rear camera the app reports the limitation rather than incorrectly saying it switched.

**Browser notes:** The radio uses short, uncompressed 16 kHz audio chunks over the Socket.IO connection. It is designed for a tiny, 3-user room, rather than high-quality music/audio. The first press may display a microphone permission prompt. Audio playback can require tapping `🔊 audio`, especially on iPhone. Push-to-talk works only while the browser tab is active.

**Deploy:** upload these files (including `public/wallpapers`) to GitHub and deploy on Render with Build Command `npm install`, Start Command `npm start`. Use an HTTPS URL for camera and microphone.

**Testing limitations:** Static and isolated browser-side checks do not guarantee WebRTC connections work between two independent phones or through restrictive networks. Render's free plan may sleep. No media is persistently stored. Do not treat this application as a reliable emergency communication service.

---

# CRIMSON CHAT — COMPLETE BROWSER PROJECT

Version 2.2 · three-user real-time chat, a fixed map image, camera reports, LIVE streaming, private voice/video calls, wallpapers, mutual trust, and a landscape terminal mode.

## Put it online (Windows or phone browser)

1. Extract the ZIP. Inside is `server.js`, `package.json`, `README.md` and the **entire `public` folder**. Keep the folder names.
2. Create or open your GitHub repository at https://github.com/new. Upload **all** the extracted items (not the ZIP itself); the `public/wallpapers` folder must contain `wall-01.svg` through `wall-40.svg` (animated wallpapers are CSS, not additional SVG files).
3. In Render (https://render.com), choose **New → Web Service**, connect the GitHub repository, select **Node**. Build command: `npm install`. Start command: `npm start`. Select the available hosting plan and deploy.
4. When the status becomes **Live**, open the HTTPS `.onrender.com` address on your phone and another device.
5. Each person enters a different name. Up to three connected people can join at once.

**Important:** Opening `index.html` directly in a browser is not enough for multi-user messaging. The online Node/Socket.IO server must be running. You do **not** need to install Node on the phone: the hosting provider runs it.

## What's new in 2.2 — fullscreen, outgoing voice effects, call drawing, live wallpapers

- **Fullscreen:** Tap **⛶ full** near the bottom-right of the website to enter/exit browser fullscreen. During a private **video call**, **⛶ fullscreen** enlarges the call video stage specifically. Exit using the same control or the browser's Escape/exit control. Some iPhone browsers restrict fullscreen websites; the app shows an explanation if unsupported.
- **10 voice presets plus Normal:** In a private voice or video call, choose Echo, Deep (bass), High (treble), Robot, Radio, Cave, Alien, Megaphone, Whisper (airy), or Telephone. Browser Web Audio processing is applied to the **outgoing microphone track** before it is sent to the other caller when supported; it does not alter chat audio or people viewing LIVE broadcasts. **Deep/High change equalization/timbre, not the actual voice pitch**; the effect is intentionally labeled so it isn't misrepresented as true pitch shifting. Some voice effects may sound different across microphones/devices, and old browsers may use the unmodified mic as fallback. Use headphones to avoid speaker feedback when calling.
- **Point and Draw while in a private video call:** Tap **● point** or **╱ draw**, then tap/drag over either **their video** (main feed) or **your video** (small preview). The person on the other end sees the marks over the matching camera view. They are temporary overlays, not changes to the video recording; pointers and strokes vanish after **2 seconds without interaction**. Tap **off** to stop drawing. Each drawing signal is limited to the two users in that accepted private video call, not sent to the public room or saved on the server.
- **Two moving wallpapers:** In **walls**, choose **LIVE · Scrolling Grid** or **LIVE · Orbit Circles**, in addition to 20 regular and 20 `//CODEWALL` unlockable static wallpapers. Animations are made with CSS and require no internet image service. If your system is set to *Reduced Motion*, these patterns remain still. With mutual **trust**, either live wallpaper can be shared in that private chat.
- No change to the original square-edged crimson interface, static picture-based map, map reports, photo sharing, LIVE video, terminal layout or trust/emergency tools.

**Verified for 2.2:** HTML element and JavaScript syntax checks, 42 wallpaper choices, screenshot-sized layout checks, temporary-pointer timeout, incoming/outgoing drawing callbacks, and all 10 Web Audio effects creating a valid processed audio track in a local browser test. **Not verified in this environment:** a real voice-filtered call or synchronized drawings between separate phones over HTTPS. Test those with two devices on your deployed Render site; direct WebRTC may require a TURN relay on some networks.

## What's new in 2.1 — ASE, camera switching, mini-call window

- A large translucent **ASE** logo sits in the center of the conversation panel behind messages. It is visible in both regular chat and landscape `//CODEMENU` without obstructing taps.
- **Reverse camera** buttons are available in the browser's **take photo** dialog, when you broadcast your own LIVE video, and during your own private **video call**. They attempt to switch between front/back cameras. Some devices expose only one camera or ignore facing-mode requests.
- The **X** in a started private call now **minimizes instead of hanging up**. A small video/call window appears in the top-right, can be **dragged by its header**, and **double-tapped** to restore the full call. There is also a square restore button and a separate end-call button in the small window. An unaccepted incoming call is still declined when X is pressed.
- **Camera colors** are a new **separate** set of brightness, contrast, hue and saturation sliders. Open them from the photo camera, your live-video window, or your video call. They persist locally and do not change the full interface filter settings. Browser snapshots include the camera filter. Where browser canvas-stream capture is supported, the filtered camera is also what your LIVE viewers and private video-call recipient receive; older browsers may send unfiltered video as fallback.
- Camera and microphone use always require permission and user initiation. A minimized call keeps its microphone/camera active until **End Call** is pressed, the connection ends, or browser permission is revoked.

## Chat and cameras

- Public conversation includes everyone. Tap a name for one-on-one private messages; back arrow returns to the three-person conversation.
- A photo button beside the message field opens **take photo** or **gallery**. Browser camera uses `getUserMedia` after permission. A **device camera** file-picker fallback is provided when the browser cannot use the live camera view. Confirm a preview and caption before sharing.
- In a private chat, **call** starts an audio call or **video call** starts a two-way video call. The person receiving the call must press **accept** before their microphone/camera starts; all calls can be declined/ended/muted. HTTPS, browser permission, and a connection that supports WebRTC are required.
- Tap **go live**, grant camera access, and then start broadcasting. Other people can tap the `LIVE` label under your name to watch. You can record up to 20 seconds of **your own** stream with **record** and **stop**, then optionally put that clip on the map. No viewer-side automatic recording.

## Map (your fixed picture, no live map service)

- Map button = three white vertical strokes at top-right. Back arrow returns to the chat.
- **mark area** places a point with a text bubble. **path** places up to 30 waypoints, then **finish** and add a message.
- **photo** / **video** lets you take or choose media, tap a map location, add a caption, and save it. **Reports** tab holds the photo/video annotations; **Marks** tab holds normal points and paths. Tap video reports to play them.
- Public items are delivered to everyone; private items stay with only the two participants in that pair. The server checks room membership for every media fetch.
- **! emergency**: choose the spot on the map, choose an online person, and send an urgent in-app point alert plus a ringing audio-call request. This is *not* a call to emergency services. The recipient **must manually accept** the call; no camera/microphone is opened automatically.

## Wallpapers and visual settings

- Press **walls** to choose from 20 unique abstract wallpapers (circles, squares, grids, waves, patterns, gradients).
- Type `//CODEWALL` into the message field and press send to unlock **20 additional** darker, sharper patterns. This is a local display command, not a chat message. The unlock stays on that browser.
- **filters** affects the entire screen: grit, contrast, brightness, hue and saturation. These preferences are saved locally.
- **trust** appears in one-to-one chats. Both people must press trust. When both approve, the app displays an **8-character pairing label** and either person may select a wallpaper that updates **both users' private chat background**. Untrust revokes further shared wallpaper changes.
- **The pairing label is for visual confirmation ONLY**. It is **not** real authentication, encryption, a secret credential, or a password. Never share sensitive data assuming the code secures the connection.

## `//CODEMENU` terminal layout

- Type `//CODEMENU` into chat and send to open/close the local alternate screen.
- The screen is designed for a **phone held horizontally**: the **chat is on the left**, the **fixed-image map with drone-like grid and crosshair is in the middle**, and **conversation/tool tabs are on the right**.
- Under the map, directional **touchpad** buttons move the crosshair; choose **MARK** or **PATH** first, then tap **PLACE** to add points. Standard touch-to-mark works too.
- Tap **EXIT TERMINAL** to return to the original square red/black layout. The fake tactical crosshair is decorative: it is not connected to a real drone, GPS, location tracker, or weapon.

## Important limitations

- **Temporary storage only**: text messages, map items, chat photos, and report media are stored in server memory. They can disappear after redeploy, server restart or free-host sleep/restart. No permanent database has been configured.
- Up to **three connected users**, not secured personal accounts. Names can be reused when someone disconnects; this app is a demo, not for confidential chat or sensitive photos. It has **no end-to-end encryption**.
- Photo messages are compressed to JPEG. Photo reports use JPEG and video reports support WebM/MP4/MOV up to 8 MiB each. Some mobile formats may not play on other browsers; use MP4/WebM where possible.
- Some carrier networks prevent direct WebRTC connections; production reliability may require a **TURN relay service**. A public Render HTTPS site is needed for camera/microphone prompts to work on phones.
- The new version passed HTML/JavaScript structural checks and syntax checks. **Live browser interaction testing and two-phone camera/microphone/media-call testing were unavailable in this environment**, and npm dependency installation failed because the package registry was unreachable. Camera switching and filtered WebRTC streams can vary by browser and network; test these features on your HTTPS deployment.
- `//CODEWALL` and `//CODEMENU` are interface commands for the local device; no server admin or hacking features are enabled.

## Files

```
package.json
server.js
README.md
public/
  index.html
  style.css
  app.js
  map-image.png
  grit-noise.png
  wallpapers/
    wall-01.svg through wall-40.svg
```

## Run locally on a computer (optional)

```bash
npm install
npm start
```
Then open `http://localhost:3000` on the same computer. This address is **not** public until you deploy it.


## v2.6: disconnect cleanup / opt-in training challenge / no emoji icons
- Disconnecting or leaving the site removes that participant's saved map pins, paths, emergency markers, and photo/video reports from all rooms immediately. Other participants receive real-time `map:removed` events. Their public chat messages remain, but their map media is removed from memory.
- The HACK SIM button opens a **fictional cybersecurity challenge**, not access to real private conversations. It cannot read private chat messages, photos or private map data. A participant **must enable** training challenges before appearing as a target. This is disabled by default.
- Read the code printed beside the opted-in participant. Type it to get a reserved fake example IP (203.0.113.x), compute a checksum, and enter both fields. Successful completion opens a **scripted sample transcript and fictional marks** for exactly 60 seconds, then closes automatically.
- While attempting the puzzle, the challenger hears synthesized square-wave beeps (if sound is enabled). A person who opted in hears a brief sine/sawtooth synthesized alarm and sees an alert after another participant completes the training puzzle. Audio is browser-dependent and can be disabled.
- The interface now uses textual controls in place of emoji pictographs; the square-edged theme remains.
- No credentials, network scans, real IP discovery, interception, or hidden access features are involved.
