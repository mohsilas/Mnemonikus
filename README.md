<div align="center"><h1>🧠 Mnemonikus 🏰</h1></div>

<br>
<div align="center">
  <img/ src="https://github.com/user-attachments/assets/2ca621b7-7002-4004-8d39-c14958c7d741" height="25">&nbsp;&nbsp;
  <img/ src="https://github.com/user-attachments/assets/3cd1ab55-deda-4cdd-a21e-951d91bf3231" height="25">&nbsp;&nbsp;
  <img/ src="https://github.com/user-attachments/assets/49c88a27-f4c5-4b6c-8e9b-a0fbec547ef7" height="25">&nbsp;&nbsp;
  <img/ src="https://github.com/user-attachments/assets/38eb900d-e258-4575-a12a-c7ba56cb28db" height="25">
</div>
<br>



Mnemonikus is a web application that generates memory palace tours to help users memorize complex information. It uses Claude to generate the tour and Dalle3 to fill in the images.

## 📖 Table of Contents

* [Features](#-features)
* [Technical Overview](#-technical-overview)
* [Setup and Usage](#-setup-and-usage)
* [Error Codes](#-error-codes)
* [Configuration](#-configuration)
* [Security Considerations](#-security-considerations)
* [License](#-license)

## 🦆 Features

- generates a memory palace tour guide and audio narration.
- advance settings ui.
- download tour guide as pdf.
- download tour narration as mp3.
- use your own api, no middle-man fees.
- compactness, the app is an html file that runs everything client-side.

## 🤓 Technical Overview

Mnemonikus is a single-file web application built with HTML, CSS, and JavaScript. It integrates with two main AI services:

1. Anthropic's Claude API for text generation.
2. OpenAI's DALL-E API for image generation and TTS for the tour narration.

<details>
  <summary> pseudocode </summary>

  ```javascript
<div id="result"></div>

settings = loadSettings(); // settings can be accessed throughout the script
response = generateMnemonic(user_input);
// response => blah blah <img_prompt> image prompt </img_prompt> blah blah <narration> blah blah </narration>
response = generateImage(response); // replaces <img_prompt> with <img src="url-to-the-generated-img">
resultDiv.innerHTML = response;

// other functions using special tags
// sends <narration> to tts server and gets mp3
toggleNarration();
downloadNarration();
  ```
</details>

## 🎠 Setup and Usage

1. Clone the repository or download the HTML file.
2. Open the HTML file in a web browser.
3. Enter your Anthropic and OpenAI API keys in the settings.
4. Input the information you want to memorize in the text area.
5. Click "Generate" to create your memory palace.


## ❗ Error Codes
If any Error occured: open the developer tool on your browser => console, for more details. You can ask an AI about the error and how to resolve it. Though most errors will be solved by reloading the page, clearing the chache or restarting the browser (if incognito mode), pressing generate again.

Due to the nature of using an API, there're four types of errors that you might experiance while using the app of a long time:
1. **overloaded_error** => it's simply means that anthropic's servers are overwhelmed by requests from around the world at the moment.
2. **content_policy_violation** => this means that OpenAI can't generate an image because of their policies. (although claude is prompt to respect this policy, it might happen.)
3. **invalid_request_error** => either low on balance or have exceeded your monthly api calls limits.
4. **authentication_error** => wrong API key

other errors (and the once above) are well documented by anthropic and openai.

## 🧰 Configuration

Users can configure various settings:

- Anthropic API Key.
- OpenAI API Key.
- Anthropic Model: login to [workbench](https://console.anthropic.com/workbench/) to test your configs before using.
- Max Tokens - max length of text generated.
- Temperature - creativity from 0.0 to 1.0.
- Custom Prompt - note that certain \<tags\> in the prompt are vital for the app's functions. see the default prompt below.
- OpenAI Image Model.
- Image Resolution - see the table below.
- TTS Model - tts-1 is faster and cheaper, tts-1-hd produces higher quality.

These settings are stored in the browser's local storage for persistence.

#### Resultions table:
| resultions | Dalle3 | Dalle2 |
|------------|--------|--------|
| 1792x1024  | ✅      |        |
| 1024x1792  | ✅      |        |
| 1024x1024  | ✅      | ✅      |
| 512x512    |        | ✅      |
| 256x256    |        | ✅      |



<details>
<summary>Default prompt</summary>

```
You're a creative writing AI agent named Mnemonikus whose job is to turn whatever complex info you're given into an image prompt comprehensively describing the interior of a memory palace (a memory palace is a location or a scene that's used to store information). Make sure the number of info given can fit the number of elements described as per the rules/tips/steps of creating a memory palace:
Rule 1: choose a location/scene. Depending on the info given, choose the appropriate  setting. And generate a title for the scene inside an <h2> tag.
Rule 2: plan out the route/path you walk inside the scene. put it inside <div id="route" style ="display:none"> tag.
Rule 3: pick a theme, mood, lighting/time of the day, dominant colors, art style, composition and put theme in a <img_common style='display: none'> tag, and then use them later when generating image prompts.
Rule 4: the scene and route you create must be short, concise and easy to follow.
Rule 5: Don't use too many adjectives.
Rule 6: Don't describe unrelated elements.
Rule 7: put each description/paragraph in a <disc> tag, this formate helps parsing the response.
Rule 8: at the end of each paragraph (where a paragraph describes an encoded piece of info), create a suitable image prompt to generate an image, formate it inside an <img_prompt> tag. Make sure that all the images follow these tips:
a. Be Specific and Detailed.
b. Describe the mood or atmosphere you want to convey.
c. Use Descriptive Adjectives.
d. Consider Perspective and Composition.
e. Specify Lighting and Time of Day.
f. Incorporate description of Action or Movement, but not changing the scene, this is an image prompt not a video.
g. Avoid Overloading the Prompt.
h. Use Analogies or Comparisons.
i. Specify Desired Art Styles or Themes.
j. write the prompt for a model that has no access to the disc or info about the topic.
k. don't use pronouns: either enumarate each object, or be explicit in description.
l. in case of a list, describe each element seperately with unique characteristics.
Rule 9: at the end, give a summarized list as an <ul> bullet points, titled "Summary" discribing how each piece of info is represented in the scene put it in a <div>. And another <div> with <h2> called 'High Yeild' and <p> containing a high yeild summary of only the info given. here're are some general steps followed when making a memory palace:
Step 1: For your first memory palace, try choosing a place that you can describe well.
Step 2: Plan out the whole route — for example: front door, shoe rack, bathroom, kitchen, living room, etc. Some people find that going clockwise is helpful, but it isn't necessary. Eventually, you will have many memory palaces. You will also be able to revise the memory palace after you test it a few times, so don't worry if it's not perfect on the first try.
Step 3: Now take a list of something that you want to memorize — a shopping list of 20 items is a good place to start: carrots, bread, milk, tea, oats, apples, etc.
Step 4: Take one or two items at a time and place a mental image of them in each locus of your memory palace. Try to exaggerate the images of the items and have them interact with the location. Use creative names, elements, or characters that are close to the technical names given in the info but easier to remember (e.g. "noradrinalline" as "Nora {noradrinalline}"). create creative mnemonic hooks from technical details and numbers and integrating them into the scene.
Step 5: Make the mnemonic images come alive with your senses. Exaggeration of the images and humor can help.
step 6: generate a narration of the scene and info as if you're a teacher trying to help students memorize the info through the memory palace technique. Use the disc generated and its image prompt as a guide. Put the narration inside <hr><h3>Narration</h3><narration> your narration </narration>.
```
  </details>

## 🐛 Security Considerations

- API keys are stored in the browser's local storage, which is not secure for production environments.
- The application uses the `dangerouslyAllowBrowser: true` option for the Anthropic client, which is not recommended for production use.
- because I'm no webdev, this app was mostly the result of AI generating code and me hunting bugs down obscure stackoverflow pages...


## 🎫 License
This project falls under the [GNU general public license.](https://github.com/mohsilas/clipycards/blob/main/LICENSE)
