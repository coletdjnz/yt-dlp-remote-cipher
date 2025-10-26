# yt-dlp-remote-cipher

A yt-dlp plugin to solve YouTube JS challenges remotely using a [yt-cipher](https://github.com/kikkia/yt-cipher) server.

<!-- TOC -->
* [yt-dlp-remote-cipher](#yt-dlp-remote-cipher)
    * [Install](#install)
      * [pip/pipx](#pippipx)
      * [Manual install](#manual-install)
    * [Configure](#configure)
      * [Server URL](#server-url)
      * [API Key](#api-key)
      * [Other options](#other-options)
    * [Development](#development)
<!-- TOC -->

### Install

**Requires yt-dlp `2025.XX.XX` or above.**

If yt-dlp is installed through `pip` or `pipx`, you can install the plugin with the following:

#### pip/pipx

```
pipx inject yt-dlp yt-dlp-remote-cipher
```
or

```
python3 -m pip install -U yt-dlp-remote-cipher
```

#### Manual install

1. Download the latest release zip from [releases](https://github.com/coletdjnz/yt-dlp-remote-cipher/releases) 

2. Add the zip to one of the [yt-dlp plugin locations](https://github.com/yt-dlp/yt-dlp#installing-plugins)

    - User Plugins
        - `${XDG_CONFIG_HOME}/yt-dlp/plugins` (recommended on Linux/macOS)
        - `~/.yt-dlp/plugins/`
        - `${APPDATA}/yt-dlp/plugins/` (recommended on Windows)
    
    - System Plugins
       -  `/etc/yt-dlp/plugins/`
       -  `/etc/yt-dlp-plugins/`
    
    - Executable location
        - Binary: where `<root-dir>/yt-dlp.exe`, `<root-dir>/yt-dlp-plugins/`

If installed correctly, you should see the `remotecipher` JS Challenge provider in `yt-dlp -v YOUTUBE_URL` output:

    [debug] [youtube] [jsc] JS Challenge Providers: remotecipher-X.Y.Z (external)

### Configure

> [!TIP]
> You can pass multiple options by separating them with semicolons (`;`). 
> 
> e.g `--extractor-args "youtubejsc-remotecipher:base_url=...;api_key=..."`

#### Server URL

You will need to point yt-dlp to an available yt-cipher server. You can follow the instructions at the [yt-cipher repository](https://github.com/kikkia/yt-cipher) to set up your own server.

To point yt-dlp to the server, set the `base_url` extractor argument:

   `--extractor-args "youtubejsc-remotecipher:base_url=https://ytcipher.example.com"`
   
By default, `http://127.0.0.1:8001` is used as the server base URL.

If running locally with a proxy, set the `NO_PROXY` environment variable to avoid proxying requests to the local server.
e.g. `NO_PROXY=127.0.0.1`

#### API Key

Configure yt-dlp to use an API key if the server requires it:

   `--extractor-args "youtubejsc-remotecipher:api_key=YOUR_API`

Alternatively you can set the `REMOTE_CIPHER_API_KEY` environment variable.

#### Other options

- `timeout`: Set the request timeout in seconds (default follow `--socket-timeout` (20s))

   `--extractor-args "youtubejsc-remotecipher:timeout=15"`

### Development

1. Install hatch
    ```sh
    pip install hatch
    ```
2. Run setup
    ```sh
    hatch run setup
    ```
3. Lint and format
    ```sh
    hatch fmt
    ```
4. Build
    ```sh
    hatch build
    ```