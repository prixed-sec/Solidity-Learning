# Solidity & Smart Contract Security Learning

My journey learning Solidity, EVM internals, and Smart Contract Security.

## 📚 Progress Tracker

### CryptoZombies
- [x] Lesson 1: Making the Zombie Factory (`ZombieFactory.sol`)
- [x] Lesson 2: Zombies Attack Their Victims (`Lesson2_ZombieFeeding.sol`)
- [ ] Lesson 3: Advanced Solidity Concepts
- [ ] Lesson 4: Zombie Battle System
- [ ] Lesson 5: ERC721 & Crypto-Collectibles
- [ ] Lesson 6: App Front-ends & Web3.js

---

## 🔍 Security Notes & Observations

### Lesson 1 — `ZombieFactory.sol`
Even in basic contracts, several security considerations stand out:
* **Outdated Compiler & Floating Pragma (`^0.4.19`):** Versions prior to Solidity `0.8.0` lack built-in overflow/underflow checks. In production, a locked pragma (e.g., `0.8.20`) is preferred.
* **Deterministic Randomness (`keccak256(_str)`):** DNA generation relies solely on user input (`_name`), making the outcome completely predictable before submitting a transaction.
* **Unrestricted Access (`public`):** `createRandomZombie` has no rate-limiting or ownership checks, allowing anyone to spam the `zombies` array infinitely.

### Lesson 2 — `Lesson2_ZombieFeeding.sol`
Interacting with external contracts introduces new attack surfaces:
* **Hardcoded External Address (`ckAddress`):** The CryptoKitties address is hardcoded directly into the state without immutability or an admin setter function, making it impossible to update if the external protocol migrates.
* **Legacy Interface Syntax:** Uses `contract KittyInterface` instead of the modern `interface` keyword, and relies on legacy `keccak256(_species)` without `abi.encodePacked()`.
* **Off-Chain Centralization Risk:** The Web3 front-end relies on a centralized HTTP API (`api.cryptokitties.co`) to fetch metadata and images.
