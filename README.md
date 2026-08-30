[![](https://img.shields.io/nuget/v/soenneker.enums.currencycodes.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.enums.currencycodes/)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.enums.currencycodes/publish-package.yml?style=for-the-badge)](https://github.com/soenneker/soenneker.enums.currencycodes/actions/workflows/publish-package.yml)
[![](https://img.shields.io/nuget/dt/soenneker.enums.currencycodes.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.enums.currencycodes/)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.enums.currencycodes/codeql.yml?label=CodeQL&style=for-the-badge)](https://github.com/soenneker/soenneker.enums.currencycodes/actions/workflows/codeql.yml)

# Soenneker.Enums.CurrencyCodes

A string-backed currency-code type for payment and financial API contracts. Values use lowercase, three-letter wire strings such as `usd`, `eur`, and `gbp`.

## Install

```bash
dotnet add package Soenneker.Enums.CurrencyCodes
```

## Usage

```csharp
using Soenneker.Enums.CurrencyCodes;

CurrencyCode currency = CurrencyCode.Usd;
string wireValue = currency.Value; // "usd"

if (CurrencyCode.TryFromValue(input, out CurrencyCode? parsed))
{
    // Use parsed in a typed request model
}
```

`System.Text.Json` serializes the type as its lowercase string value and restores recognized values to the corresponding static instance. `FromValue` throws for an unknown value; use `TryFromValue` at external-input boundaries. `FromName` and `TryFromName` are also generated for C# member-name lookup, such as `"Usd"`.

## Important boundaries

The constants are a compatibility list for API contracts, not a live currency registry or a guarantee that a payment processor accepts a currency. The set includes legacy identifiers such as `mro`, `std`, and `sll`; verify processor support and settlement rules when accepting a user-selected currency.

The type represents only the currency identifier. It does not provide symbols, localized names, exchange rates, decimal precision, minor-unit conversion, or amount validation. Keep monetary amounts in an appropriate decimal or minor-unit representation and apply the target processor's rules separately.
