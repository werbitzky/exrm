# Elixir Release Manager

## Getting Started

This project's goal is to make releases with Elixir projects a breeze. It is composed of a mix task, and all build files required to successfully take your Elixir project and perform a release build. All you have to do to get started is the following:

1. Add `exrm` as a dependency to your project

```elixir
  defp deps do
    [{:exrm, github: "bitwalker/exrm"}]
  end
```

2. Fetch and Compile

- `mix deps.get`
- `mix deps.compile`

3. Perform a release

- `mix release`

4. Run your app! (my example is based on a simple ping server, see the appendix for more info)

```
> rel/example_app/bin/example_app
Erlang/OTP 17 [RELEASE CANDIDATE 1] [erts-6.0] [source-fdcdaca] [64-bit] [smp:4:4] [async-threads:10] [hipe] [kernel-poll:false]

Interactive Elixir (0.12.5) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)> :gen_server.call(:test, :ping)
:pong
iex(2)>
```

## Features

## Issues

If you run into problems, this is still early in the project's development, so please create an issue, and I'll address ASAP.

## Appendix

The example server I setup was as simple as this:

- `mix new test`
- `cd test && touch lib/test/server.ex`

Then put the following in `lib/test/server.ex`

```elixir
defmodule Test.Server do
  use GenServer.Behaviour

  def start_link() do
    :gen_server.start_link({:local, :test}, __MODULE__, [], [])
  end

  def init([]) do
    { :ok, [] }
  end
  
  def handle_call(:ping, _from, state) do
    { :reply, :pong, state }
  end

end
```

You should be able to replicate my example using these steps. If you can't, please let me know.