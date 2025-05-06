# **Architecture Overview**

## **Modular, SOLID-Compliant Design**
The Silent Code adheres to a modular and SOLID-compliant architecture to ensure scalability, maintainability, and testability.

---

### **Core Modules**
Each module is independent, testable, and aligned with the Single Responsibility Principle (SRP).

#### **1. Habit Detection Engine**
**Purpose**: Detect habit loops using AI.

**Classes**:
- `HabitDataCollector`: Collects and stores stress, time, guilt metrics.
- `HabitPredictor` (Interface): Abstracts prediction logic.
- `TFLitePredictor` (Implements `HabitPredictor`): Runs TensorFlow Lite model.
- `PredictionEncryptor`: AES-256 encrypts predictions before storage.

#### **2. User Management**
**Purpose**: Secure authentication and profile handling.

**Classes**:
- `AuthManager`: Handles Firebase Auth (OAuth, email/password).
- `UserProfile`: Stores encrypted user data.
- `SessionValidator`: JWT validation for API requests.

#### **3. Content Delivery**
**Purpose**: Serve faith-driven and cultural content.

**Classes**:
- `ContentFetcher` (Interface): Fetches verses/proverbs.
- `GraphQLFetcher` (Implements `ContentFetcher`): Queries GraphQL API.
- `ContentCache`: LRU cache with encrypted entries.

#### **4. Behavioral Rewiring System**
**Purpose**: Help users rewire habits through actionable micro-tasks.

**Classes**:
- `ActionScheduler`: Queues micro-actions.
- `ActionExecutor`: Executes actions with permission checks.
- `RewardSystem`: Grants points for completed actions.

#### **5. Ethical Growth & DAO**
**Purpose**: Promote organic growth and decentralized governance.

**Classes**:
- `InviteManager`: Bluetooth/Wi-Fi Direct invites.
- `ElderRecognizer`: PageRank-based elder detection.
- `DAOVoter`: Handles Solana-based NFT voting.

---

### **Security Implementation**
- **At Rest**: AES-256 encryption (SQLCipher, SharedPreferences).
- **In Transit**: TLS 1.3 with certificate pinning.
- **Authentication**: Firebase Auth with 2FA and biometric locks.
- **Code Hardening**: Obfuscation (ProGuard/R8), root/jailbreak detection.

---

### **Class Diagram (Simplified)**
```plaintext
┌───────────────────┐          ┌───────────────────┐  
│   HabitPredictor  │<|--------│  TFLitePredictor  │  
└───────────────────┘          └───────────────────┘  
           ▲                             ▲  
           │                             │  
┌───────────────────┐          ┌───────────────────┐  
│ HabitDataCollector│          │ PredictionEncryptor│  
└───────────────────┘          └───────────────────┘  

┌───────────────────┐          ┌───────────────────┐  
│    AuthManager    │─────┐    │   SessionValidator│  
└───────────────────┘     │    └───────────────────┘  
                          ▼  
┌───────────────────┐          ┌───────────────────┐  
│   UserProfile     │<─────────┤UserProfileEncryptor│  
└───────────────────┘          └───────────────────┘  
