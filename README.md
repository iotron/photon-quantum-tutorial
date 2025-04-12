# Quantum Multiplayer Development Guide

## Table of Contents

1. [Introduction](#introduction)
   - [Photon Quantum Overview](#photon-quantum-overview)
   - [Deterministic ECS vs Unity GameObject Model](#deterministic-ecs-vs-unity-gameobject-model)
   
2. [Setting Up Photon Quantum](#setting-up-photon-quantum)
   - [Project Setup and Requirements](#project-setup-and-requirements)
   - [Quantum Project Structure and Workflow](#quantum-project-structure-and-workflow)
   
3. [Quantum ECS Basics](#quantum-ecs-basics)
   - [Entities, Components, and Frames in Quantum](#entities-components-and-frames-in-quantum)
   - [Systems and Game Logic Update Cycle](#systems-and-game-logic-update-cycle)
   - [ECS in Quantum vs Unity MonoBehaviours](#ecs-in-quantum-vs-unity-monobehaviours)

4. [Input Handling](#input-handling)
   - [Defining Player Input Commands for Quantum](#defining-player-input-commands-for-quantum)
   - [Local Input Polling and Processing](#local-input-polling-and-processing)
   - [Unity Input System vs Quantum Input Model](#unity-input-system-vs-quantum-input-model)

5. [Player Spawning and Setup](#player-spawning-and-setup)
   - [Player Join Process and Character Creation](#player-join-process-and-character-creation)
   - [Player Data and the PlayerLink Component](#player-data-and-the-playerlink-component)
   - [Spawning Characters vs Instantiating in Unity](#spawning-characters-vs-instantiating-in-unity)

6. [Character Movement and Physics](#character-movement-and-physics)
   - [Movement System and KCC (Kinematic Character Controller)](#movement-system-and-kcc-kinematic-character-controller)
   - [Deterministic Physics and Collision Handling](#deterministic-physics-and-collision-handling)
   - [Unity Physics vs Quantum Physics Comparison](#unity-physics-vs-quantum-physics-comparison)

7. [Weapons and Shooting](#weapons-and-shooting)
   - [Weapon Inventory Management and Switching](#weapon-inventory-management-and-switching)
   - [Firing Mechanics and Bullet Simulation](#firing-mechanics-and-bullet-simulation)
   - [Implementing Shooting: Unity vs Quantum Approach](#implementing-shooting-unity-vs-quantum-approach)

8. [Skills and Abilities](#skills-and-abilities)
   - [Skill Inventory and Casting Logic](#skill-inventory-and-casting-logic)
   - [Area-of-Effect Skills and Cooldown Management](#area-of-effect-skills-and-cooldown-management)
   - [Handling Abilities in Unity vs Quantum](#handling-abilities-in-unity-vs-quantum)

9. [Health, Damage, and Respawning](#health-damage-and-respawning)
   - [Status System for Health and Damage](#status-system-for-health-and-damage)
   - [Respawn System and Spawn Point Logic](#respawn-system-and-spawn-point-logic)
   - [Life/Death Cycle: Unity vs Quantum](#lifedeath-cycle-unity-vs-quantum)

10. [Visuals and Entity Views](#visuals-and-entity-views)
    - [Entity Prefabs and QuantumEntityView Integration](#entity-prefabs-and-quantumentityview-integration)
    - [Character & Weapon Animation (Animator and IK setup)](#character--weapon-animation-animator-and-ik-setup)
    - [Visual Effects via Quantum Events (Muzzle flashes, Explosions)](#visual-effects-via-quantum-events-muzzle-flashes-explosions)
    - [Camera Follow and ViewContext for Local Player](#camera-follow-and-viewcontext-for-local-player)

11. [UI Integration](#ui-integration)
    - [Player HUD (Health, Ammo, and Fire Rate Bars)](#player-hud-health-ammo-and-fire-rate-bars)
    - [Skill Cooldown Display and Ability Indicators](#skill-cooldown-display-and-ability-indicators)
    - [Damage Pop-up Text (Floating Combat Text)](#damage-pop-up-text-floating-combat-text)
    - [Updating UI: Unity Canvas vs Quantum Data](#updating-ui-unity-canvas-vs-quantum-data)

12. [Networking and Matchmaking](#networking-and-matchmaking)
    - [Photon Quantum Networking Overview (Server and Clients)](#photon-quantum-networking-overview-server-and-clients)
    - [Connecting to Photon Rooms and Matchmaking Flow](#connecting-to-photon-rooms-and-matchmaking-flow)
    - [Predictive Input and Rollback Synchronization](#predictive-input-and-rollback-synchronization)
    - [Networking Code: Photon Quantum vs Unity Netcode](#networking-code-photon-quantum-vs-unity-netcode)

13. [Debugging and Tools](#debugging-and-tools)
    - [Deterministic Simulation Debugging (Replays & Validation)](#deterministic-simulation-debugging-replays--validation)
    - [Quantum Profiler and Diagnostics Tools](#quantum-profiler-and-diagnostics-tools)
    - [Troubleshooting Common Quantum Issues](#troubleshooting-common-quantum-issues)

---

*Note: This guide is targeted at intermediate Unity developers who are learning Photon Quantum and are familiar with the basics of Unity. The guide compares typical Unity implementations with Photon Quantum’s ECS/deterministic approach, supported by extensive code examples from production-quality scripts.*

---
