---
layout: post
title: "Flatfoot, pt 2 - Phoenix 1.3"
img: flatfoot-pt-2/cover.png # Add image post (optional)
date: 2017-08-13 00:00:00 +0500
description: Using Phoenix 1.3 to build an API. # Add post description (optional)
tag: [Capstone, Blogging, Elixir, Phoenix, Phoenix 1.3, JSON, Websocket]
---
# Flatfoot

![](https://github.com/favicon.ico) &nbsp;&nbsp;<a href="https://github.com/davelively14/flatfoot" target="\_blank">View on GitHub</a>
<br>
<img src="https://image.flaticon.com/icons/png/128/12/12195.png" width="32"> &nbsp;&nbsp;<a href="https://obscure-reef-78695.herokuapp.com/" target="\_blank">View Demo</a>

## Note on this entry

This is an updated version of an earlier post, where I used the first release candidate for Phoenix 1.3 for my project. The released Phoenix 1.3.0 [differed slightly](https://elixirforum.com/t/phoenix-1-3-0-released/7150/8) from the release candidate, notably in where the `web` directory is located. Those changes are all reflected here.

## Capstone

The idea for my capstone project came from my [wife](http://www.neboagency.com/about/people/#person-57). After one of those senseless, cyberbullying induced suicides, my wife though of an app where parents could monitor their loved one’s social media public feeds for any signs of bullying or outward displays of suicide ideation. In order to limit the scope of what promised to be a significant undertaking for a lone developer, I chose to collect on a single social media site initially. Given its robust API and general ease of use, I chose [Twitter](https://dev.twitter.com/).

## The Stack

For my tech stack, I chose to deviate from other languages I had already used. There wasn’t anything particularly wrong with Rails, JQuery, or AngularJS, but with an open sandbox and my pick of tools, I selected my favorites: [Eilxir](https://elixir-lang.org/) on the backend, with [Phoenix](http://www.phoenixframework.org/) providing the web interface layer, and [React](https://facebook.github.io/react/) with [Redux](http://redux.js.org/) for the frontend demo. While Python or any number of other languages might have been more performant in terms of parsing and analyzing the collected data, few can compete with Elixir’s out of the box scalability, fault tolerance, and maintainability.

In order to develop a wider variety of skills in an academic setting, I chose to expose two different Phoenix endpoints as my user interaction layer. The first is a JSON API for handling all things related to user profile, settings, and authentication. For the other, I would use a [famously](http://www.phoenixframework.org/blog/the-road-to-2-million-websocket-connections) efficient Phoenix Channel to manage websocket connections that expose the social media monitoring functionality of the app to the user. In regards to data collection from external API's and analysis, I chose to utilize Elixir's built in Erlang OTP abstraction.

### Living on the Edge

<img align="left" src="https://pbs.twimg.com/profile_images/540333799557439489/-s9uoLIN.png" width="250">
Since this is an app I built in order to further my education, I opted to venture out on the bleeding edge and use Phoenix 1.3. Don’t let the what seems like a minor version change fool you. While there are no real breaking changes or significant new features being introduced in 1.3, alterations to the directory structure and new code generators introduce a seismic shift in how a developer approaches a Phoenix project. [Chris McCord](http://www.chrismccord.com/) provides an overview of these changes in the [Lonestar Elixir keynote address](https://www.youtube.com/watch?v=tMO28ar0lW8), his release candidate [Elixir Forum post](https://elixirforum.com/t/phoenix-v1-3-0-rc-0-released/3947), [version 1.3 forum post](https://elixirforum.com/t/phoenix-1-3-0-released/7150/8), and his more recent [ElixirConf EU keynote](https://www.youtube.com/watch?v=pfFpIjFOL-I). Additionally, [astonj](http://astonj.com/) has compiled and maintains a [Phoenix Contexts - learning resources](https://elixirforum.com/t/phoenix-contexts-learning-resources/5930). Those were all essential for me to getting started, but I found the concepts easier to grasp once I began building my project.

While the Phoenix team does emphasize that these changes are suggestions for how to organize and approach your project, for the purposes of my app I chose to implement it (mostly) as suggested. For me, these are the three big takeaways from this new version:

#### Web Location
- While Phoenix has only ever been the web framework for your Elixir app, the new directory structure makes that abundantly clear and better defines its role. Everything relating to collecting and serving Phoenix web endpoints is neatly packed away within the `lib/my_app_web` directory.

#### Contexts
- On a similar note, models are gone. Whereas Phoenix's web interface was once built around models within the `/web` directory, we now extract that data fetching and manipulation (along with their implementation and support modules) to their own, self-contained systems. The functionality within those systems is exposed via **contexts**, which are dedicated modules that expose and group related functionality for an underlying system (i.e. `clients.ex` is the context module for the `Clients` system and is located in the `lib/my_app/clients` directory). These contexts allow us to decouple and isolate the systems from the remainder of the application and manage them independently. If that's a bit confusing, just hang on - it'll make mores sense as we get into the app.

#### Assets Location
- Assets no longer clog up the root directory. All of your external assets are stored in the `/assets` directory. Since I was using Webpack for this project, this was a particular pain for me initially, but ultimately it makes the project easier to navigate. If you’re interested, [here’s how I setup and configured](https://github.com/davelively14/configs/blob/master/phoenix_1.3.0_react_redux.md) my Phoenix 1.3 app to work with Webpack 2, React, Redux, and React Router.

At its core, Phoenix 1.3 provides a forcing mechanism to design with intent. You have to think about what you’re going to do before you do it. Early on, I struggled a bit with the new structure, but ultimately these guidelines lead to more purposeful app development, with clear divisions of responsibility, and more reliable code.

## The stuff dreams are made of

<img src="http://www.filminamerica.com/Movies/TheMalteseFalcon/falcon06.jpg" alt="Maltese Falcon, 1941" style="display: block; margin: 0 auto">

A quick note on the nomenclature for this project. In keeping with the Phoenix mythical bird theme, these systems are named after characters from the classic 1941 film, [The Maltese Falcon](https://en.wikipedia.org/wiki/The_Maltese_Falcon_(1941_film)). The relevant part of the movie's premise is rather simple: A prospective **Client** approaches Bogart's famous character, Sam **Spade**, with an interesting case. Spade takes the case and dispatches his partner, Miles **Archer**, to gather information on the case and report back, but ultimately it's up to Spade to solve the mystery. Fortunately, we made a few improvements on the movie, so if Archer would happen to die under mysterious circumstances, he’ll be seamlessly revived and put back into action thanks to the magic of OTP.

I settled on the name Flatfoot for the app. I realize that's more a beat cop than a private investigator like Spade, but 1940's era slang for a PI doesn't seem appropriate in a modern context.

### Organizing in Phoenix 1.3

We can see a basic outline of the architecture quite clearly in the new directory structure. Each system has it's own directory within `/lib/flatfoot`. Also worth noting, the old `/web` directory - once a clinger to the root in early versions of Phoenix - now finds a more appropriate home and a new name: `/lib/flatfoot_web`.

<img src="../assets/img/flatfoot-pt-1/dir_tree_overview_1_3_0.png" alt="Figure 1" style="width: 100%">
<small>**Figure 1.** *Flatfoot directory tree in Phoenix 1.3*</small>

If you’re used to running a third party bundler like [webpack](https://webpack.github.io/) with earlier versions of Phoenix, you’re also likely to notice how uncluttered the root directory is. Our `package.json`, `webpack.config.js`, `.babelrc`, testing configs, and the `node_module` directory are now all packed away quite neatly within `/assets`.

We're left with a clean, easy to reference directory tree, with clearly defined boundaries for our systems.

### System design

<img src="../assets/img/flatfoot-pt-1/web_system_1_3_0.png" alt="Figure 2" style="width: 100%">
<small>**Figure 2.** *Flatfoot systems overview.*</small>

In this app's most basic form, all user interaction is managed by the `FlatfootWeb` system. It's responsible for handling requests from the user, requesting and persisting data via interaction with the other systems, and returning gathered data to the user. The `Clients` and `Spade` systems expose their interface to the `Web` system via their context modules. The `Clients` system handles all requests relating to the management of users and their preferences, such as creating a profile, editing that profile, and authorizing access via session tokens. The `Spade` system is where the significant action begins.

<img src="../assets/img/flatfoot-pt-1/data_flow.png" alt="Figure 3" style="width: 100%">
<small>**Figure 3.** *Data flow when requesting new results.*</small>

Via websocket transport monitored by `SpadeChannel`, users may request retrieval or deletion of persisted results or request new results altogether. Figure 3 depicts what happens when a user requests new results.
- On order, `SpadeChannel` will make a call to the `SpadeInspector` context module, which in turn sends a request to `SpadeInspector.Server` - an OTP module within the system.
- That `Server` builds `configs` (which includes it's own `pid` as a return address) for each social media account being monitored and sends those `configs` to the `Archer` context, which in turn sends those configs to the internal `Archer.Server` module.
- That `Server` then calls on `Archer.FidoSupervisor` - a `TaskSupervisor` - to initialize and monitor the backends (in this case just `Archer.Backends.Twitter`).
- Each backend will send results back to `SpadeInspector.Server`, per the return address `pid`.
- Upon receipt of new results, `SpadeInspector.Server` system will evaluate those results, store them, and asynchronously return them to the user.

## Contexts as API for App Boundaries

As Mikel Myskala has [pointed out](http://michal.muskala.eu/2017/05/16/putting-contexts-in-context.html), the biggest mind shift here is understanding that we're only minimally coupling our data to our application. One of the more challenging aspects was developing optimal boundaries for my application - and I'm still pretty sure I could further improve things.

<img src="../assets/img/flatfoot-pt-1/boundaries.png" alt="Figure 3" style="width: 100%">
<small>**Figure 4.** *Flatfoot's boundaries*</small>

Unlike previous versions of Phoenix, accessing the underlying schema and modules should only be accomplished by calling functions within the context module - so no more `Repo` calls from controllers. Within these contexts you'll find common, RESTful functions like `Clients.create_user(attrs)` or `Clients.get_user!(123)`. But you can quickly create more dynamic and useful functions like `Clients.get_user_by_token(token)`, which returns a `User` when provided a valid session token. The `Flatfoot.Clients` context functions as the boundary and it's the only place you should expose the underlying system to the rest of the app.

### Internal directory structures

Each system has it’s own directory, with a matching name context file. To aide in my own readability, I broke slightly with the out of the box Phoenix 1.3 directory convention. In order to avoid cluttering each system’s root directory with schema, I nested all of the `Ecto` schemas within the `/schema` directory:

<pre>
|-- spade
    |-- schema
    |   |-- backend.ex
    |   |-- suspect.ex
    |   |-- suspect_account.ex
    |   |-- user.ex
    |   |-- ward.ex
    |   |-- ward_account.ex
    |   |-- ward_result.ex
    |   |-- watchlist.ex
    |
    |-- <a href="https://github.com/davelively14/flatfoot/blob/master/lib/flatfoot/spade/spade.ex" target="\_blank">spade.ex</a> <-- Click to view
</pre>

It’s important to note that these systems can be more than just a single context file and schema. Any Elixir modules affecting the system can - and most likely should - be located within the boundary. In my `Archer` system (see directory tree below), I included an `archer/otp` directory to house my `ArcherSupervisor`, `Archer.Server`, and `/backends`, which contains my task modules.

<pre>
|-- archer
    |-- otp
    |   |-- backends
    |   |   |-- twitter.ex
    |   |
    |   |-- archer_supervisor.ex
    |   |-- server.ex
    |
    |-- schema
    |   |-- backend.ex
    |
    |-- <a href="https://github.com/davelively14/flatfoot/blob/master/lib/flatfoot/archer/archer.ex" target="_blank" __>archer.ex</a> <-- Click to view
</pre>

The key to maintaining the boundary here, is that any interactivity with the server or backend schema goes through the `archer.ex` context. For example, `Flatfoot.Archer.fetch_data/1` exposes the `Flatfoot.Archer.Server.fetch_data/1` function:

```elixir
defmodule Flatfoot.Archer do
  ...
  ##########
  # Server #
  ##########

  alias Flatfoot.Archer.Server

  def fetch_data(configs) do
    Server.fetch_data(configs)
  end
  ...
end
```
<br>
While this can appear unnecessary, this loose coupling provides a layer of isolation that let's us modify our code internal to the system without having to consider that we are breaking any dependencies elsewhere in our app. A (nonsensical) example here, would be that if we wanted, we could change the name of the function from `Server.fetch_data/1` to `Server.get_me_some_data/1`. Instead of having to change every call to `Server.fetch_data/1`, we only have to adjust it in the context:

```elixir
...
def fetch_data(configs) do
  Server.get_me_some_data(configs)
end
...
```

## Same schema, different system

There are often times when different systems need access to the same table in the database. In Flatfoot, the `Archer`, `Spade`, and `SpadeInspector` systems all require access to data from the `backends` table. In earlier version of Phoenix, everyone would just refer to the same `Archer.Backends` model, thereby adding yet another coupling between different systems. In Phoenix 1.3, however, we simply create customized schemas for each system.

<img src="../assets/img/flatfoot-pt-1/boundaries_backend_focus.png" alt="Figure 3" style="width: 100%">
<small>**Figure 5.** *Each system needing access to the `backends` table has their own schema.*</small>

While each of the three `Backend` modules in Figure 5 are schemas that represent data from the same table, they only pull fields and associations according to the needs of the system (see Figure 6 below). The `SpadeInspector` system only needs the module name for each backend in order to build the right configuration, while the `Spade` system only needs a few fields available in case users need that data to select a backend for a particular account. We are able to deliberately encapsulate our schemas and associations within each system and minimize coupling.

<img src="../assets/img/flatfoot-pt-1/backend_systems.png" alt="Figure 3" style="width: 100%">
<small>**Figure 6.** *Backends for each system.*</small>

### Special considerations - associations in disparate systems

For my app, I had one situation where I needed to associate across boundaries in order to properly handle deleting a `User`. Similar to the situation above, both the `Clients` system and `Spade` system make reference to the `users` table and they both specify different `has_many` associations for their unique `User` schemas:

<img src="../assets/img/flatfoot-pt-1/user_problems.png" alt="Figure 3" style="width: 100%">
<small>**Figure 7.** *Same table, different associations*</small>

This all works perfectly well until someone needs to delete their account. The `Clients` context needs to offer account deletion functionality, so we create a simple function within that context:

```elixir
def delete_user(%User{} = user) do
  Repo.delete(user)
end
```
<br>
When we run our tests, however, we get an error:

```
1) test delete_user/1 deletes associated wards from Archer (Flatfoot.ClientsTest)
     test/clients/clients_test.exs:95
     ** (Ecto.ConstraintError) constraint error when attempting to delete struct:
     
         * foreign_key: wards_user_id_fkey
     
     "If you would like to convert this constraint into an error, please
     call foreign_key_constraint/3 in your changeset and define the proper
     constraint name. The changeset has not defined any constraint."
```
<br>
Our `User` is still be referenced by elements of another table, so Ecto will throw that `ConstraintError`. Our problem, though, is that our `User` schema in `Clients` does not declare the `has_many` ratio with `wards` table.

We could simply add the `has_many :wards` and `has_many :watchlists` with a `on_delete: delete_all` option, which is what the [Phoenix 1.3 guides suggest](https://hexdocs.pm/phoenix/1.3.0/contexts.html#cross-context-dependencies). But since those guides weren't available in the RC version of 1.3.0, and I was rather obsessed with decoupling, I opted to create one central schema that contained all the associations.

I wouldn't recommend doing this (follow the guides above), but I leave it here to show an alternate method: create a new shared system:

<pre>
|-- shared
|   |-- schema
|   |   |-- <b>user.ex</b>
|   |
|   |-- shared.ex
</pre>

The system has one schema, `user.ex`:

```elixir
defmodule Flatfoot.Shared.User do
  use Ecto.Schema

  schema "users" do
    has_many :sessions, Flatfoot.Clients.Session, on_delete: :delete_all
    has_many :notification_records, Flatfoot.Clients.NotificationRecord,
              on_delete: :delete_all
    has_many :blackout_options, Flatfoot.Clients.BlackoutOption,
              on_delete: :delete_all
    has_many :wards, Flatfoot.Spade.Ward, on_delete: :delete_all
    has_many :watchlists, Flatfoot.Spade.Watchlist, on_delete: :delete_all
  end
end
```

And the context, `shared.ex`, only one function:

```elixir
defmodule Flatfoot.Shared do
  alias Flatfoot.{Repo, Shared.User}

  def delete_user(user_id) do
    User |> Repo.get(user_id) |> Repo.delete
  end
end
```

Now we go back and modify our `Clients` context:

```elixir
def delete_user(%Flatfoot.Clients.User{} = user) do
  result = Flatfoot.Shared.delete_user(user.id)
  if result |> elem(0) == :ok, do: {:ok, user}, else: result
end
```

Note that we return a `Clients.User` structure instead of the `Shared.User` that `Flatfoot.Shared.delete_user(user.id)` returns. If we just returned the result directly, it would only be a user struct with associations, which isn't that useful.

## Conclusion

Phoenix 1.3 is a significant departure, not only from earlier iterations of framework, but also from the MVC architectures that have dominated web development recently. One can't help but feel that Phoenix is coming into it's own, escaping the dominating shadow of the popular frameworks before it, and offering something new, something more in line with evolving, modern web design. Additionally, Phoenix 1.3 feels more like a natural extension of an Elixir umbrella app or collection of microservices than it does a monolithic MVC app like Rails.

It takes some getting used to, but the future is bright.
