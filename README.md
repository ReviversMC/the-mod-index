# The Mod Index

Which mod index? What?

The Mod Index plans to be a source where anyone can refer to for Minecraft mods. Get mod metadata, download links, and more.  
The index does **NOT** host or redistribute mod files (e.g. jars), but instead provides links/information to the mod files.

![Competing standards meme](./assets/competingStandards.png)

## Difference between the-mod-index and other sources

|                              | the-mod-index                                                                                                                    | Modrinth                                                | CurseForge                                              |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------|
| Purpose                      | Provide mod information from multiple platforms                                                                                  | Mod downloading site                                    | Mod downloading site                                    |
| Mod availability             | Modrinth, CurseForge, and user submitted mods. Files from Modrinth, Curse, GitHub and others. Not reliant on any single platform | Modrinth mods only                                      | CurseForge mods only                                    |
| API usability                | Direct read only access to index/manifests                                                                                       | Open source REST api                                    | Closed source REST api                                  |
| Reliability                  | Manifests hosted on GitHub, entire index and tools are forkable                                                                  | UNKNOWN, Backend is open source and forkable            | UNKNOWN                                                 |
| Mod updates reflected by API | Delayed                                                                                                                          | Immediate                                               | Immediate                                               |
| Relative creation date       | New                                                                                                                              | Established                                             | Established                                             |
| List available mods          | Supported. One call to get them all                                                                                              | Supported, with filters. Multiple calls to get them all | Supported, with filters. Multiple calls to get them all |
| Search for mod by identifier | Supported, the-mod-index identifier                                                                                              | Supported, Modrinth project id                          | Supported, CurseForge project id                        |
| Search by mod hash           | Supported, sha512 (hex)                                                                                                          | Supported, sha1 (hex) or sha512 (hex)                   | Unsupported. Use fingerprint system instead             |
| Relative release cycle       | Fast                                                                                                                             | Moderate                                                | Moderate                                                |

## How it works
the-mod-index is an open source, forkable, community driven index, wanting to simplify obtaining mod metadata and files. We do this by:

- Having tools such as [the-mod-index creator](https://github.com/reviversmc/the-mod-index-creator) to regularly update the index
- Validating all index entries to be valid using [the-mod-index validator](https://github.com/reviversmc/the-mod-index-validation)
- Accepting entries for mods that are not hosted on Modrinth or CurseForge (TODO)
- Hosting all files on a reliable, transparent server (GitHub)

Meta data we serve includes:

- Author
- Description
- Download link
- SHA 512 File hash (only when a download link is found for the hash)
- Modrinth and/or CurseForge ids
- Source control link, if available
- Contact links, if available
- Much, much more!

We use an identifier for all mods indexed, in the format "modLoader:modName:fileHash", and files are stored in the format "/modLoader/modName", where all identifiers are lowercase.
Only mods with at least 1 file hash will be indexed, and file hashes will only be stored if there is at least one download link available

TODO: Notice about obtaining CurseForge files

## Requesting data
Take a look around, you can view schemas or just view a random mod's manifest for reference.

There is no server interpreting your http calls - what you see is what you get.  
Request for the raw of the index/manifests, and you shall receive the raw of the index/manifests.

Base URL: https://raw.githubusercontent.com/ReviversMC/the-mod-index/{BRANCH}/mods/index.json, where {BRANCH} is the name of the branch. For example, branch v3, which corresponds to version 3 of the index.  
You are advised to always use the "default" branch where possible, as that will be the version actively supported.

> Versioning notice: the-mod-index follows semantic versioning. A new branch will only be created on major version changes, and major version changes **WILL** break backwards compatibility.  
> When minor or patch version changes are made, the branch will be updated to the new version. This allows for you to use the additional info added in a minor or patch version, but still maintains backwards compatibility with the major version.
> 
> As such, we strongly discourage you from using "HEAD" as your branch, as compatibility will break when we push a major update.
---
GET /mods/index.json   
Response: 
- 200 (success): [Index Schema](/schema/indexSchema.json)  
- 404 (not found): The index file does not exist.
---
GET /mods/{modLoader}/{modName}.json  
Parameters:  
- modLoader: The mod loader of a mod. E.g. for an identifier "bricks:fakemod:fakehash", the modLoader would be "bricks"
- modName: The name of the mod as found in the index. E.g. for an identifier "bricks:fakemod:fakehash", the modLoader would be "fakemod"

Response: 
- 200 (success): [Manifest Schema](/schema/manifestSchema.json)
- 404 (not found): The manifest does not exist.
---

## API for your favourite coding language
Prefer using an API for your (insert coding language here)? I do ;-;  
We have a first party [Kotlin API](https://github.com/reviversmc/the-mod-index-api). If you want to contribute an API for your favourite language, we'd be happy to feature it.

## Community
Want to chat? See ya on Discord

[![Discord chat](https://img.shields.io/badge/chat%20on-discord-7289DA?logo=discord&logoColor=white)](https://discord.gg/6bTGYFppfz)