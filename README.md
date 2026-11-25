# Solidity & Smart Contract Security Learning

My journey learning Solidity, EVM internals, and Smart Contract Security.

## 📚 Progress Tracker

### CryptoZombies
- [x] **Lesson 1:** Making the Zombie Factory (`ZombieFactory.sol`)
- [ ] **Lesson 2:** Zombies Attack Their Victims
- [ ] **Lesson 3:** Advanced Solidity Concepts
- [ ] **Lesson 4:** Zombie Battle System
- [ ] **Lesson 5:** ERC721 & Crypto-Collectibles
- [ ] **Lesson 6:** App Front-ends & Web3.js

---

## 🔍 Security Notes & Observations

### Lesson 1 — `ZombieFactory.sol`
Even in basic contracts, several security considerations stand out:
* **Outdated Compiler & Floating Pragma (`^0.4.19`):** Versions prior to Solidity `0.8.0` lack built-in overflow/underflow checks. In production, a locked pragma (e.g., `0.8.20`) is preferred.
* **Deterministic Randomness (`keccak256(_str)`):** DNA generation relies solely on user input (`_name`), making the outcome completely predictable before submitting a transaction.
* **Unrestricted Access (`public`):** `createRandomZombie` has no rate-limiting or ownership checks, allowing anyone to spam the `zombies` array infinitely.
