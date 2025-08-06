## The 4-Step System Design Process

System design interviews typically provide 45-60 minutes to design complex systems that took years to build in reality. The key isn't perfection—it's demonstrating structured thinking and scalability knowledge. This guide walks through designing **SkyCanvas**, a recreational drone swarm for aerial art displays.

## Step 1: Constraints and Use Cases (10-15 minutes)

**Never jump straight into design!** Most candidates fail here by making assumptions. Instead, requirements should be clarified through questions.

### Core Questions for SkyCanvas:

**Functional Requirements:**

- How many drones per show? _Assume 100-1000 drones_
- What patterns can they create? _3D formations, animated sequences, light paintings_
- How long do shows last? _10-30 minutes typically_
- Real-time control or pre-programmed? _Both—choreographed sequences with override capability_

**Non-Functional Requirements:**

- How many concurrent shows globally? _Start with 100 shows/day, growing to 1000_
- Latency requirements? _<50ms for formation commands—safety critical_
- What about drone failures mid-show? _Graceful degradation—show continues_
- Geographic distribution? _Initially US, expanding globally_

### Calculating Scale:

Some napkin maths (interviewers appreciate this):

- 1000 shows/day × 500 avg drones = 500,000 drone control sessions daily
- Each drone sends telemetry every 100ms = 10 updates/second
- 500,000 × 10 × 86,400 seconds = 432 billion telemetry points/day
- Storage: Each show choreography ~10MB, telemetry ~1GB/show = ~1TB daily

**Example dialogue:**

> "Before starting the design, the scale needs clarification. Is this for hobbyists with 10 drones, or commercial shows with thousands? This drastically changes the architecture."

## Step 2: Abstract Design (10 minutes)

Draw a simple high-level architecture connecting major components. Don't dive deep yet—just demonstrate understanding of the system's skeleton.

### SkyCanvas Core Components:

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│   Web Portal    │────▶│   API Gateway    │────▶│  Show Manager   │
│  (Choreography) │     │  (REST/GraphQL)  │     │   (Scheduling)  │
└─────────────────┘     └──────────────────┘     └─────────────────┘
                                │                          │
                                ▼                          ▼
                        ┌──────────────────┐     ┌─────────────────┐
                        │  Command Queue   │────▶│  Drone Gateway  │
                        │   (Real-time)    │     │  (WebSockets)   │
                        └──────────────────┘     └─────────────────┘
                                                          │
                    ┌──────────────────┐                 ▼
                    │   Data Storage   │         ┌─────────────────┐
                    │  - Choreography  │◀────────│   Drone Fleet   │
                    │  - Telemetry     │         │  (Edge Devices) │
                    │  - User Data     │         └─────────────────┘
                    └──────────────────┘
```

**Key Design Decisions:**

- **Web Portal**: Artists design shows using visual tools
- **API Gateway**: Single entry point for all client requests
- **Show Manager**: Orchestrates scheduling, resource allocation
- **Command Queue**: Ensures reliable, ordered command delivery
- **Drone Gateway**: Maintains persistent connections to drones
- **Data Storage**: Hybrid approach—different stores for different needs

**Example explanation:**

> "The creative tools are separated from the real-time control plane. This lets artists work on choreography without affecting live shows. The command queue decouples show execution from drone communication."

## Step 3: Understanding Bottlenecks (5-10 minutes)

Identify where the system will break under load. Every design has weak points—recognising them demonstrates experience.

### SkyCanvas Bottlenecks:

**1. Drone Gateway Connections**

- Problem: 500,000 drones × persistent WebSocket = massive memory usage
- Impact: Single server can handle ~10,000 connections = need 50+ servers

**2. Real-time Command Distribution**

- Problem: Broadcasting formation changes to 1000 drones in <50ms
- Impact: Network latency + processing could exceed safety thresholds

**3. Telemetry Ingestion**

- Problem: 5 million updates/second at peak
- Impact: Database writes become bottleneck, data loss risks

**4. Choreography Rendering**

- Problem: Computing 3D positions for 1000 drones × 30fps
- Impact: CPU intensive, could delay command generation

**5. Geographic Latency**

- Problem: Controlling drones in Tokyo from US servers = 150ms+ latency
- Impact: Violates the 50ms requirement

**Trade-off Discussion Example:**

> "Telemetry frequency could be reduced to ease ingestion, but that compromises safety monitoring. Instead, non-critical metrics should be sampled while prioritising battery/position data."

## Step 4: Scaling the Design (15-20 minutes)

Apply scalability patterns to address bottlenecks. This demonstrates depth of knowledge.

### Scalability Principles Applied to SkyCanvas:

#### **1. Horizontal Scaling (Adding More Machines)**

**Drone Gateway Scaling:**

```
                    Load Balancer (Consistent Hashing by Show ID)
                    /            |            \
            Gateway-1       Gateway-2      Gateway-N
            (Shows 1-100)  (Shows 101-200)  (...)
```

- Consistent hashing keeps drone sessions sticky
- Auto-scaling based on connection count
- Each gateway handles specific show ranges

#### **2. Caching (Memory Before Disk)**

**Multi-Level Cache Strategy:**

```
Browser Cache     CDN            Redis           Database
(Choreography)    (Static)       (Hot Shows)     (Cold Storage)
    1ms           10ms           5ms             100ms
```

**Example:**

> "Tonight's Vegas show choreography lives in Redis. Drones pull it once at startup, not repeatedly from the database."

#### **3. Database Optimisation**

**Polyglot Persistence for SkyCanvas:**

- **PostgreSQL**: User accounts, show metadata (ACID needed)
- **MongoDB**: Choreography documents (flexible schema for patterns)
- **InfluxDB**: Time-series telemetry (optimised for metrics)
- **S3**: Show recordings, audit logs (cheap cold storage)

**Sharding Strategy:**

```
Telemetry DB Shards:
Shard-1: Shows in Americas
Shard-2: Shows in Europe  
Shard-3: Shows in Asia
(Sharded by geographic region to keep data close to drones)
```

#### **4. Load Balancing**

**Smart Routing for SkyCanvas:**

- **Geographic**: Route to nearest edge server
- **Least Connections**: For WebSocket distribution
- **Weighted Round Robin**: For API requests
- **Priority Queue**: Emergency commands bypass normal traffic

#### **5. Asynchronous Processing**

**Event-Driven Architecture:**

```
Show Scheduled → Message Queue → Workers Process:
                                  - Generate flight paths
                                  - Validate safety zones
                                  - Pre-compute transitions
                                  - Warm up drone connections
```

**Example:**

> "When an artist uploads choreography, the system doesn't block. It queues for processing—generating flight paths, checking collisions, optimising battery usage—then notifies when ready."

#### **6. Edge Computing**

**Distributed Command Centres:**

```
Global Orchestrator (US)
    ├── Regional Hub (California) 
    │   └── Local Controller (LA Show) → 500 drones
    ├── Regional Hub (Texas)
    │   └── Local Controller (Austin Show) → 300 drones
    └── Regional Hub (Tokyo)
        └── Local Controller (Shibuya Show) → 1000 drones
```

**Latency Optimisation:**

> "Each show runs on edge servers within 50km of the venue. Only choreography sync and monitoring go to central servers."

## Advanced Patterns for SkyCanvas

### **Circuit Breakers**

If a drone loses connection for 3 seconds, circuit breaker activates:

1. Stop sending commands (prevent queue buildup)
2. Mark drone as "failed"
3. Redistribute its choreography to neighbours
4. Alert safety system

### **Bulkheading**

Isolate show failures:

```
Show Instance A (Isolated Process)
├── Command Channel
├── Telemetry Channel  
└── Safety Monitor

Show Instance B (Separate Process)
├── Command Channel
├── Telemetry Channel
└── Safety Monitor
```

One show crashing doesn't affect others.

### **Backpressure**

When telemetry overwhelms the system:

1. Drones detect slow ACKs
2. Automatically reduce transmission rate
3. Prioritise critical metrics (battery, position)
4. Buffer non-critical data locally

## Real-World Analogies to Discuss

When explaining designs, reference similar systems:

- **SkyCanvas Command Distribution** ≈ **Uber's driver dispatch** (real-time location updates)
- **Choreography Storage** ≈ **Netflix's video catalogue** (CDN distribution)
- **Telemetry Pipeline** ≈ **IoT platforms** (massive sensor ingestion)
- **Safety System** ≈ **Trading systems' kill switches** (instant shutdown capability)

## Practice Questions Using SkyCanvas

1. **"How would the system handle a drone swarm where half lose GPS signal?"**
    
    - Fallback to visual positioning using computer vision
    - Neighbour-relative positioning (mesh network)
    - Graceful show degradation protocols
2. **"Design search for a library of 1 million choreographies"**
    
    - Elasticsearch for full-text search
    - Tag-based categorisation
    - ML-powered similarity matching
3. **"How are drone collisions prevented?"**
    
    - Pre-flight path validation
    - Real-time collision detection grid
    - Safety bubbles with exponential backoff
    - Emergency scatter protocol

## Key Takeaways

### Do's:

- **Ask clarifying questions** (shows assumptions aren't being made)
- **Start simple, then scale** (proves ability to iterate)
- **Discuss trade-offs** (demonstrates real-world thinking)
- **Use concrete numbers** (shows understanding of scale)
- **Draw diagrams** (visual communication is crucial)

### Don'ts:

- **Don't over-engineer initially** (start with MVP)
- **Don't ignore data estimates** (maths matters)
- **Don't forget about failures** (everything breaks)
- **Don't be rigid** (adapt to interviewer feedback)
- **Don't skip monitoring** (how is success measured?)

### Final Interview Tip:

> "This design addresses current requirements, but at 10x scale, consideration would be given to a mesh network where drones communicate peer-to-peer, reducing central coordination overhead."

This shows thinking beyond the immediate problem—exactly what companies building at scale need.

---

## The 30-Second Elevator Pitch

_"SkyCanvas is a distributed system for orchestrating aerial drone art. It separates the creative plane (choreography design) from the control plane (real-time coordination), uses edge computing to meet latency requirements, and employs event-driven architecture for scalability. The system handles failure gracefully through circuit breakers and bulkheading, while supporting global shows through geographic sharding and CDN distribution."_

Remember: System design interviews test ability to think at scale, not memorise solutions. Use this framework, but adapt it to whatever system needs designing. The drone swarm is just practice—the patterns are universal.


See also:
- [[Coding Interview Patterns]]
- [[System Design]]
- [[Algorithmic Complexity]]
- [[Scalability]]
- [System Design Interview Guide](https://www.hiredintech.com/system-design/)


---

_Summary generated by Claude Opus 4.1 and amended by me._