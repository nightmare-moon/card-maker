Dossier — Character Card Maker

A lightweight, single-file browser application for creating, editing, importing, and exporting Character Card v2 (chara_card_v2) character cards.

Dossier runs entirely in your browser. No server, database, build system, or installation is required.

Features
Create Character Card v2 characters
Live character preview
Upload a character portrait
Export cards as:
.card.png
.card.json
Embed Character Card JSON directly inside exported PNG files
Import existing Character Card PNG files
Import existing Character Card JSON files
Edit imported cards and export updated copies
Add alternate greetings
Define personality and example dialogue
Add custom system prompts
Add post-history instructions
Create lorebook entries with trigger keywords
Add creator metadata, tags, notes, and character versions
Drag-and-drop support for images and card files
No backend required
Interface

The interface is organized into five sections:

Core — character name, description, scenario, first message, and alternate greetings
Voice & Behavior — personality, example messages, system prompt, and post-history instructions
Lorebook — optional keyword-triggered lore entries
Metadata — creator, version, tags, and creator notes
Export — load an existing card or export the current character

A live character preview is displayed beside the editor.

Requirements

You only need a modern web browser such as:

Chrome
Edge
Firefox
Brave
Opera

No Node.js, Python, Docker, database, or web server is required.

Running the Application

Clone the repository:

git@github.com:nightmare-moon/card-maker.git

Open the project directory:

cd card-maker.git

Then open the HTML file directly in your browser.

On Windows, you can also simply double-click the .html file.

For example:

Dossier.html

The application runs completely client-side.

Creating a Character
1. Core

Enter the character's:

Name
Description
Scenario
First message
Alternate greetings

The Description is the primary character description stored in the card.

2. Voice & Behavior

Configure:

Personality
Example messages
System prompt
Post-history instructions

Example message format:

<START>
{{user}}: Hello.
{{char}}: Hello there.

These examples can help define the character's speaking style and behavior.

3. Add a Portrait

Click or drag an image into the Portrait area.

The application converts the uploaded image to PNG internally and scales very large images so the maximum dimension is 1024 pixels.

4. Lorebook

Lorebook entries can contain:

Entry name
Trigger keys
Content

Example:

Entry name:
The Harbor District

Trigger keys:
harbor, docks, port

Content:
The Harbor District is the oldest commercial area of the city...

Lorebook information is stored inside the card's character_book structure.

5. Metadata

Optional metadata includes:

Creator
Character version
Tags
Creator notes

Example tags:

original, fantasy, companion
Exporting Cards

Dossier supports two export formats.

Character Card JSON

Click:

Download card JSON

The generated file follows the Character Card v2 structure:

{
  "spec": "chara_card_v2",
  "spec_version": "2.0",
  "data": {}
}

The exported filename is based on the character name:

character-name.card.json
Character Card PNG

Click:

Download card PNG

The application takes the uploaded portrait and embeds the Character Card JSON inside the PNG.

The exported filename looks like:

character-name.card.png

If no portrait is supplied, Dossier automatically creates a placeholder image.

How PNG Card Data Is Stored

Character Card data is stored inside a PNG tEXt chunk using the keyword:

chara

The card data is:

Serialized to JSON
UTF-8 encoded
Base64 encoded
Written into the PNG chara metadata chunk

When an existing card is imported, Dossier scans the PNG for a tEXt or iTXt chunk named chara, extracts the Base64 data, and reconstructs the card JSON.

Existing chara metadata is removed before new card data is inserted so duplicate card metadata does not accumulate.

Loading an Existing Card

Open the Export tab.

Drag or select either:

.card.png

or:

.card.json

Dossier will populate the editor with the card's existing fields.

You can then modify the character and export a new copy.

Imported PNG cards also restore the card image into the preview.

Character Card Fields

Dossier currently supports fields including:

name
description
personality
first_mes
avatar
mes_example
scenario
creator_notes
system_prompt
post_history_instructions
alternate_greetings
tags
creator
character_version
extensions
character_book

The exported wrapper uses:

spec: chara_card_v2
spec_version: 2.0
Lorebook Structure

Lorebook entries are exported with properties such as:

{
  "name": "The Harbor District",
  "keys": [
    "harbor",
    "docks"
  ],
  "secondary_keys": [],
  "content": "Lorebook content goes here.",
  "enabled": true,
  "insertion_order": 10,
  "case_sensitive": false,
  "priority": 10,
  "selective": false,
  "constant": false,
  "probability": 100
}

Lorebook entries are included under:

data.character_book.entries
Project Structure

The application can run as a single HTML file:

project/
├── Dossier.html
└── README.md

The HTML file contains:

HTML interface
CSS styling
JavaScript application logic
PNG parsing
CRC32 calculation
PNG metadata embedding
Character Card JSON generation
Import/export functionality

No external JavaScript dependencies are required.

The interface loads Google Fonts when an internet connection is available.

Privacy

Character information and uploaded images are processed directly in the browser.

Dossier does not require a backend server and does not intentionally upload character data to an application server.

The stylesheet does import fonts from Google Fonts.

Development

Because the application is written with plain HTML, CSS, and JavaScript, you can modify it with any code editor.

Examples:

Visual Studio Code
Cursor
Sublime Text
Notepad++
Vim

After making a change, save the file and refresh the browser.

Updating the GitHub Repository

After modifying the application or README:

git status
git add -A
git commit -m "Update Dossier character card maker"
git push
Known Limitations
The application is currently a single-page browser application.
Character data is stored locally only while the page is open unless exported.
The browser must support the File API, Canvas API, Blob API, and typed arrays.
PNG card importing depends on compatible chara metadata being present.
Very large portrait images are resized before export.
Future Ideas

Possible additions include:

Character Card validation
Autosave with browser local storage
Dark mode
Additional Character Card specification support
Lorebook import/export
Character search and library management
Multiple portrait support
Character templates
Drag-and-drop JSON validation
PNG metadata inspector
Card compatibility testing
Optional desktop packaging
License: MIT License

If you publish the project publicly, consider adding a LICENSE file to the repository.

About

Dossier is a simple browser-based tool for building Character Card v2 compatible characters without requiring a backend or installation
