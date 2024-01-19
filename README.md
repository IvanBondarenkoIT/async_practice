# async_practice

https://docs.aiohttp.org/en/stable/index.html

Welcome to AIOHTTP
Asynchronous HTTP Client/Server for asyncio and Python.

Current version is 3.9.1.

Key Features
Supports both Client and HTTP Server.

Supports both Server WebSockets and Client WebSockets out-of-the-box without the Callback Hell.

Web-server has Middlewares, Signals and pluggable routing.

Library Installation
$ pip install aiohttp
For speeding up DNS resolving by client API you may install aiodns as well. This option is highly recommended:

$ pip install aiodns
Installing all speedups in one command
The following will get you aiohttp along with aiodns and Brotli in one bundle. No need to type separate commands anymore!

$ pip install aiohttp[speedups]
Getting Started
Client example
import aiohttp
import asyncio

async def main():

    async with aiohttp.ClientSession() as session:
        async with session.get('http://python.org') as response:

            print("Status:", response.status)
            print("Content-type:", response.headers['content-type'])

            html = await response.text()
            print("Body:", html[:15], "...")

asyncio.run(main())
This prints:

Status: 200
Content-type: text/html; charset=utf-8
Body: <!doctype html> ...
Coming from requests ? Read why we need so many lines.

Server example:
from aiohttp import web

async def handle(request):
    name = request.match_info.get('name', "Anonymous")
    text = "Hello, " + name
    return web.Response(text=text)

app = web.Application()
app.add_routes([web.get('/', handle),
                web.get('/{name}', handle)])

if __name__ == '__main__':
    web.run_app(app)
For more information please visit Client and Server pages.

Development mode
When writing your code, we recommend enabling Python’s development mode (python -X dev). In addition to the extra features enabled for asyncio, aiohttp will:

Use a strict parser in the client code (which can help detect malformed responses from a server).

Enable some additional checks (resulting in warnings in certain situations).

What’s new in aiohttp 3?
Go to What’s new in aiohttp 3.0 page for aiohttp 3.0 major release changes.

Tutorial
Polls tutorial

Source code
The project is hosted on GitHub

Please feel free to file an issue on the bug tracker if you have found a bug or have some suggestion in order to improve the library.

Dependencies
async_timeout

attrs

multidict

yarl

Optional aiodns for fast DNS resolving. The library is highly recommended.

$ pip install aiodns
Optional Brotli or brotlicffi for brotli (RFC 7932) client compression support.

$ pip install Brotli
Communication channels
aio-libs Discussions: https://github.com/aio-libs/aiohttp/discussions

Feel free to post your questions and ideas here.

gitter chat https://gitter.im/aio-libs/Lobby

We support Stack Overflow. Please add aiohttp tag to your question there.

Contributing
Please read the instructions for contributors before making a Pull Request.

Authors and License
The aiohttp package is written mostly by Nikolay Kim and Andrew Svetlov.

It’s Apache 2 licensed and freely available.

Feel free to improve this package and send a pull request to GitHub.

Policy for Backward Incompatible Changes
aiohttp keeps backward compatibility.

After deprecating some Public API (method, class, function argument, etc.) the library guaranties the usage of deprecated API is still allowed at least for a year and half after publishing new release with deprecation.

All deprecations are reflected in documentation and raises DeprecationWarning.

Sometimes we are forced to break the own rule for sake of very strong reason. Most likely the reason is a critical bug which cannot be solved without major API change, but we are working hard for keeping these changes as rare as possible.
