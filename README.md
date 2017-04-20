# PlugEtsCache

A simple caching system based on [Plug](https://github.com/elixir-lang/plug) and [ETS](http://erlang.org/doc/man/ets.html).

## Installation

1. Add `plug_ets_cache` to your list of dependencies in `mix.exs`:

  ```elixir
  def deps do
    # Get from hex
    [{:plug_ets_cache, "~> 0.1.0"}]
    # Or use the latest from master
    [{:plug_ets_cache, github: "andreapavoni/plug_ets_cache"}]
  end
  ```

2. Ensure `plug_ets_cache` is started before your application:

  ```elixir
  def application do
    [applications: [:plug_ets_cache]]
  end
  ```

## Usage

1. Set configuration in `config/config.exs` (the following values are defaults):

  ```elixir
  config :plug_ets_cache,
    db_name: :ets_cache,
    ttl_check: 60,
    ttl: 300
  ```

2. Add `PlugEtsCache.Plug` to your router/plug:

  ```elixir
  plug PlugEtsCache.Plug
  ```

3. Call `PlugEtsCache.Response.cache_response` *after you've sent a response*:

  ```elixir
  # example with a Phoenix controller
  defmodule MyApp.SomeController do
    use MyApp.Web, :controller
    import PlugEtsCache.Response, only: [cache_response: 1]

    # ...

    def index(conn, params) do
      # ...
      conn
      |> render "index.html"
      |> cache_response
    end

    # ...
  end
  ```

## Documentation
The docs can be found at [https://hexdocs.pm/plug_ets_cache](https://hexdocs.pm/plug_ets_cache).

## TODO

* add more detailed docs
* configure `ttl` on specific cached responses

## Contributing

Everyone is welcome to contribute to PlugEtsCache and help tackling existing issues!

Use the [issue tracker](https://github.com/andreapavoni/plug_ets_cache/issues) for bug reports or feature requests.

Please, do your best to follow the [Elixir's Code of Conduct](https://github.com/elixir-lang/elixir/blob/master/CODE_OF_CONDUCT.md).

## License

Plug source code is released under MIT License. Check [LICENSE](https://github.com/andreapavoni/plug_ets_cache/blob/master/LICENSE) file for more information.
