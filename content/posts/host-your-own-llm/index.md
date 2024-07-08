---
title: 'LLMs locally'
description: 'LLMs on your machine'
summary: 'Install and run large language models locally using Ollama.'
date: 2024-07-08
tags: ["LLMs"]
showTags: true
readTime: true
---

## Intro
If you don't already know what [ollama](https://ollama.com) is, I don't know which rock you've been living under.

Basically its a simplified way of getting up and running with large language modals(**LLMs**) locally,
giving you ChatGPT like capabilities right on your very own device.

We are going to give you this same capabilities but on your machine.
Before we dive in, just a heads up:

> Ollama says you should have at least 8 GB of RAM to run the 3B models, 16 GB for the 7B models, and 32 GB for the 13B big boys.

Just know that bigger numbers need beefier computers.

Follow the instructions on [ollama](https://ollama.com/download) to install it, once installed go ahead and search for a model that fits your needs.

I am going to use the `neural-chat model`, its lightweight and can run in machines with less than 8gigs.

Download it using `ollama pull <neural-chat>` [^1].

`ollama pull` downloads the model from ollama's registry to your machine and stores in the following respective locations

- Linux: `/usr/share/ollama/.ollama/models`
- Windows: `C:\Users\%username%\.ollama\models`
- macOS: `~/.ollama/models`


Run the downloaded model using `ollama run <neural-chat>`.

That's it, you have your own instance of an llm on your machine.

[^1]: you can replace the contents of `<neural-chat>` with your prefered model
