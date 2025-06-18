# eBase32 – Technical Specification

This document defines the formal specification of the eBase32 encoding standard.

## Motivation

eBase32 was created to provide a Base32 encoding that is:
- free of ambiguous characters (e.g. `0`, `O`, `I`, `l`, `S`, `5`)
- URL-safe with no special characters
- human-friendly and copy-safe
- suitable for IDs, tokens, and infrastructure applications

---

## Character Set

eBase32 uses the following 32 characters:

```
ACEFHKLMNPRTWXYadeghknrtwxy34679
```

All characters are:
- strictly alphanumeric (no symbols)
- visually distinct in most fonts
- resistant to human input and copy/paste errors
- ASCII and Unicode compatible

---

## Encoding Process

### Step 1: Convert bytes to bit stream
All input bytes are converted to a single bit stream (8 bits per byte).

### Step 2: Group into 5-bit blocks
The bit stream is split into 5-bit chunks. Each 5-bit group represents an integer from `0` to `31`.

### Step 3: Map values to characters
Each 5-bit value is used as an index into the eBase32 character set. The corresponding character is appended to the output string.

### Step 4: Pad remaining bits
If bits remain at the end, they are left-shifted and zero-padded to form a complete 5-bit group.

---

## Padding

eBase32 **does not use padding** (e.g., no `=`).

---

## Comparison to Other Standards

| Standard        | Charset      | URL-safe | No Ambiguity       | Notes                      |
|----------------|--------------|----------|---------------------|-----------------------------|
| Base32 (RFC)   | A–Z, 2–7     | Yes      | ❌ No               | Includes `I`, `1`, `O`, `0` |
| Crockford      | 0–9, A–Z     | Yes      | ⚠️ Partial          | Fuzzy input handling        |
| z-base-32      | custom       | Yes      | ⚠️ Partial          | Includes edge cases         |
| **eBase32**    | fixed 32     | ✅ Yes   | ✅ Yes              | Strict, deterministic       |

---

## License

eBase32 is freely usable under the MIT License.

Reference implementation available at: [GitHub – Endkind/eBase32](https://github.com/Endkind/eBase32)
