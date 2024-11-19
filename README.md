# Optimism_VM_Architecture

The Optimistic Virtual Machine (OVM) is a virtual machine designed for Layer 2 scaling solutions, specifically for Optimism. It provides EVM compatibility while enabling high throughput and low-cost transactions.

```mermaid
graph TB
    subgraph "Layer 1 - Ethereum Mainnet"
        L1[Ethereum] --> Bridge[Bridge Contract]
    end
    
    subgraph "Layer 2 - Optimism"
        Bridge <--> Sequencer[Sequencer]
        Sequencer --> BatchSubmitter[Batch Submitter]
        
        subgraph "OVM Runtime Environment"
            BatchSubmitter --> ExecutionManager[Execution Manager]
            ExecutionManager --> StateManager[State Manager]
            StateManager --> SafetyChecker[Safety Checker]
            
            subgraph "Transaction Processing"
                ExecutionManager --> Transpiler[Transpiler]
                Transpiler --> ByteCode[OVM Bytecode]
                ByteCode --> StateTransition[State Transition]
            end
        end
        
        StateTransition --> FraudProof[Fraud Proof System]
        FraudProof --> Bridge
    end

    User[User] --> Sequencer
```
