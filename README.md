# dokku-redirect

dokku-redirect is a plugin for [dokku][dokku] that gives the ability to set simple redirects for an application.

This plugin only redirects between domains. It does not inspect or modify the remainder of the URL. For TLS-enabled domains managed by dokku, this plugin automatically sets up redirects for both http and https connections.

## Installation

```sh
# dokku 0.6+
$ dokku plugin:install https://github.com/dokku/dokku-redirect.git
```

## Commands

```
$ dokku redirect:help
    redirect:add <app> <src> <dst> [<code>]    Add a redirect from <src> domain to <dst> domain, with optional HTTP code
    redirect:remove <app> <src>                Remove a redirect from <src> domain
    redirect:remove-all <app>                  Remove all redirects from an app
    redirect:report [<app>]                    Display a report on redirects, optionally limited to a single app
```

## Redirect Codes

| Code | Name               | Behavior                                           |
| ---- | ------------------ | -------------------------------------------------- |
| 301  | Moved Permanently  | __(Default)__ Permanent, preserves method          |
| 302  | Found              | Temporary, may change method to GET                |
| 303  | See Other          | (HTTP/1.1) Temporary, changes method to GET        |
| 307  | Temporary Redirect | (HTTP/1.1) Temporary, preserves method             |

## Examples

Check redirects on my-app
```shell
$ dokku redirect:report my-app

SOURCE       DESTINATION      CODE
ma.dokku.me  my-app.dokku.me  301
```

Add a new redirect on my-app
```shell
$ dokku redirect:add my-app ma.dokku.me my-app.dokku.me

-----> Adding redirect for my-app...
       done
```

Remove an existing redirect
```shell
$ dokku redirect:remove my-app ma.dokku.me

-----> Removing redirect for my-app...
       done
```

## License

This plugin is released under the MIT license. See the file [LICENSE](LICENSE).

[dokku]: https://github.com/progrium/dokku
