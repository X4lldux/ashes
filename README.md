#Ashes

A code generation tool for the [Phoenix](http://www.phoenixwebframework.com) web framework.

```elixir
defp deps do
  [{:ashes, ">= 0.0.1"}]
end
```

###Controllers
Generates a controller with a given name, will also generate a view and create a folder
for you to put related .eex templates in. **Don't forget to add the controller in `routes.ex`**

```bash
$ mix ashes.generate controller <controllername>
```

```elixir
# routes.ex
defmodule MyApp.Router do
  resource "/my", MyController
end
```

Will give you the following methods by default:

* index
* edit
* new
* show
* create
* update
* delete

**Options**
* `--skip-form` - removes the `edit` and `new` methods from the controller (likely used for APIs)
* `--skip-view` - doesn't create a view module
* `--skip-template`- doesn't create a folder for templates

###Channels
Generates a channel with the given name. **Don't forget to add the channel to your router**

```bash
$ mix ashes.generate channel <channelname> [events]
```
```elixir
# routes.ex
defmodule MyApp.Routes do
  socket "/ws", MyApp do
    channel "my:*", MyChannel
  end
end
```

Will give you the following methods by default:
* `join(_topic, socket)`
* `leave(_reason, socket)`

If you provide events in the generate command, they will be added to the channel as
```elixir
def handle_in("eventname", message, socket) do
  {:ok, socket}
end
```

###Models
Generates an [Ecto](https://github.com/elixir-lang/ecto) model with the given name and schema. **Requires ecto!**

```bash
$ mix ashes.generate model <modelname> [schema entries]
```

Schema entries should be of the form `name:type` with types being defined by ecto. 

**Options**
* `--timestamps` - adds a `created_at` and `updated_at` field to the schema along with some plumbing to keep the fields up to date.

###Migrations
**Assumes a valid repo module name of MyApp.Repo**

Generates an [Ecto](https://github.com/elixir-lang/ecto) migration with the given name. **Requires ecto**
```bash
$ mix ashes.generate migration <migrationname>
```

