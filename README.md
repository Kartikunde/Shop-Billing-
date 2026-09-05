You are a senior full-stack engineer, AI agent engineer, Web3 developer, UI/UX designer, and hackathon architect.

Build a complete, polished, production-style hackathon MVP called **SkillMint**.

# 1. PRODUCT VISION

SkillMint is an AI-powered skill verification platform.

The core concept is:

> **"Don't just claim your skills. Prove them."**

Instead of allowing users to simply upload certificates or add skills to LinkedIn, SkillMint uses an AI interviewer to actually test the user's knowledge through an adaptive conversational assessment.

After successfully passing the assessment:

1. AI evaluates the candidate.
2. A deterministic scoring system calculates the final score.
3. The system determines the skill level.
4. The backend creates a cryptographic assessment hash.
5. The backend authorizes the successful assessment.
6. The user connects their crypto wallet.
7. A smart contract mints a verifiable NFT skill badge on the **Polygon Amoy testnet**.
8. The user receives a public verification page that anyone can use to verify the credential.

The complete flow must be:

USER
→ SELECT SKILL
→ CONNECT WALLET
→ AI INTERVIEW
→ ADAPTIVE QUESTIONS
→ AI EVALUATION
→ DETERMINISTIC SCORE
→ PASS/FAIL
→ SIGNED VERIFICATION
→ NFT MINT
→ PUBLIC VERIFICATION PAGE

# 2. HACKATHON MVP SCOPE

Do NOT overbuild.

The primary MVP should support ONE skill initially:

**JavaScript**

Assessment level:

**Intermediate**

The architecture must be designed so additional skills can be added later.

Do NOT initially build:

* Mobile application
* DAO
* Token economy
* NFT marketplace
* Multiple blockchains
* Complex social network
* 20 different skills
* Complex gamification

Focus on making the core experience extremely polished.

# 3. TECH STACK

Use the following architecture.

## Frontend

* Next.js
* React
* TypeScript
* Tailwind CSS
* Modern responsive UI
* wagmi
* RainbowKit
* viem

## Backend

Use:

* Python
* FastAPI
* Uvicorn

Backend responsibilities:

* AI interviewer
* Conversation state
* Answer evaluation
* Scoring
* Assessment management
* Cryptographic hashing
* Verification authorization
* Blockchain interaction

## Database

Use:

* Firebase Firestore

Store:

* users
* assessments
* questions
* answers
* evaluation results
* scores
* verification status
* badge information
* transaction hashes

## AI

Use an LLM API.

Make the LLM provider configurable through environment variables.

The AI must behave as an adaptive technical interviewer rather than a simple chatbot.

## Blockchain

Use:

* Solidity
* OpenZeppelin
* ERC-721
* Polygon Amoy testnet

The smart contract must support secure NFT badge minting.

# 4. PROJECT STRUCTURE

Create a clean monorepo:

skillmint/

```
frontend/
    app/
    components/
    hooks/
    lib/
    public/
    types/

backend/
    main.py
    agent.py
    evaluator.py
    scoring.py
    blockchain.py
    database.py
    models.py
    config.py
    requirements.txt

contracts/
    SkillMint.sol
    scripts/
    test/

README.md

.env.example
```

Keep frontend, backend, and smart contract code modular.

# 5. FRONTEND PAGES

Create the following pages.

## Landing Page

Route:

/

Design a premium Web3 + AI interface.

Hero section:

SKILLMINT

"Prove your skills.
Don't just claim them."

Subtitle:

"AI-powered skill assessments with blockchain-verifiable credentials."

Primary CTA:

"Start Assessment"

Secondary CTA:

"Verify a Badge"

Include sections explaining:

1. AI Assessment
2. Adaptive Interview
3. Verified Score
4. Blockchain Credential

Include a simple process:

ASSESS
→ VERIFY
→ MINT
→ SHARE

Add a polished footer.

# 6. ASSESSMENT PAGE

Route:

/assessment

At the beginning show:

Skill:
JavaScript

Level:
Intermediate

Number of questions:
5–7 adaptive questions

Button:

"Start Assessment"

Once started, display a conversational AI interview interface.

Example:

AI Interviewer:

"Let's begin with a basic JavaScript question.

What is the difference between let, const and var?"

User types answer.

After submission, AI evaluates the response and generates the next question.

The interface should feel like a real technical interview.

Features:

* Chat bubbles
* AI typing indicator
* Question number
* Progress indicator
* Answer input
* Submit button
* Timer
* Assessment status
* Exit protection

Do not show the final score until the assessment is complete.

# 7. AI AGENT BEHAVIOR

The AI must be an adaptive interviewer.

System prompt concept:

"You are SkillMint's technical interviewer.

Your purpose is to determine whether the candidate genuinely understands JavaScript.

Ask one question at a time.

Start with intermediate-level questions.

After each response:

1. Analyze correctness.
2. Analyze technical depth.
3. Identify misconceptions.
4. Determine whether the next question should become harder, easier, or remain at the same level.
5. Ask a relevant follow-up question when appropriate.
6. Never reveal the correct answer during the assessment.
7. Do not give the candidate the final score until the assessment is complete.

Do not simply ask a fixed list of questions.

Adapt the interview based on the candidate's answers."

The AI should test concepts such as:

* Variables
* let / const / var
* Scope
* Closures
* Functions
* Promises
* Async/await
* Event loop
* DOM
* Arrays
* Objects
* Error handling
* ES6 concepts

Questions should adapt based on demonstrated ability.

# 8. STRUCTURED AI EVALUATION

Do not rely on free-form AI text for scoring.

The AI should return structured JSON.

Example:

{
"correctness": 8,
"depth": 7,
"reasoning": 9,
"communication": 8,
"next_difficulty": "hard",
"follow_up_needed": true,
"confidence": 0.91,
"feedback": "Candidate demonstrates strong understanding of closures."
}

Validate the JSON using a schema.

Never trust malformed AI output.

# 9. FINAL SCORING SYSTEM

Use a deterministic scoring system.

Categories:

Technical Knowledge = 40%

Problem Solving = 30%

Accuracy = 20%

Communication = 10%

Example:

Technical Knowledge = 85
Problem Solving = 80
Accuracy = 90
Communication = 75

Final score:

85 × 0.40

* 80 × 0.30
* 90 × 0.20
* 75 × 0.10

= 83.5

Round to the nearest integer.

Levels:

0–49:
Beginner

50–69:
Developing

70–84:
Proficient

85–100:
Advanced

Pass threshold:

70%

If score >= 70:

status = VERIFIED

If score < 70:

status = NOT_VERIFIED

Only VERIFIED users can mint a badge.

# 10. RESULT PAGE

Route:

/result

Show an impressive result dashboard.

Example:

ASSESSMENT COMPLETE

JavaScript

86 / 100

ADVANCED

✓ VERIFIED

Display:

Technical Knowledge
88

Problem Solving
84

Accuracy
90

Communication
78

Also show:

Questions completed:
7

Assessment ID:
SM-10492

Assessment date:
September 5, 2026

If the user passed, show:

"MINT YOUR SKILL BADGE"

If failed:

"Assessment not passed"

and:

"Try Again"

Do not allow NFT minting for failed assessments.

# 11. CRYPTOGRAPHIC VERIFICATION

Do NOT put the entire interview or private user answers on-chain.

Create an assessment record containing:

* Assessment ID
* Skill
* Score
* Level
* Assessment date
* Verification status

Generate a SHA-256 hash of the canonical assessment data.

Example concept:

assessment data
→ canonical JSON
→ SHA-256
→ assessmentHash

Store the hash with the assessment.

The hash should be included in the blockchain verification process.

The system should be able to prove that the assessment record was not changed after verification.

# 12. BACKEND AUTHORIZATION

The backend must authorize badge minting only for successful assessments.

Flow:

Assessment completed
↓
Score calculated
↓
Score >= 70
↓
Assessment hash generated
↓
Backend signs authorization
↓
Wallet submits mint transaction
↓
Smart contract verifies authorization
↓
NFT minted

Never allow an arbitrary frontend user to call a public unrestricted mint function.

# 13. SMART CONTRACT

Create:

contracts/SkillMint.sol

Use OpenZeppelin ERC-721.

The NFT represents a verified skill credential.

Required information:

* Token ID
* Candidate wallet
* Skill
* Score
* Level
* Assessment hash
* Metadata URI

The contract must restrict minting.

Only the authorized verifier/backend should be able to authorize a badge.

Use appropriate access control and signature verification.

Do not hardcode private keys.

Use environment variables for sensitive values.

Add Solidity tests for:

* Successful mint
* Unauthorized mint rejection
* Invalid signature rejection
* Duplicate/invalid authorization
* Correct metadata
* Correct assessment hash

# 14. NFT METADATA

Create metadata similar to:

{
"name": "SkillMint — Advanced JavaScript",
"description": "AI-verified JavaScript skill credential.",
"image": "ipfs://...",
"attributes": [
{
"trait_type": "Skill",
"value": "JavaScript"
},
{
"trait_type": "Level",
"value": "Advanced"
},
{
"trait_type": "Score",
"value": 86
},
{
"trait_type": "Assessment",
"value": "AI Adaptive Interview"
},
{
"trait_type": "Network",
"value": "Polygon Amoy"
}
]
}

Do not expose private interview answers in NFT metadata.

# 15. WALLET CONNECTION

Use RainbowKit + wagmi.

Support a common wallet such as MetaMask.

The user should:

1. Click Connect Wallet.
2. Connect wallet.
3. See shortened wallet address.
4. Start assessment.
5. After passing, click Mint Badge.
6. Confirm transaction.
7. See transaction status.
8. See successful mint.

Show states:

CONNECTING

WAITING FOR SIGNATURE

MINTING

CONFIRMED

FAILED

# 16. BADGE PAGE

Route:

/badge/[tokenId]

Create a beautiful NFT credential card.

Example:

---

✓ VERIFIED SKILL

JavaScript

ADVANCED

86 / 100

AI ASSESSED

Assessment ID:
SM-10492

Polygon Amoy

Token #10492

[View Blockchain Proof]

---

Show transaction hash and contract address.

# 17. PUBLIC VERIFICATION PAGE

Route:

/verify/[assessmentId]

This is extremely important.

Anyone should be able to open a verification URL without logging in.

Example:

SKILLMINT VERIFICATION

✓ VERIFIED

JavaScript

Advanced

Score:
86%

Assessment:
AI Adaptive Interview

Assessment ID:
SM-10492

Assessment Date:
September 5, 2026

Blockchain:
Polygon Amoy

Assessment Hash:
0x...

Token ID:
10492

Wallet:
0x7A...92F

[View Blockchain Proof]

The verification page should clearly explain:

"This credential confirms that the holder successfully completed a SkillMint AI assessment. The assessment record is cryptographically linked to the blockchain credential."

# 18. VERIFY BLOCKCHAIN DATA

The verification page should compare:

Database assessment hash
VS
Blockchain assessment hash

If they match:

✓ Blockchain Verified

If they don't:

⚠ Verification mismatch

Never display "verified" if the blockchain proof does not match.

# 19. DATABASE MODEL

Create Firestore collections.

users

{
walletAddress,
createdAt
}

assessments

{
assessmentId,
walletAddress,
skill,
level,
status,
score,
categoryScores,
questions,
answers,
assessmentHash,
createdAt,
completedAt
}

badges

{
assessmentId,
tokenId,
walletAddress,
skill,
score,
level,
contractAddress,
transactionHash,
metadataURI,
assessmentHash,
mintedAt
}

Do not store unnecessary private information.

# 20. API DESIGN

Implement:

POST /assessment/start

Creates an assessment.

POST /assessment/message

Accepts:

{
"assessmentId": "...",
"message": "candidate answer"
}

Returns:

{
"question": "...",
"evaluation": {...},
"progress": 3
}

POST /assessment/finish

Finalizes the assessment and calculates deterministic score.

Returns:

{
"assessmentId": "...",
"score": 86,
"level": "Advanced",
"status": "VERIFIED",
"assessmentHash": "..."
}

POST /badge/authorize

Creates a secure authorization for an eligible assessment.

GET /assessment/{assessmentId}

Returns assessment information.

GET /badge/{tokenId}

Returns badge information.

GET /verify/{assessmentId}

Returns public verification information.

# 21. SECURITY

Follow good security practices.

Never expose:

* API keys
* Private keys
* Firebase service account credentials
* Backend signing keys

Use .env files.

Create:

.env.example

Include placeholders such as:

LLM_API_KEY=
FIREBASE_PROJECT_ID=
FIREBASE_PRIVATE_KEY=
FIREBASE_CLIENT_EMAIL=
POLYGON_RPC_URL=
CONTRACT_ADDRESS=
SIGNER_PRIVATE_KEY=

Never commit .env.

Add .gitignore.

Validate all API input.

Validate wallet addresses.

Prevent users from minting badges for another user's assessment.

Prevent duplicate badge minting.

Prevent score manipulation from frontend.

The backend must be the source of truth for assessment scores.

# 22. UI/UX DESIGN

Make the interface look like a serious modern startup rather than a basic student project.

Design direction:

* Premium
* Minimal
* Futuristic
* AI + Web3
* Clean typography
* Subtle gradients
* Glassmorphism used carefully
* Smooth animations
* Responsive design
* Dark mode as primary theme

Use cards, progress indicators, badges, status indicators, and subtle motion.

Avoid excessive animations.

Make the assessment interface extremely easy to understand.

The result page should feel rewarding.

The NFT badge should look professional and shareable.

# 23. ERROR HANDLING

Handle:

* AI API failure
* Invalid AI response
* Network failure
* Wallet rejection
* Wrong blockchain network
* Smart contract failure
* Firebase failure
* Duplicate mint
* Assessment timeout
* Invalid assessment ID

Display human-readable errors.

Never expose stack traces to users.

# 24. DEMO MODE

Because this is a hackathon project, implement a controlled demo mode.

Create:

DEMO MODE

This should allow the team to demonstrate the complete flow quickly.

However, do not fake blockchain verification.

If demo mode is enabled:

* Use seeded assessment data where appropriate.
* Still show the real architecture.
* If possible, mint a real NFT on Polygon Amoy.

Clearly label demo/testnet data as such.

# 25. HACKATHON DEMO FLOW

Optimize the application for a 2–3 minute live demonstration.

The ideal demo:

1. Open SkillMint.
2. Click Start Assessment.
3. Connect MetaMask.
4. Start JavaScript interview.
5. Answer 5–7 questions.
6. Show AI adapting questions.
7. Finish assessment.
8. Display score:
   86%
9. Display:
   ✓ VERIFIED
10. Click:
    MINT SKILL BADGE
11. Confirm wallet transaction.
12. Show:
    NFT MINTED
13. Open:
    /verify/SM-10492
14. Show blockchain verification.
15. Click blockchain explorer link.

The entire flow should be smooth and visually impressive.

# 26. IMPORTANT PRODUCT MESSAGE

The UI should repeatedly communicate the central distinction:

Traditional credential:

"I completed a course."

SkillMint:

"I demonstrated the skill."

Use messaging such as:

"Certificates prove completion.
SkillMint proves capability."

Do not claim that AI assessment guarantees a person's real-world competence. Describe it accurately as an AI-based assessment and verification credential.

# 27. README

Create a complete README containing:

* Project overview
* Problem
* Solution
* Features
* Architecture
* Tech stack
* AI agent workflow
* Scoring methodology
* Blockchain architecture
* Smart contract explanation
* Database schema
* API documentation
* Local setup
* Environment variables
* Firebase setup
* Polygon Amoy setup
* Wallet setup
* Contract deployment
* Frontend setup
* Backend setup
* Testing
* Demo instructions
* Future improvements

# 28. DEVELOPMENT APPROACH

Do NOT generate a huge amount of broken code at once.

Build incrementally.

First create the project structure.

Then implement:

PHASE 1
Frontend UI

PHASE 2
AI interview

PHASE 3
Scoring

PHASE 4
Firebase

PHASE 5
Smart contract

PHASE 6
Wallet connection

PHASE 7
NFT minting

PHASE 8
Verification

PHASE 9
Security and error handling

PHASE 10
Polish and testing

After each phase, verify that the application works before moving to the next.

# 29. ACCEPTANCE CRITERIA

The project is complete only when:

[ ] Landing page works

[ ] User can start assessment

[ ] Wallet can connect

[ ] AI asks questions

[ ] AI evaluates answers

[ ] Questions adapt to performance

[ ] Assessment contains 5–7 questions

[ ] Deterministic score is calculated

[ ] Pass/fail works

[ ] Assessment hash is generated

[ ] Firebase stores assessment

[ ] Smart contract is deployed to Polygon Amoy

[ ] Unauthorized minting is prevented

[ ] Successful candidate can mint NFT

[ ] NFT metadata works

[ ] Transaction hash is displayed

[ ] Badge page works

[ ] Public verification page works

[ ] Blockchain hash is checked

[ ] Failed candidates cannot mint

[ ] Duplicate minting is prevented

[ ] Error states are handled

[ ] Mobile/tablet/desktop UI is responsive

[ ] README explains complete setup

# 30. IMPORTANT

Do not replace the AI interviewer with a static question list.

Do not calculate the final score only using an LLM-generated number.

Do not allow frontend users to directly determine their score.

Do not expose private keys.

Do not put private interview answers on-chain.

Do not create an unrestricted mint function.

Do not claim that an NFT itself proves real-world expertise.

The core value is:

AI conducts an adaptive assessment
+
Backend verifies the result
+
Cryptographic hash protects the assessment record
+
Blockchain provides portable verification
+
NFT represents the verified credential

Start by creating the complete project structure and then implement the application phase-by-phase.

At every stage, provide:

1. Files created
2. Code implemented
3. Commands to run
4. Environment variables required
5. How to test the feature
6. Any remaining issues

Do not skip implementation details.

The final result must be a working, polished hackathon MVP rather than a conceptual prototype.
