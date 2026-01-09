# GPT Crawler

Crawl a site to generate knowledge files to create your own custom GPT from one or multiple URLs


## Example

[Here is a custom GPT](https://chat.openai.com/g/g-kywiqipmR-builder-io-assistant) that I quickly made to help answer questions about how to use and integrate [Builder.io](https://www.builder.io) by simply providing the URL to the Builder docs. 

This project crawled the docs and generated the file that I uploaded as the basis for the custom GPT.

[Try it out yourself](https://chat.openai.com/g/g-kywiqipmR-builder-io-assistant) by asking questions about how to integrate Builder.io into a site. 

> Note that you may need a paid ChatGPT plan to access this feature

## Get started

### Prerequisites

Be sure you have Node.js >= 16 installed

### Clone the repo

```sh
git clone https://github.com/Abhishek-yadav04/crowler.gpt
```

### Install Dependencies

```sh
npm i
```

If you do not have Playwright installed:
```sh
npx playwright install
```

### Configure the crawler

Open [config.ts](config.ts) and edit the `url` and `selectors` properties to match your needs.

E.g. to crawl the Builder.io docs to make our custom GPT you can use:

```ts
export const config: Config = {
  url: "https://www.builder.io/c/docs/developers",
  match: "https://www.builder.io/c/docs/**",
  selector: `.docs-builder-container`,
  maxPagesToCrawl: 50,
  outputFileName: "output.json",
};
```

See the top of the file for the type definition for what you can configure:

```ts
type Config = {
  /** URL to start the crawl */
  url: string;
  /** Pattern to match against for links on a page to subsequently crawl */
  match: string;
  /** Selector to grab the inner text from */
  selector: string;
  /** Don't crawl more than this many pages */
  maxPagesToCrawl: number;
  /** File name for the finished data */
  outputFileName: string;
  /** Optional function to run for each page found */
  onVisitPage?: (options: {
    page: Page;
    pushData: (data: any) => Promise<void>;
  }) => Promise<void>;
    /** Optional timeout for waiting for a selector to appear */
    waitForSelectorTimeout?: number;
};
```

### Run your crawler

```sh
npm start
```

### Upload your data to OpenAI

The crawl will generate a file called `output.json` at the root of this project. Upload that [to OpenAI](https://platform.openai.com/docs/assistants/overview) to create your custom assistant or custom GPT.

#### Create a custom GPT

Use this option for UI access to your generated knowledge that you can easily share with others

> Note: you may need a paid ChatGPT plan to create and use custom GPTs right now

1. Go to [https://chat.openai.com/](https://chat.openai.com/)
2. Click your name in the bottom left corner
3. Choose "My GPTs" in the menu
4. Choose "Create a GPT"
5. Choose "Configure"
6. Under "Knowledge" choose "Upload a file" and upload the file you generated


#### Create a custom assistant

Use this option for API access to your generated knowledge that you can integrate into your product.

1. Go to [https://platform.openai.com/assistants](https://platform.openai.com/assistants)
2. Click "+ Create"
3. Choose "upload" and upload the file you generated



## Contributing

Know how to make this project better? Send a PR!

## 👨‍💻 Author

<p align="center">
  <img src="https://github.com/Abhishek-yadav04.png" width="100px" style="border-radius: 50%;" alt="Abhishek Yadav" />
</p>

<p align="center">
  <b>Abhishek Yadav</b><br>
  Computer Science Student
</p>

<p align="center">
  <a href="https://github.com/Abhishek-yadav04">
    <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github" alt="GitHub" />
  </a>
</p>

---

<p align="center">
  <b>⭐ Star this repo if you find it helpful!</b>
</p>

<p align="center">
  Made with ❤️ by Abhishek Yadav
</p>
