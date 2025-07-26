# content-cache.ts.adligo.org
This will be a content server designed for highly available caching of web content. 

## Overview
It will be designed to facilitate pull, cache as a proxy, or have content pushed into it to allow the content to live in a variety of locations, including AEM, Git, and other content repositories.

## Architecture 
A modular architecture will provide a wide range of Use-Cases, including hosting on different clouds.   

#### Basic Cache
Although this server will be able to be used as a basic cache, as follows, this is NOT the primary Use-Case!

```
     ┌───────────┐          ┌─────────┐          ┌─────────────┐          ┌───┐
     │CacheServer│          │LocalDisk│          │ContentClient│          │AEM│
     └─────┬─────┘          └────┬────┘          └──────┬──────┘          └─┬─┘
           │     LoadConfig      │                      │                   │  
           │────────────────────>│                      │                   │  
           │                     │                      │                   │  
           │                 GetFileA                   │                   │  
           │<───────────────────────────────────────────│                   │  
           │                     │                      │                   │  
           │                     │     GetFileA         │                   │  
           │───────────────────────────────────────────────────────────────>│  
           │                     │                      │                   │  
           │               ProvideFileA                 │                   │  
           │───────────────────────────────────────────>│                   │  
           │                     │                      │                   │  
           │     StoreFileA      │                      │                   │  
           │────────────────────>│                      │                   │  
     ┌─────┴─────┐          ┌────┴────┐          ┌──────┴──────┐          ┌─┴─┐
     │CacheServer│          │LocalDisk│          │ContentClient│          │AEM│
     └───────────┘          └─────────┘          └─────────────┘          └───┘
```

#### Curated Cache
The primary use case of the Content Cache Server will be to host content after it's curated as follows;

```
     ┌──────────────┐           ┌───┐          ┌──────────────┐           ┌───────────┐          ┌─────────┐          ┌─────────────┐
     │ContentCreator│           │AEM│          │ContentCurator│           │CacheServer│          │LocalDisk│          │ContentClient│
     └───────┬──────┘           └─┬─┘          └───────┬──────┘           └─────┬─────┘          └────┬────┘          └──────┬──────┘
             │    CreateFileA     │                    │                        │                     │                      │       
             │───────────────────>│                    │                        │                     │                      │       
             │                    │                    │                        │                     │                      │       
             │                    │     ViewFileA      │                        │                     │                      │       
             │                    │<───────────────────│                        │                     │                      │       
             │                    │                    │                        │                     │                      │       
             │                    │                    │     PublishFileA       │                     │                      │       
             │                    │                    │───────────────────────>│                     │                      │       
             │                    │                    │                        │                     │                      │       
             │                    │                    │                        │     StoreFileA      │                      │       
             │                    │                    │                        │────────────────────>│                      │       
             │                    │                    │                        │                     │                      │       
             │                    │                    │                        │                 GetFileA                   │       
             │                    │                    │                        │<───────────────────────────────────────────│       
             │                    │                    │                        │                     │                      │       
             │                    │                    │                        │               ProvideFileA                 │       
             │                    │                    │                        │───────────────────────────────────────────>│       
     ┌───────┴──────┐           ┌─┴─┐          ┌───────┴──────┐           ┌─────┴─────┐          ┌────┴────┐          ┌──────┴──────┐
     │ContentCreator│           │AEM│          │ContentCurator│           │CacheServer│          │LocalDisk│          │ContentClient│
     └──────────────┘           └───┘          └──────────────┘           └───────────┘          └─────────┘          └─────────────┘
```

## Features
configurable disk and memory caching 
configurable storage (i.e. local, or cloud Azure, AWS, GCP)

## License
Apache 2.0

For questions, support, or feedback, us on Discord https://discord.gg/awPES8wj2p or open an issue on GitHub.
