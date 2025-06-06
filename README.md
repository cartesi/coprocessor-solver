# Coprocessor Solver

A task processing and verification system that handles computational tasks on the blockchain using EigenLayer

## What It Does

### 1. Task Processing
- Receives computational tasks from the blockchain
- Each task contains:
  - A machine hash (identifies the computation type)
  - Input data
  - A callback address for results
- Tasks are stored in a PostgreSQL database with status tracking

### 2. BN254 Signature Aggregation
- Collects and verifies signatures from multiple operators
- Uses BN254 signatures for efficient aggregation
- Implements quorum-based verification:
  - Requires 67% threshold of operator signatures
  - Tracks operator stakes and participation
  - Verifies non-signer stakes and signatures

### 3. Operator Management
- Tracks operator states and sockets
- Manages operator registration and updates
- Handles operator communication channels
- Monitors operator participation in tasks

### 4. Task Verification Pipeline
1. **Task Reception**
   - Monitors blockchain for new tasks
   - Stores tasks in database
   - Assigns initial status

2. **Processing**
   - Distributes tasks to operators
   - Collects operator responses
   - Aggregates BN254 signatures
   - Verifies quorum thresholds using on-chain EigenLayer AVS information

3. **Result Handling**
   - Verifies that output merkle root match the generated merkle roots of the outputs of the computation
   - Stores finalization data
   - Triggers callbacks on blockchain with results
