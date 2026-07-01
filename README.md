# ✨ all the llm skills i've loved before 💖

## 🎶 How to use this repo 🎵

This repo is designed so that it can be cloned or symlinked as the skills directory of an agent of choice. I use opencode, so I keep this repo cloned in a working directory called "skills" and I symlink skills into the opencode config directory (e.g. .config/opencode/). You could also just clone the repo into the config directory as skills/. 

## The skills ☁️🌈

### grill-me 💭

Taken from the very famous and viral eight-liner of genius thanks to [Matt Pocock](https://www.aihero.dev/my-grill-me-skill-has-gone-viral) 💌 

Deceptive in its simplicity and diabolical in its detail.

I adapted this very slightly, so it's clear how to use it for various purposes, including document review, for which it works very well. 

Also, since LLMs tend to comply with the "one question at a time" directive for the first several questions and then try to start sneaking in multi-part questions, this version adds a polite reminder to limit the inquiry to "one" question at a time. 

### playwright-cli 🪩 

From the official [playwright-cli GitHub repo](https://github.com/microsoft/playwright-cli) 🌺

I added a one-liner to clarify that the cli is already installed, so LLMs won't try to install local copies or try to install it some other way and/or mess things up in other creative ways.

For e2e testing I like LLMs to use playwright via the cli.

### prd 📝

This is based on the skill of the same name in [Ryan Carson's git repo](https://github.com/snarktank/ralph), itself inspired by the works of [loop guru Geoffrey Huntley](https://ghuntley.com/ralph/) 🦘🌟

I've updated it for my workflow in several ways.

This version can either use a detailed spec that is already written, or it can invoke the grill-me skill (above) to create one before proceeding to create the prd.  

It also adds the concept of a [Spike](https://en.wikipedia.org/wiki/Spike_(software_development)), which is used in various agile methodologies. Many times you want to do some technical research before proceeding with development. That research serves to answer open questions in the user stories. 

Anyhow, LLMs know what a Spike is, so this gives them the latitude to include Spikes in the prd. When your Ralph is looping, it will know to start by completing the Spikes and documenting or filling in missing information and making necessary decisions before applying those to the user stories. 

My version of the skill is also more intentional about unit testing, building automated tests, and using the playwright-cli skill (above) for any browser-based testing that's needed. This helps ensure that LLM agents know they should be creating tests and validating them before a story is "done". The software development philosophy I have always followed is that the work is not done until it is tested, which includes automated tests that can be run to catch regressions. 
  
