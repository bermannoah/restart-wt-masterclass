# Restart Network x WeTransfer Masterclass

### Table of Contents
**[1. Who am I?](#who-am-i)**<br>
**[2. Who are we?](#who-are-we)**<br>
**[3. Who are you?](#who-are-you)**<br>
**[4. What is the WeTransfer API?](#what-is-the-wetransfer-api)**<br>
**[5. Upload flow](#upload-flow)**<br>
**[6. New (?) concept: Multi Part Put uploads](#new--concept-multi-part-put-uploads)**<br>
**[7. Thinking differently about files](#thinking-differently-about-files)**<br>
**[8. So how do I get started?](#so-how-do-i-get-started)**<br>
**[9. SDKs](#sdks)**<br>
**[10. What kind of projects would you make with this?](#what-kind-of-projects-would-you-make-with-this)**<br>

## Who am I?

- Noah Berman (noah@wetransfer.com)
- other details etc @ https://noahberman.org
- work for https://wetransfer.com as a backend developer
- not a "traditional developer" - photographer/writer/filmmaker/customer service person, then went to https://turing.io

## Who are we?

- WeTransfer is a file sharing service! Looks simple for users, is pretty complex "behind the scenes." 
- Public API team introductions

## Who are you?

- what is your name and what is your favourite sandwich (if you have one)
- if you feel like sharing, what's the thing about programming that you're having a lot of fun with right now?
(Doesn't have to be a big thing, it can be ... you really enjoy naming variables or something.)

## What is the WeTransfer API?

- Gives you access to WeTransfer's upload flow
- Create transfers and send 'em
- Or so much more!

## Upload flow

Okay so what _is_ the WeTransfer upload flow?

- 1. Authorize with the API
- 2. Create an empty transfer. NOTE: You'll get the link you need to view the transfer in this step.
- 3. Send a list of items to the transfer
- 4. Per transfer, request upload urls for parts of each file. They'll be 6MB. More on this in a sec. 
- 5. When all chunks have been uploaded, send a call to the "complete" endpoint. 
- 6. Repeat until all files have been "completed." 

## New (?) concept: Multi Part Put uploads

Often times file upload systems will have you send the entire file all at once. This reduces complexity and makes things less involved for both the people doing the upload and the system handling the upload on the other end.

But: 

- what happens if the connection drops?
- what happens on a slow connection?
- what if something unexpected happens to the file during upload? 

That's where Multi Part Put comes in. At its core, you break a file into smaller chunks and upload those chunks to (in this case) Amazon's S3 storage. They are put back together when all parts have been uploaded (which is why we do the "complete" call) and can then be accessed like a regular file. 

This gives application developers ways of handling connection failures or other pieces of weirdness - if the connection drops out you can retry a single chunk, instead of a whole file. 

## Thinking differently about files

Another thing that MPP involves is thinking of files in a way we might not be used to. Usually when we interact with a file that isn't _obviously_ text we tend to think of it as just a blob containing data -- but it's also a piece of text, too! 

You can use an app like [hex fiend](https://ridiculousfish.com/hexfiend/) (mac) or something like [hex editor pro](https://www.microsoft.com/en-us/p/hex-editor-pro/9wzdncrdq8l3?activetab=pivot:overviewtab) (windows) to view the "text" that makes up a file. When we chop a file up into chunks we're essentially telling our system to read to a particular point in a file, send that text, then read to the next point, read that, send it, and so on. 

When we tell the system that all of the chunks have been uploaded, it combines them back together to get the full 'text', which can then be downloaded and used as expected.

## So how do I get started?

- Go to [developers.wetransfer.com](https://developers.wetransfer.com) and click on the Sign up button. Sign in with your own personal github account. If you don't have one, you will need to create one to use the API.

- Once you've given our app permission and logged in you'll need to create an API key. Click on `Dashboard` then `Create new application`. It requires a name, description and URL are optional. Click `Create`. 

- Huzzah, now you have an API key! 

- Next, go to the [documentation](https://developers.wetransfer.com/documentation) where you can read about how the API works, see a list of SDKs, likely errors, and catch up on our recent changes. 

## SDKs

- We do try to abstract a lot of the above logic away, so all you have to do is plug code we (or others) have written into your program and see what you can make it do. But it's important to understand what's going on behind the scenes, so you can best take advantage of what we offer.

- To make this more or less painless we - and the community - have provided a suite of SDKs (Software Development Kits) to support creating whatever you can imagine.
 
- [Javascript](https://github.com/WeTransfer/wt-js-sdk), [PHP](https://github.com/arkaitzgarro/wetransfer-php-sdk), [Ruby](https://github.com/WeTransfer/wetransfer_ruby_sdk), [Swift](https://github.com/WeTransfer/WeTransfer-Swift-SDK), [C#](https://github.com/Steffens-Bridgemate/WeTransfer-C-wrapper/), [R](https://github.com/tfaber/wetransfeR) - feel free to play with any of them

- You can also create your own (or submit issues and pull requests to the above SDKs)!

## What kind of projects would you make with this?

One thing you can do is to integrate a WeTransfer upload into an existing project or site. But we think there are loads of different ways you can use the API. See some of our ideas by going to the main page on [https://developers.wetransfer.com]. 

We're also here to help you build whatever you can imagine. On a personal note I would like to encourage you to make things that make you laugh or entertain you -- something 'useless' from a business point of view, but tremendously useful from a creativity point of view. I like [Simone Giertz' TED talk](https://www.youtube.com/watch?v=c0bsKc4tiuY) on the subject. What's the most mind-blowingly useless integration you can think of?



