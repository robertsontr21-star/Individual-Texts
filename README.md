# Individual Texts

Send the same message to a whole list of people on iPhone — as separate, individual
texts (not a group chat) — with one tap. Built entirely with Apple's free, built-in
**Shortcuts** app. No App Store, no developer account, no cost.

Why Shortcuts instead of a "real" App Store app: a native app requires Xcode and a
paid/free Apple Developer setup on a Mac to install on your phone, and it wouldn't be
able to do anything Shortcuts can't already do here (iOS doesn't let third-party apps
send iMessage/SMS on your behalf anyway — only Apple's own Messages automation can).
Shortcuts is the actual free, no-code way to get this.

## What it does

You give it a message and a list of people. It loops through the list and calls
"Send Message" once per person, so each contact gets their own 1:1 text — never
combined into one thread.

There are two versions below. Start with **Option A** if you just want it working in
5 minutes. Move to **Option B** once you know who you'll be texting regularly (e.g.
a standing list of family, a team, a client list) so you stop re-selecting people
every time.

---

## Option A — Quick version (pick contacts each time)

1. Open the **Shortcuts** app on your iPhone.
2. Tap **+** (top right) to create a new shortcut. Name it something like
   **"Text Everyone"**.
3. Tap **Add Action** and add these actions in order:

   1. **Text** — type the message you want to send (or leave it and instead add
      **Ask for Input** → *Text* right before this step if you want to be prompted
      for the message every run).
   2. **Select Contacts** — turn on **"Select Multiple"**. This lets you pick as
      many people as you want from your Contacts.
   3. **Repeat with Each** — set it to repeat over the result of *Select Contacts*
      (tap the "Items" field → choose the magic variable for the contacts list).
   4. Inside the repeat block, add **Send Message**:
      - Set **Recipients** to the *Repeat Item* variable (the current contact).
      - Set the message body to your **Text** variable from step 1.
      - Tap the ⓘ (info) icon on the action and turn **off** "Show When Run" /
        make sure it's not set to show the compose sheet — you want it to send
        silently in the background. (On some iOS versions this is a toggle
        labeled "Show Message" — turn it off.)
4. Tap **Done**.
5. To run it: open Shortcuts and tap "Text Everyone", or add it to your Home Screen
   (Share → Add to Home Screen) so it looks and feels like a normal app icon, or
   ask Siri "Text Everyone."

The first time you run it, iOS will ask permission to access Contacts and to send
messages — allow both.

---

## Option B — Set-and-forget version (reusable broadcast list)

This skips re-picking people every time by using a **Contacts Group** as your
distribution list. (A Contacts group is just a saved list of people in the Contacts
app — completely different from an iMessage group chat. Nothing about it is shared
or visible to the people in it.)

### 1. Create the group once

- Open **Contacts** app → tap **Lists** (top left) → **Add List** → name it e.g.
  `Broadcast List`.
- Add everyone you want to be able to mass-text into that list.
- You can make more than one list (e.g. `Family`, `Book Club`) and duplicate the
  shortcut below for each.

### 2. Build the shortcut

1. Open **Shortcuts** → **+** → name it **"Broadcast"**.
2. Add actions in order:

   1. **Ask for Input** → *Text* → prompt: "What's the message?"
   2. **Find Contacts where** → set the filter to *List* **is** `Broadcast List`
      (the group you made above).
   3. **Repeat with Each** → Items = the result of *Find Contacts*.
   4. Inside the repeat, add **Send Message**:
      - Recipients: the *Repeat Item*.
      - Message: the *Provided Input* variable from step 1.
      - Turn off the compose/confirmation sheet so each send is silent.
3. Tap **Done**.

### 3. Run it

Tap the shortcut, type your message once, and it silently fires an individual
text to everyone on the list — each as their own separate thread.

Add it to your Home Screen (Share → Add to Home Screen) so it behaves like a
normal app icon, or trigger it by voice: "Hey Siri, Broadcast."

---

## Notes / gotchas

- **Blue vs green bubbles:** contacts using iMessage get an iMessage; contacts
  without it fall back to regular SMS. Both are sent as individual 1:1 messages,
  never grouped.
- **Cost:** this uses your phone's normal texting (iMessage is free over
  data/Wi-Fi; SMS falls under your carrier's plan — unlimited on most plans
  today, but check if you're on a limited plan).
- **Large lists:** sending to a lot of people back-to-back may trigger iOS/carrier
  spam-prevention pauses. For lists beyond ~15-20 people, consider splitting into
  two runs.
- **Editing your list:** just edit the Contacts group in Option B — no need to
  touch the shortcut again.
- **Personalizing per person** (e.g. "Hi John, ...") is possible by adding a
  **Text** action inside the loop that combines "Hi " + the contact's first name
  + your message, instead of sending the same static text to everyone.
