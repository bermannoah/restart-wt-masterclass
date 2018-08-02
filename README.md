# Restart Network x WeTransfer Masterclass

### Table of Contents
**[1. Who am I?](#who-am-i)**<br>
**[2. Who are we?](#who-are-we)**<br>
**[3. Who are you?](#who-are-you)**<br>
**[4. What is the WeTransfer API?](#what-is-the-wetransfer-api)**<br>

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

## Files as "text"

Another thing that MPP involves is thinking of files in a way we might not be used to. Usually when we interact with a file that isn't _obviously_ text we tend to think of it as just a blob containing data 

## SDKs
 
- JS, PHP, Ruby, Swift, C#, R - feel free to play with any of them

## What kind of projects would you make with this?

One thing you can do is to integrate a WeTransfer upload into an existing project or site. But we think there are loads of different ways you can use the API. See some of our ideas by going to https://developers.wetransfer.com.

