---
title: 'host your own llm'
description: 'Setup ollama, to be usable over the internet'
date: 2024-04-07T15:15:50+03:00
draft: true
type: "post"
tags: ["ai", "ollama", "self-host", "large language models", "LLMs"]
---

## Intro
If you don't already know what [ollama](https://ollama.com) is, I don't know which rock you've been living under.
Basically its a simplified way of getting up and running with large language modals(**LLMs**) locally,
giving you ChatGPT like capabilities right on your very own device.

We are going to give you this same capabilities but, on a virtual private server(**vps**) like digitalocean, hetzner or linode;
allowing you to have them on demand over the internet.
> I am going to use digitalocean as its what I have available.

After you've already setup your server on digital ocean.

> [!NOTE]
>
>  Ollama recommends that you should have at least 8 GB of RAM to run the 3B models, 16 GB to run the 7B models, and 32 GB to run the 13B models.

ssh into your server and install [ollama](https://ollama.com/download).
For this tutorial, we'll use the neural-chat model, its lightweight and can run in machines with less than 8gigs.

Download it using `ollama pull neural-chat` and run it using `ollama run neural-chat`.

That's it, you have your own instance of an llm on your machine.
But we don't want it be available on our machine only right, we want to use it on our phones like ChatGPT.

<!-- TODO:: Continue -->



