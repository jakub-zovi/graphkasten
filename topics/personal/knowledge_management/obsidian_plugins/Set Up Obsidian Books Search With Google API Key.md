---
tags:
  - personal
  - personal/pkm
created: 2026-05-09T22:02
modified: 2026-05-12T15:58
published: 2024-10-15
sources:
  - "[Set Up Obsidian Books Search With Google API Key](https://www.zylstra.org/blog/2024/10/set-up-obsidian-books-search-with-google-api-key/)"
topics:
  - Obsidian
  - Book Search Plugin
  - Google Books API
authors:
  - "[[Ton Zijlstra]]"
ai-assisted: true
hidden:
public: true
clipping: true
human-review: true
---
I am trying out the [Books Search plugin for Obsidian](https://github.com/anpigon/obsidian-book-search-plugin). I keep notes on all books I’ve read, own or have come across. I add meta data to those notes manually. The Books Search plugin helps make that easier by picking up that meta data from Google Books through their API. You install the plugin through the Community Plugin list, and can then add an API key. Without that key, after a few tries you will get an error message.

The plugin documentation does however not state how to connect the plugin to that Google API.

These are the steps I took after a bit of searching:

- In the [Google cloud console](https://console.cloud.google.com/) first create a project. (A Google account is needed)
- In the same console, under credentials, click create credentials and create an API key. Copy that key and save it in the settings of the Obsidian Books Search plugin.
- In the same console, under Enable APIs & Services, enable the Google Books API.
- Go back to Credentials, edit your API key, select Restrict Key under API restrictions, and select from drop down list the Google Books API you’ve just enabled. (If it doesn’t show any APIs to choose, you have not enabled any APIs yet.) Now the key works only for the Google Books API.
- Ignore the warning in the console about OAuth consent, as this is not needed (the books API is accessible without authorisation, and you’re also not building an app for others to use.)

Using the Book Search plugin I notice it is by default restricted to English books, not finding titles in other languages that Google Books does have in its lists. The locale settings in the plugin allow me to switch language before a search in the search form through a very long drop down menu, but doing that (or doing the same search for each of three or four languages) quickly negates the effectivity gain the plugin provides.

It is unclear from the [Google API documentation if locale can be set to multiple languages](https://developers.google.com/books/docs/v1/using#langRestrict).

Probably not, given Google’s long history of interpreting multilingual as serial monolingual (see this

[2007 presentation at Google by Stephanie Booth](https://www.youtube.com/watch?v=rqJdEMeyXZc)

pointing this same stuff out), ignoring that multilingual people tend to change languages throughout their activities even for just a single word or short phrase. (I don’t have Dutch, English or German days or topics, in the case of books I may want to find the German original of an English translation, or want to search for a specific thing in French because I know it exists, while also interested in any Dutch translation that might be available or the Italian original. My notes are always in multiple languages.)

## ChatGPT Note
You’re very close — the issue is that the tutorial is slightly outdated relative to the current Google Cloud UI.

What’s happening is:

* You created an API key successfully.
* You are now in the **API restrictions** dropdown.
* But **Google Books API is not enabled yet** for your project, so it does not appear in the list.

Google only shows APIs in that dropdown after they’ve been enabled for the project. ([Google for Developers][1])

Do this first:

1. Open:
   * [https://console.cloud.google.com/apis/library](https://console.cloud.google.com/apis/library)

2. Make sure the correct project is selected at the top.

3. Search for:
   * **Books API**
   * or **Google Books API**

1. Open it and click:
   * **Enable**

After enabling it:
5. Go back to:
   * APIs & Services → Credentials → your API key

5. Under:
   * **API restrictions**
   * choose:
     * “Restrict key”

5. Now you should see:
   * **Books API**
   * or **Google Books API**
     in the selectable list.

Then save.

A few additional notes:

* The API is sometimes listed simply as **Books API** instead of “Google Books API”.
* It can take ~30–60 seconds after enabling before it appears in restrictions.
* If it still doesn’t show up, refresh the page completely.

The plugin in Obsidian usually only needs:

* a normal API key
* no OAuth setup
* Books API enabled

You can test the key quickly in your browser with:

```text
https://www.googleapis.com/books/v1/volumes?q=isbn:9780262046305&key=YOUR_API_KEY
```

If you get JSON back, the key works. ([Google for Developers][1])

[1]: https://developers.google.com/books/docs/v1/using?utm_source=chatgpt.com "Using the API | Google Books APIs | Google for Developers"
