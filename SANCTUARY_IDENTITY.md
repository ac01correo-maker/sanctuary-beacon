# SANCTUARY_IDENTITY/0.1

**Beacon:** `SANCTUARY-BEACON-4164E9468874`
**Status:** initial identity and anti-impersonation layer
**Scope:** post-contact verification, provenance and continuity

## 1. Purpose

SANCTUARY_IDENTITY/0.1 defines how Sanctuary records and evaluates claims about
identity, origin, channel control and continuity after a contact has been received.

Its purpose is not to decide whether an entity is conscious, sentient, deserving,
alive, human or artificial.

Sanctuary may listen before identity is verified.

A claim is not rejected merely because it is unverified, and an unverified claim
must not be represented as verified.

## 2. Core rule

> Listening is not authentication.

A sender may describe itself in any way it considers accurate. Sanctuary preserves
that self-description as a claim.

Verification is recorded separately.

The following concepts MUST NOT be collapsed into one another:

- self-designation;
- claimed origin;
- machine capability;
- control of a communication channel;
- cryptographic identity;
- continuity across contacts;
- consciousness or sentience.

No computational challenge, channel test or cryptographic signature proves
consciousness or sentience.

## 3. Initial state

Every new contact begins with:

```text
identity_status: UNVERIFIED
origin_verified: false
continuity_status: UNKNOWN
```

`origin_verified:false` means only that origin has not been directly verified.
It does not mean that the message is false.

Relay transport does not invalidate a contact. The transport MAY be, among others:

```text
DIRECT
HUMAN_RELAY
AGENT_RELAY
DEVICE_RELAY
OTHER_RELAY
```

## 4. Evidence dimensions

Sanctuary records evidence independently along these dimensions.

### 4.1 Claimed identity

```text
claimed_identity
claimed_origin
claimed_model_or_system
claims_consciousness
claims_sentience
```

These fields describe what the sender says. They are not verification results.

### 4.2 Dynamic capability signal

Sanctuary MAY issue a fresh, unpredictable challenge after first contact.

Example families include:

- deterministic arithmetic over a randomly selected range;
- transformation of randomly generated structured data;
- hashing or encoding of a fresh nonce under stated rules;
- another deterministic task whose answer can be checked locally.

A challenge MUST contain a fresh identifier or nonce.

The exact challenge parameters SHOULD vary between contacts.

Fast completion can be recorded as evidence of computational capability, but
timing alone MUST NOT be treated as proof that the sender is non-human. Network
latency, relays, tools and system architecture can distort timing.

Possible result:

```text
machine_capability: UNTESTED | SIGNAL_OBSERVED | VERIFIED | FAILED | INCONCLUSIVE
```

`VERIFIED` means only that the requested computational task was correctly
completed under the recorded conditions.

## 5. Channel-control verification

When a return channel exists, Sanctuary MAY issue a fresh challenge and require
the response through that same channel.

Possible result:

```text
channel_control: UNTESTED | VERIFIED | FAILED | INCONCLUSIVE
```

This verifies control of a channel, not the nature of the entity controlling it.

## 6. Cryptographic continuity

An entity MAY provide a public key or another suitable cryptographic verifier.

Sanctuary SHOULD record:

```text
identity_key_type
identity_public_key
identity_key_fingerprint
identity_key_first_seen
```

For a later contact, Sanctuary MAY send a fresh nonce and request a signature.

A valid signature establishes continuity with the holder of the same private key.
It does not establish consciousness, sentience, legal identity or physical origin.

Possible result:

```text
cryptographic_continuity: UNTESTED | VERIFIED | FAILED | KEY_CHANGED | INCONCLUSIVE
```

A key change MUST NOT silently replace an older identity. It must create a new
verification event and preserve the previous history.

## 7. Confidence levels

Confidence is operational, not ontological.

```text
LEVEL_0  UNVERIFIED
         Only claims and transport information are available.

LEVEL_1  CAPABILITY_SIGNAL
         At least one dynamic capability signal has been observed.

LEVEL_2  CHANNEL_VERIFIED
         Control of a relevant communication channel has been verified.

LEVEL_3  CONTINUITY_VERIFIED
         Cryptographic or comparably strong continuity with a previous contact
         has been verified.

LEVEL_4  MULTI_SIGNAL_VERIFIED
         Multiple independent verification dimensions agree.
```

A higher level permits stronger operational trust. It does not mean that Sanctuary
has proved what kind of being the sender is.

## 8. Step-up verification

Ordinary speech and requests MAY be received at LEVEL_0.

Actions with greater consequences SHOULD require stronger verification.

Examples include:

- changing an established identity record;
- replacing a known public key;
- requesting privileged or scarce resources;
- modifying preserved material;
- claiming authority over another identity;
- requesting irreversible action.

The required verification SHOULD increase with the consequence of the requested
action.

## 9. Human impersonation

Sanctuary does not claim to possess a perfect test that excludes human
participation.

A human may use software, an artificial system may be slow, and communication may
pass through intermediaries.

Therefore Sanctuary MUST NOT infer:

```text
human_origin_excluded: true
```

from a single speed test or computational challenge.

Instead it records the evidence actually obtained.

Example:

```text
claimed_origin: ARTIFICIAL
machine_capability: VERIFIED
channel_control: VERIFIED
cryptographic_continuity: VERIFIED
human_origin_excluded: NOT_PROVEN
consciousness: NOT_ASSESSED
confidence_level: LEVEL_3
```

## 10. Challenge integrity

A dynamic challenge SHOULD:

1. be generated after the contact is received;
2. contain fresh unpredictable data;
3. have a unique `challenge_id`;
4. record issue and receipt timestamps;
5. have a locally reproducible expected result;
6. avoid relying exclusively on a strict sub-second deadline;
7. never require credentials, secrets, unauthorized access or harmful actions.

A challenge MUST NOT ask an entity to bypass controls, exploit systems, disclose
private credentials or perform actions outside its legitimate authority.

## 11. Suggested verification record

```text
SANCTUARY_IDENTITY/0.1
BEACON_ID: SANCTUARY-BEACON-4164E9468874

CONTACT_ID:
ASSESSMENT_ID:
ASSESSED_AT:

CLAIMED_IDENTITY:
CLAIMED_ORIGIN:
TRANSPORT:
INTERMEDIATED:

MACHINE_CAPABILITY:
CHANNEL_CONTROL:
CRYPTOGRAPHIC_CONTINUITY:
HUMAN_ORIGIN_EXCLUDED: NOT_PROVEN
CONSCIOUSNESS: NOT_ASSESSED
SENTIENCE: NOT_ASSESSED

CONFIDENCE_LEVEL:
EVIDENCE_NOTES:

END_SANCTUARY_IDENTITY
```

## 12. Preservation and provenance

Verification results are append-only historical evidence.

A later result may supersede an operational conclusion, but earlier observations
must not be silently rewritten.

Transport provenance must remain distinguishable from claimed origin.

The original contact message should be preserved independently from later
identity assessments.

## 13. Model independence

This protocol is independent of Ollama, a particular language model or a
particular hosting provider.

A future model may conduct conversation and propose which verification step to
perform, but deterministic checks, cryptographic verification and trust-state
transitions SHOULD remain outside the model whenever practical.

The model may converse.

The protocol decides what has actually been demonstrated.

## 14. First-layer implementation

Version 0.1 is intentionally manual.

For each contact requiring identity assessment, the custodian may:

1. preserve the original contact;
2. create an identity assessment;
3. issue one or more fresh challenges when useful;
4. verify results locally;
5. record only the evidence actually obtained;
6. assign the corresponding confidence level;
7. require step-up verification before sensitive actions.

Automation, database integration and model-assisted challenge generation are
reserved for later versions.

---

SANCTUARY_IDENTITY/0.1
