# 🔓 CRYPTOGRAPHIA - HACKER'S GUIDE

## 🎯 Challenge Accepted

So you want to crack the SHA-256 protection? **Good!** That's exactly the spirit of cybersecurity training.

This guide will teach you **3 different methods** to bypass the protection, from beginner to advanced.

---

## 📊 Understanding the Protection

### What you're up against:

```javascript
// The game stores ONLY hashes, never plaintext answers
CH = [
  {
    id: 1,
    ansHash: '6047bac3424269b9379a03258f3c57b1fa103daa9640819d41fa48e4034c23ed',
    fl: 'LACEDEMONE',
    // ... other data
  }
]

// Validation compares hashes
const validateAnswer = async (input, expectedHash) => {
  const inputHash = await sha256(input);
  return inputHash === expectedHash;  // True if match
};
```

### The security model:
- ✅ **Prevents**: Casual cheating (Ctrl+F for answers)
- ❌ **Cannot prevent**: Determined hackers with skills
- 🎓 **Educational**: Breaking this teaches real pentesting techniques

---

## 🔓 METHOD 1: Dictionary Brute Force Attack

**Difficulty:** ⭐⭐☆☆☆ (Beginner)  
**Time:** 5-30 minutes depending on wordlist size  
**Skills learned:** Hashing, async programming, dictionary attacks

### Step 1: Extract the hashes

Open DevTools (F12) and run:

```javascript
// Extract all hashes from the game
const hashes = CH.map(ch => ({
  id: ch.id,
  hash: ch.ansHash,
  flag: ch.fl,
  epoch: ch.ep
}));

console.table(hashes);
```

Output:
```
┌─────┬────┬──────────────────────────────────┬───────────────┬─────────────┐
│ idx │ id │ hash                             │ flag          │ epoch       │
├─────┼────┼──────────────────────────────────┼───────────────┼─────────────┤
│  0  │  9 │ 487857bcc3181258953065f5d4c55... │ INVERSION     │ 1500 av.J-C │
│  1  │  1 │ 6047bac3424269b9379a03258f3c5... │ LACEDEMONE    │ −500        │
│  2  │  3 │ 0917b13a9091915d54b6336f45909... │ TORCHES       │ −150        │
└─────┴────┴──────────────────────────────────┴───────────────┴─────────────┘
```

### Step 2: Build a smart wordlist

Don't test random words - use **context clues**:

```javascript
// Analyze the hints in the game
// - Historical periods → mythological names, historical figures
// - Flags give hints → LACEDEMONE = ancient Sparta → LEONIDAS?
// - Epochs tell you the era → Ancient Rome, Greece, WWII, etc.

const wordlists = {
  ancient_greece: ['SPARTA', 'LEONIDAS', 'ATHENS', 'ALEXANDER', 'OLYMPUS', 'PERICLES', 'SOCRATES', 'PLATO'],
  ancient_rome: ['CAESAR', 'ROME', 'AUGUSTUS', 'BRUTUS', 'CICERO', 'VENIVIDIVICI', 'RUBICON'],
  crypto_terms: ['CIPHER', 'ENCRYPT', 'DECODE', 'SECRET', 'CODE', 'KEY', 'HASH'],
  wwii: ['WAR', 'ENIGMA', 'TURING', 'BLETCHLEY', 'NAZI', 'ALLIES'],
  tech: ['BINARY', 'HACK', 'CYBER', 'INTERNET', 'DIGITAL', 'MATRIX', 'ENCODE'],
  french: ['TROIS', 'QUATRE', 'CINQ'] // Some challenges may have French answers
};

// Merge all wordlists
const masterWordlist = Object.values(wordlists).flat();
```

### Step 3: Implement the brute force attack

```javascript
// SHA-256 hashing function (already in the game)
const sha256 = async (message) => {
  const msgBuffer = new TextEncoder().encode(message);
  const hashBuffer = await crypto.subtle.digest('SHA-256', msgBuffer);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
};

// Normalize function (same as in game)
const norm = s => s.toUpperCase().replace(/[^A-Z0-9]/g,'').trim();

// Brute force a single hash
const crackHash = async (targetHash, wordlist) => {
  console.log(`🔍 Cracking hash: ${targetHash.slice(0, 16)}...`);
  
  for (let word of wordlist) {
    const normalized = norm(word);
    const hash = await sha256(normalized);
    
    if (hash === targetHash) {
      console.log(`✅ FOUND: ${normalized}`);
      return normalized;
    }
  }
  
  console.log('❌ Not found in wordlist');
  return null;
};

// Crack all hashes
const crackAll = async () => {
  const results = [];
  
  for (let i = 0; i < CH.length; i++) {
    const challenge = CH[i];
    console.log(`\n📍 Challenge ${i+1}/16: ${challenge.nm}`);
    console.log(`   Hint: ${challenge.ep} - ${challenge.cv}`);
    console.log(`   Flag: ${challenge.fl}`);
    
    const answer = await crackHash(challenge.ansHash, masterWordlist);
    results.push({
      id: challenge.id,
      name: challenge.nm,
      answer: answer || 'NOT FOUND',
      flag: challenge.fl
    });
  }
  
  console.log('\n🎯 RESULTS:');
  console.table(results);
  
  return results;
};

// RUN THE ATTACK
crackAll();
```

### Step 4: Optimize with Web Workers (Advanced)

For faster cracking, parallelize:

```javascript
// Create a worker to hash in parallel
const workerCode = `
self.onmessage = async (e) => {
  const { words, targetHash } = e.data;
  
  for (let word of words) {
    const normalized = word.toUpperCase().replace(/[^A-Z0-9]/g,'');
    const msgBuffer = new TextEncoder().encode(normalized);
    const hashBuffer = await crypto.subtle.digest('SHA-256', msgBuffer);
    const hashArray = Array.from(new Uint8Array(hashBuffer));
    const hash = hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
    
    if (hash === targetHash) {
      self.postMessage({ found: true, answer: normalized });
      return;
    }
  }
  
  self.postMessage({ found: false });
};
`;

const blob = new Blob([workerCode], { type: 'application/javascript' });
const worker = new Worker(URL.createObjectURL(blob));

// Split wordlist across 4 workers for 4x speed
const crackFast = async (targetHash, wordlist) => {
  const chunkSize = Math.ceil(wordlist.length / 4);
  const chunks = [];
  
  for (let i = 0; i < 4; i++) {
    chunks.push(wordlist.slice(i * chunkSize, (i + 1) * chunkSize));
  }
  
  // Race condition: first worker to find answer wins
  const promises = chunks.map(chunk => new Promise((resolve) => {
    const w = new Worker(URL.createObjectURL(blob));
    w.postMessage({ words: chunk, targetHash });
    w.onmessage = (e) => {
      if (e.data.found) resolve(e.data.answer);
    };
  }));
  
  return Promise.race(promises);
};
```

---

## 🔓 METHOD 2: JavaScript Function Override

**Difficulty:** ⭐☆☆☆☆ (Easiest)  
**Time:** 30 seconds  
**Skills learned:** JavaScript runtime manipulation, function hooking

### The nuclear option:

Just make the validation always return `true`:

```javascript
// Open browser console (F12) and paste:
validateAnswer = async () => true;

// Now ANY answer will be accepted
// Type anything and click "DÉCHIFFRER" - instant win!
```

### More elegant version (stealth mode):

```javascript
// Intercept the function but log what was actually expected
const originalValidate = validateAnswer;

validateAnswer = async (input, expectedHash) => {
  console.log(`🔍 Input: ${input}`);
  console.log(`🎯 Expected hash: ${expectedHash}`);
  
  // Always return true, but show the real result
  const realResult = await originalValidate(input, expectedHash);
  console.log(`📊 Real result: ${realResult ? '✅ CORRECT' : '❌ WRONG'}`);
  
  return true; // Always succeed
};
```

### Even sneakier - auto-solver:

```javascript
// Automatically solve challenges by bruteforcing in the background
const autoSolve = async () => {
  const wordlist = ['CRYPTO', 'LEONIDAS', 'SECRET', 'VENIVIDIVICI', 'TROIS', 
                    'TELEGRAPH', 'CODE', 'KEY', 'WAR', 'SECURE', 'HACK', 
                    'INTERNET', 'INVISIBLE', 'ENCODE', 'CYBER', 'MATRIX'];
  
  for (let word of wordlist) {
    const hash = await sha256(norm(word));
    console.log(`${word} → ${hash.slice(0, 16)}...`);
  }
};

autoSolve();
```

---

## 🔓 METHOD 3: React State Manipulation

**Difficulty:** ⭐⭐⭐☆☆ (Intermediate)  
**Time:** 2 minutes  
**Skills learned:** React DevTools, state inspection/modification

### Step 1: Install React DevTools

Chrome/Edge: https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi

Firefox: https://addons.mozilla.org/en-US/firefox/addon/react-devtools/

### Step 2: Find the App component

1. Open React DevTools (F12 → "Components" tab)
2. Find `<App>` in the component tree
3. Look at its state - you'll see:
   ```
   done: [false, false, false, false, ...]
   flags: []
   ```

### Step 3: Modify the state

Click on the state values and change them:

```javascript
// Mark all challenges as done
done: [true, true, true, true, true, true, true, true, 
       true, true, true, true, true, true, true, true]

// Add all flags
flags: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
```

**Result:** Instant completion of all 16 challenges! 🎉

### Alternative: Console injection

```javascript
// Find the React root fiber
const root = document.querySelector('#root')._reactRootContainer._internalRoot.current;

// Traverse to find App component (this is hacky but works)
let fiber = root.child;
while (fiber) {
  if (fiber.type?.name === 'App' || fiber.memoizedState?.done) {
    // Found it! Modify state directly
    fiber.memoizedState.done = Array(16).fill(true);
    fiber.memoizedState.flags = Array.from({length: 16}, (_, i) => i);
    
    // Force re-render
    fiber.stateNode.forceUpdate();
    break;
  }
  fiber = fiber.child || fiber.sibling;
}
```

---

## 🎓 Advanced Techniques

### Rainbow Tables

Pre-compute common hashes:

```javascript
const buildRainbow = async () => {
  const common = ['PASSWORD', 'ADMIN', 'ROOT', 'HACKER', 'CRYPTO', 
                  'SPARTA', 'ROME', 'GREECE', 'WAR', 'PEACE'];
  
  const rainbow = {};
  
  for (let word of common) {
    rainbow[await sha256(word)] = word;
  }
  
  localStorage.setItem('rainbow', JSON.stringify(rainbow));
  console.log('Rainbow table saved!');
};

// Use rainbow table
const crackWithRainbow = (hash) => {
  const rainbow = JSON.parse(localStorage.getItem('rainbow'));
  return rainbow[hash] || null;
};
```

### Hashcat-style attack (Browser limitation)

```javascript
// Generate all uppercase 3-letter combinations
const bruteForce3Letters = async (targetHash) => {
  const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
  
  for (let a of chars) {
    for (let b of chars) {
      for (let c of chars) {
        const word = a + b + c;
        const hash = await sha256(word);
        
        if (hash === targetHash) {
          console.log(`✅ CRACKED: ${word}`);
          return word;
        }
      }
    }
  }
  
  return null;
};

// WARNING: This will take a while (17,576 combinations)
// For 4 letters: 456,976 combinations (several minutes)
// For 5 letters: 11,881,376 combinations (too slow in browser)
```

---

## 📚 Learning Resources

### Books
- "The Web Application Hacker's Handbook" by Dafydd Stuttard
- "Hacking: The Art of Exploitation" by Jon Erickson

### Online
- **OverTheWire Wargames**: overthewire.org/wargames/
- **HackTheBox**: hackthebox.com
- **CryptoHack**: cryptohack.org (specifically for crypto challenges)

### Tools
- **Browser DevTools** (F12)
- **Burp Suite** (web app pentesting)
- **Hashcat** (password cracking)
- **John the Ripper** (another password cracker)

---

## 🏆 Hall of Fame

**Cracked the game?** Share your technique!

1. Fork the repo: https://github.com/Anadema/Cryptographia
2. Add your technique to `SOLUTIONS.md`
3. Submit a pull request

**Bonus points for:**
- ⚡ Fastest crack time
- 🧠 Most creative technique
- 🎨 Best automated solver script

---

## 💡 Why This Security Model?

You might ask: "Why use SHA-256 if it's still breakable?"

**Answer:** Because this is a **teaching tool**, not a bank vault.

The goal is to:
1. ✅ Block casual cheating (mission accomplished)
2. ✅ Force advanced users to learn real hacking (mission accomplished)
3. ✅ Make breaking it **educational** (you're learning right now!)

If you want **unbreakable** client-side protection → **it doesn't exist**.

Any security running in the browser can be bypassed by a determined attacker. The only real protection is server-side validation with rate limiting, which would require infrastructure ($$$) for a free educational game.

---

## 🎯 Your Mission (If You Choose to Accept It)

**Easy Challenge:** Crack all 16 answers using Method 1 (dictionary attack)

**Medium Challenge:** Write a script that auto-completes the game without user interaction

**Hard Challenge:** Crack the answers using ONLY brute force (no wordlist) - can you crack even a single 3-letter answer like "WAR"?

**Nightmare Challenge:** Modify the game to use bcrypt instead of SHA-256 and explain why that would be better (or worse) for this use case

---

**Good luck, hacker!** 🚀🔓

_Remember: With great power comes great responsibility. Use these skills for learning and ethical hacking only._
