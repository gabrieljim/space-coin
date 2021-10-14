https://github.com/gabrieljim/space-coin

The following is a micro audit of git commit 33c8a61a72f68444c335aff909f048d0e469ff83 by Gilbert.


## General comments

- The ICO and ERC-20 are usually not the same contract. It's not necessarily wrong to put them together, but be aware it's unconventional.


## issue-1

**[High]** Tax is not applied on all transfers

SpaceCoin.sol's `transfer` override does not apply to `transferFrom` calls.


## issue-2

**[High]** mint() and burn() incorrectly convert units

Both mint() and burn() multiply by decimals before operating. This make it impossible to mint fractional SPC, and mints many orders of magnitude more than intended on line 31.


## Nitpicks

- MAX_SUPPLY should be a constant to save on gas/storage costs.
- `isPaused` should be named something like `notPaused` to better describe the requirement.
- The `else if` in SpaceCoin.sol:83 can be simplified to an `else`
- In transfer(), consider only doing a second transfer if isTaxOn is set to true.