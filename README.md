<div align="center"><h1>🧠 Mnemonikus 🏰</h1></div>

<br>
<div align="center">
  <img/ src="https://github.com/user-attachments/assets/2ca621b7-7002-4004-8d39-c14958c7d741" height="25">&nbsp;&nbsp;
  <img/ src="https://github.com/user-attachments/assets/3cd1ab55-deda-4cdd-a21e-951d91bf3231" height="25">&nbsp;&nbsp;
  <img/ src="https://github.com/user-attachments/assets/1c6b002f-cfbb-4564-b4a2-563563de1735" height="25">&nbsp;&nbsp;
  <img/ src="https://github.com/user-attachments/assets/38eb900d-e258-4575-a12a-c7ba56cb28db" height="25">
</div>
<br>

Mnemonikus is a web application that generates memory palaces tour to help users memorize complex information. It uses Claude to generate the tour and Dalle3 to fill in the images.

## Table of Contents

1. [Features](#features)
2. [Technical Overview](#technical-overview)
3. [Setup and Usage](#setup-and-usage)
4. [Configuration](#configuration)
5. [API Integration](#api-integration)
6. [User Interface](#user-interface)
7. [Image Generation](#image-generation)
8. [Text-to-Speech](#text-to-speech)
9. [Styling](#styling)
10. [Security Considerations](#security-considerations)
11. [Future Improvements](#future-improvements)

## Features

- generates a mind palace tour guide and audio narration.
- advance settings ui.
- download tour guide as pdf.
- download tour narration as mp3.
- use your own api, no middle-man fees.
- compactness, the app is an html file that runs everything client-side.

## Technical Overview

Mnemonikus is a single-page web application built with HTML, CSS, and JavaScript. It integrates with two main AI services:

1. Anthropic's Claude API for text generation
2. OpenAI's DALL-E API for image generation and TTS for the tour narration

## Setup and Usage

1. Clone the repository or download the HTML file.
2. Open the HTML file in a web browser.
3. Enter your Anthropic and OpenAI API keys in the settings.
4. Input the information you want to memorize in the text area.
5. Click "Generate" to create your memory palace.

## Configuration

Users can configure various settings:

- Anthropic API Key
- OpenAI API Key
- Anthropic Model
- Max Tokens - max length of text generated
- Temperature - creativity from 0.0 to 1.0
- Custom Prompt
- OpenAI Image Model
- Image Resolution:

| resultions | Dalle3 | Dalle2 |
|------------|--------|--------|
| 1792x1024  | ✅      |        |
| 1024x1792  | ✅      |        |
| 1024x1024  | ✅      | ✅      |
| 512x512    |        | ✅      |
| 256x256    |        | ✅      |

- TTS Model - tts-1 is faster and cheaper, tts-1-hd produces higher quality.

These settings are stored in the browser's local storage for persistence.

## API Integration

### Anthropic API

The application uses the Anthropic API to generate the memory palace text. It sends a prompt containing the user's input and receives a structured response describing the memory palace.

### OpenAI API

The OpenAI API is used for two purposes:
1. Generating images based on the descriptions provided by the Anthropic API.
2. Converting the narration text to speech.

## User Interface

The UI consists of:

- A text input area for the user's information
- A settings panel (toggled by a gear icon)
- A "Generate" button
- A results area displaying the generated memory palace, images, and narration

## Image Generation

Images are generated for each major element of the memory palace. Users can:

- View the generated images
- Copy the image generation prompts
- Regenerate images if desired

## Text-to-Speech

The application provides text-to-speech functionality for the narration, allowing users to listen to a description of their memory palace.

## Styling

The application uses custom CSS for styling, with a responsive design that adapts to different screen sizes. It employs a clean, modern aesthetic with subtle animations for user interactions.

## Security Considerations

- API keys are stored in the browser's local storage, which is not secure for production environments.
- The application uses the `dangerouslyAllowBrowser: true` option for the Anthropic client, which is not recommended for production use.

## Future Improvements

Potential areas for enhancement include:

1. Server-side API key management for improved security
2. User accounts and saved memory palaces
3. More customization options for the memory palace generation
4. Integration with spaced repetition systems for effective memorization
5. Accessibility improvements
6. Performance optimizations for faster generation and loading
