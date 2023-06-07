# Splunk Plugin 
**Maintainer:** [@dbejanishvili](https://github.com/dbejanishvili)
**Co-Maintainers:** [@bakurits](https://github.com/bakurits) [@Gvantsats](https://github.com/Gvantsats)

A Splunk integration for Mattermost which enables users to get logs and alerts from Splunk server. 

## Admin guide

### Installation

#### Marketplace installation
1. In Mattermost, go to **Main Menu > Plugin Marketplace**.
2. Search for "Splunk" or find the plugin from the list.
3. Select **Install**.
4. When the plugin has downloaded and been installed, select **Configure**.

#### Manual installation
If your server doesn't have access to the internet, you can download the [latest plugin binary release](https://github.com/mattermost/mattermost-plugin-splunk/releases) and upload it to your server via **System Console > Plugin Management**. The releases on this page are the same used by the Marketplace. To learn more about how to upload a plugin, see the [Mattermost Developer documentation](https://docs.mattermost.com/administration/plugins.html#plugin-uploads).

## User guide

- **Authenticate user**: Use ``/splunk auth login [server base url] [splunk username]/[token]``. 
    - You must be logged into the system before you can use any slash commands regarding logging. To authenticate the user, you can use this slash command with two required parameters: Splunk server base URL, Splunk username, or token. 
    -  If you already logged in to a plugin with a token, the future logins can be done by providing only the username too. The command is ``/splunk auth login [server base url] [splunk username]``. 
    -  After successful authentication this message is shown:

        ![image](https://github.com/mattermost/mattermost-plugin-splunk/assets/74422101/25722f11-066d-4f41-9ba9-3a32e03564cd)
    
- **Get a list of all logs from the Splunk server**: Use ``/splunk log list``.

    ![image](https://github.com/mattermost/mattermost-plugin-splunk/assets/74422101/998a48d1-6e45-4cb1-bcc6-6250158a5daf)

- **Get specific log from server**: Use ``/splunk log [logname]``.

    ![image](https://github.com/mattermost/mattermost-plugin-splunk/assets/74422101/1fce88fa-2a9e-45a3-95f5-2e9d06fd25c8)

- **Subscribe to alerts**: Use ``/splunk alert subscribe``. Use this slash command and add a link for Splunk. After receiving the alert, the Splunk bot posts in the channel that new alert has been received.

    ![image](https://github.com/mattermost/mattermost-plugin-splunk/assets/74422101/0d4ec851-0420-4c23-8c3c-539142f1db63)

    ![image](https://github.com/mattermost/mattermost-plugin-splunk/assets/74422101/f689b63e-9090-4ab5-8dc2-af1152440c02)

## Development

### Set up environment

Fork the repository to your own account and then clone it to a directory outside of `$GOPATH` matching your plugin name:

`git clone https://github.com/owner/mattermost-plugin-splunk`

Note that this project uses [Go modules](https://github.com/golang/go/wiki/Modules). Be sure to locate the project outside of `$GOPATH`, or allow the use of Go modules within your `$GOPATH` with an export `GO111MODULE=on`.

### Run a Splunk server with Docker

There is a [docker-compose.yml](https://github.com/mattermost/mattermost-plugin-splunk/blob/master/dev/docker-compose.yml) in the dev folder of the repository, configured to run a Splunk server for development. You can run make splunk in the root of the repository to spin up the Splunk server. The Splunk web application will be served at `http://localhost:8000` and the API will be served at `https://localhost:8089`.

The `SPLUNK_PASSWORD` environment variable is set to `SplunkPass`, as defined in the `docker-compose.yml` file. You can login with these credentials:

Username: `admin`

Password: `SplunkPass`

If you want to modify the default Alert hostname, you can do so editing the `default.yml` file and replace `<MY_ALERT_HOSTNAME>` with your valid hostname (ex: `https://myhost.ngrok.io`).

### Build and deploy
To build your plugin use `make`, you can use `MM_DEBUG=1` as an envvar to generate a debug version of the plugin, including an unminified version of the Javascript webapp.

Use make `check-style` to check the style, use `make dist` and make deploy to build and deploy the application.
`make` will produce a single plugin file (with support for multiple architectures) for upload to your Mattermost server:

`dist/com.example.my-plugin.tar.gz`

Alternatively you can deploy a plugin automatically to your server, but it requires login credentials:

```
export MM_SERVICESETTINGS_SITEURL=http://localhost:8065
export MM_ADMIN_USERNAME=admin
export MM_ADMIN_PASSWORD=password
make deploy
```

or configuration of a [personal access token](https://developers.mattermost.com/integrate/reference/personal-access-token/):

```
export MM_SERVICESETTINGS_SITEURL=http://localhost:8065
export MM_ADMIN_TOKEN=j44acwd8obn78cdcx7koid4jkr
make deploy
```

In production, deploy and upload your plugin via the Mattermost System Console. See the [Mattermost Developer documentation](https://developers.mattermost.com/integrate/plugins/using-and-managing-plugins/) for details.

## Help and support

For questions, suggestions, and help, visit the [Splunk Plugin channel](https://community.mattermost.com/core/channels/plugin-splunk) on our Community server. To report a bug, please open a GitHub issue.

## License

This repository is licensed under the [Apache 2.0 License](https://github.com/mattermost/mattermost-plugin-splunk/blob/master/LICENSE).

## Contributing

Visit our [Development guide](https://mattermost.gitbook.io/splunk-plugin/development/development) for information about how to contribute to this plugin.

## Help wanted

If you're interested in joining our community of developers who contribute to Mattermost, check out the current set of issues that are being requested. You can also find issues labeled "Help Wanted" in the Jira repository that we have laid out the primary requirements for and could use some coding help from the community.
