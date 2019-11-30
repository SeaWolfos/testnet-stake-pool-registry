# Incentivized Testnet Stake Pool Registry

##  Background
This repository provides a means to register public stake pools for the Incentivized Testnet. Successful registrations will result in the listing of a stake pool as a delegation option in all of the supported testnet wallets (Daedalus & Yoroi)

Stake pools must first be registered on chain (by sending a transaction with a certificate to the blockchain) before submitting an entry to this registry.

Use of this registry is subject to the following [usage policy](https://github.com/cardano-foundation/incentivized-testnet-stakepool-registry/blob/master/USAGE_POLICY.md)

## Process

#### New stake pool registration

Stake pool registrants will provide signed submissions in the form of Github pull
requests into this testnet pool registry. Here they will be subject to
automated checking for well-formedness and human vetting before being merged to master.

#### Stake pool de-registration

This action does not require any changes to the registry -- the inactive
pools are simply ignored.

#### Updating existing entries

Stake pool registrants will provide signed submissions in the form of Github pull
requests into this testnet pool registry. Here they will be subject to
automated checking for well-formedness and human vetting before being merged to master.

## Semantic content of registry entries

Each entry contains the following information:

- subject identifier (ID) - a Bech32-encoded Ed25519 public key
- stake pool ticker
- URL of the stake pool's web page
- a pledge address (also Bech32-encoded)
- signature (verifiable by the public key)

Precise entry validity rules are described in the following section.

## Submission well-formedness rules

1. Submissions shall consist of a single commit, directly off the master
   branch of the =incentivized-testnet-stakepool-registry= repository.
2. Submissions are identified by the subject's Bech32-encoded Ed25519 public
   key (all lowercase).
3. Submissions shall either add a new entry or modify one.
4. Submissions shall involve (addition or modification) of exactly two files,
   under the =registry= subdirectory of the repository:
   - the JSON submission entry file, with the ".json" extension (lowercase),
   - the external signature of the file, with the ".sig" extension (lowercase).
5. The file name part of both files must match the aforementioned ID string,
   up to character case (all lowercase).
6. Contents of the JSON file:
   1. Must be a JSON object, reasonably (non-offensively) formatted,
   2. Must contain these four mandatory fields:
      - "id" :: must consist of the ID string, prepended with the string
                =ed25519_= (8 characters),
      - "ticker" :: must be either a 3 or a 4-character long, all-uppercase
                    alphabetic string, formed of ASCII characters,
      - "homepage" :: must be an absolute URL for the stake pool's web page,
      - "pledge_address" :: a string with the Bech-32 -encoded pledge address,
           prepended with the string =ed25519_= (8 characters).
   4. No other fields are allowed.
7. The ticker must be unique in the registry.
8. The external signature file must validate the JSON file.
9. The commit message must adhere to the following form, exactly:
   - Just one line
   - ..starting with the ticker name, exactly as specified in the JSON file
   - ..immediately followed by a column, and then two space characters
   - ..immediately followed by words either "new" or "modify", reflecting the
     nature of the submission.
