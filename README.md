# BitcoinLib

**.NET Bitcoin & Altcoins library**

## Features

- Compatible with [Bitcoin Core](https://bitcoin.org/en/download) RPC API.
- Strongly-typed structures for complex RPC requests and responses.
- Implicit JSON casting for all RPC messages.
- Extended methods for every-day scenarios where the built-in methods fall short.
- Exposure of all [RPC API's functionality](https://en.bitcoin.it/wiki/Original_Bitcoin_client/API_calls_list) as well as the extended methods through a single interface.
- Custom RPC exceptions.
- Supports all Bitcoin clones.
- Can operate on unlimited daemons with a single library reference.
- [Bitcoin](http://en.wikipedia.org/wiki/Bitcoin), [Litecoin](http://en.wikipedia.org/wiki/Litecoin), [Dogecoin](http://en.wikipedia.org/wiki/Dogecoin), SmartCash, Dash and other Altcoins included.
- Each coin instance can be fully parametrized at run-time and implement its own constants.
- Demo client included.
- Disconnected raw RPC connector included for quick'n'dirty debugging.
- Handles and relays RPC internal server errors along with their error code.
- Can work without a `.config` file.
- Fully compatible with [Mono](http://www.mono-project.com/).
- [Test Network (testnet)](https://bitcoin.org/en/developer-examples#testnet) and [Regression Test Mode (regtest)](https://bitcoin.org/en/developer-examples#regtest-mode) ready.
- Fully configurable.

## Donations

This library took a significant amount of time and effort to build and requires continuous maintenance in order to keep up with changes introduced with every new Bitcoin-Core release. Keep it up by donating at: [15Nb3RhMd13zp5Pc7yngUon83nFtEZUyBA](bitcoin:15Nb3RhMd13zp5Pc7yngUon83nFtEZUyBA?label=BitcoinLib)

## Support

Premium Support is available by our team of experts at: [info@powermobile.org](mailto:info@powermobile.org).

## License

See [LICENSE](LICENSE).

## NuGet packages

BitcoinLib is available on NuGet:

* [BitcoinLib](https://www.nuget.org/packages/BitcoinLib/)

## Versioning

From version 1.4.0, BitcoinLib follows [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).

## Building from source

To build BitcoinLib from source, you will need either the
[.NET Core SDK or Visual Studio](https://www.microsoft.com/net/download/).

### Linux-specific

If you are using Linux you will also need Mono installed
(in order to run Paket). The full install sequence (for Ubuntu)
will be something like [this](https://github.com/powermobileteam/fsharp-hedgehog/pull/153#issuecomment-364325504).

### Building & running tests

With Visual Studio you can build BitcoinLib and run the tests
from inside the IDE, otherwise with the `dotnet` command-line
tool you can execute:

```sh
dotnet build src/BitcoinLib.sln
```

The first time you run it, this will use Paket to restore all
the packages, and then build the code.

## Instructions for Bitcoin

- Locate your `bitcoin.conf` file (in Windows it's under: `%AppData%\Roaming\Bitcoin`, if it's not there just go ahead and create it) and add these lines:
  ```
  rpcuser = MyRpcUsername
  rpcpassword = MyRpcPassword
  server=1
  txindex=1
  ```
- Edit the `app.config` file in the Console test client to best fit your needs. Make sure you also update the `bitcoin.conf` file when you alter the `Bitcoin_RpcUsername` and `Bitcoin_RpcPassword` parameters.

## Instructions for Litecoin and other Bitcoin clones

- Perform the same steps as those mentioned above for Bitcoin.
- Litecoin configuration file is: `litecoin.conf` under: `%AppData%\Roaming\Litecoin` and its daemon is: `litecoind`.
- Each coin can be initialized by its own interface specification:
  - `IBitcoinService BitcoinService = new BitcoinService();`
  - `ILitecoinService LitecoinService = new LitecoinService();`
- Any bitcoin clone can be adopted without any further installation steps with the use of the generic `ICryptocoinService`:
  - `ICryptocoinService cryptocoinService = new CryptocoinService("daemonUrl", "rpcUsername", "rpcPassword", "walletPassword");`
- Use `(ICryptocoinService).Parameters` to fully configure each coin pointer at run-time.

## Configuration

Sample configuration:

```xml
???<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <appSettings>
    <!-- BitcoinLib settings start -->

      <!-- Shared RPC settings start -->
      <add key="RpcRequestTimeoutInSeconds" value="10" />
      <!-- Shared RPC settings end -->

      <!-- Bitcoin settings start -->
      <add key="Bitcoin_DaemonUrl" value="http://localhost:8332" />
      <add key="Bitcoin_DaemonUrl_Testnet" value="http://localhost:18332" />
      <add key="Bitcoin_WalletPassword" value="MyWalletPassword" />
      <add key="Bitcoin_RpcUsername" value="MyRpcUsername" />
      <add key="Bitcoin_RpcPassword" value="MyRpcPassword" />
      <!-- Bitcoin settings end -->

    <!-- BitcoinLib settings end -->
  </appSettings>
</configuration>
```
