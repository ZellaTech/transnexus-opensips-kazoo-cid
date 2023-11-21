# Fixing CNAM Display Issue with Kazoo and TransNexus In-line Proxy (OpenSIPS)

If you're utilizing the TransNexus in-line proxy (OpenSIPS) along with TransNexus CNAM and your Kazoo cluster, you might have observed that Kazoo removes brackets and spaces from `[V] NAME` in the `P-Asserted-Identity` header. This results in the call appearing as ` "VNAME" ` both in Kazoo and on the user's phone.

To address this concern, we've modified the OpenSIPS configuration on the in-line proxy to rewrite these headers.

## Options

We have three options:

1. **Option 1:** Pass the name as `[V]-NAME`, which will be displayed as `"V-NAME"` on the Kazoo side.
2. **Option 2:** Pass the name as `ツ-NAME`, displayed as `"ツ-NAME"` on the Kazoo side.
3. **Option 3:** Pass the name as `NAME`, displayed as `"NAME"` on the Kazoo side for all verified calls, and pass the name as `POSSIBLE SPAM`, displayed as `"POSSIBLE SPAM"` on the Kazoo side for all unsigned calls.

All options are included in this repository, labeled as "V-config", "Smile-config" and PossibleSpam-config."

## Implementation Steps

To implement either option, ensure you follow these steps:

1. Add the following line to your OpenSIPS configuration file:
`loadmodule "textops.so"`

2. Choose your preferred option and replace the entire `branch_route[1]` section in the original configuration with the chosen configuration.

Please feel free to explore both solutions and select the one that works best for you.

If you discover other characters that work or have any suggestions, please feel free to submit a Pull Request.
