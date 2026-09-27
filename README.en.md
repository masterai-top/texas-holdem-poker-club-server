[简体中文](README.md) | [繁體中文](README.zh-TW.md) | [English](README.en.md) | [Visual site](https://masterai-top.github.io/texas-holdem-poker-club-server/en/)

# C++ Texas Holdem Poker Club Push Server Source

A C++/Tars backend service for poker clubs and multiplayer rooms, focused on message delivery, player presence, game-state reporting, room-user reports, broadcast notifications and maintenance messages. Authentic interface screenshots show how the service fits into a club and private-table product.

> The public repository primarily contains `PushServer` and related contracts. It is not a complete Unity client or the entire poker backend. Verify UI features, dependencies and delivered modules separately.

## What the service does

1. Gateways report online users and routing addresses.
2. Other services query individual or batched online/game state.
3. Rooms report players, table details and online statistics.
4. PushServer routes user messages and broadcasts.
5. Administrative commands reload configuration, clean stale state and send maintenance notifications.

## Verifiable capabilities

- Single-user, multi-user and broadcast message delivery.
- Online-state reporting, batch presence lookup and online-player lists.
- Game-state reports and queries.
- Room-user and room-table reporting.
- Maintenance, red-dot, account restriction and state notifications.
- MySQL access, DBAgent proxies and user-hashed service routing.

## Product workflow and interfaces

The screenshots show quick join/create, poker clubs, cash tables, AOF, Short Deck, Omaha, SNG, MTT, results and language selection. They illustrate the integrated product experience; they do not prove that every gameplay engine is included in this standalone repository.

| Private-table rules | Game configuration | Create a club |
| --- | --- | --- |
| <img src="docs/assets/images/screen-01.jpg" width="260" alt="Poker private-table settings"> | <img src="docs/assets/images/screen-03.jpg" width="260" alt="Cash AOF Short Deck Omaha configuration"> | <img src="docs/assets/images/screen-04.jpg" width="260" alt="Create a poker club"> |

| Quick join | Club lobby | Results |
| --- | --- | --- |
| <img src="docs/assets/images/screen-08.jpg" width="260" alt="Join a private poker room"> | <img src="docs/assets/images/screen-11.jpg" width="260" alt="Poker club game lobby"> | <img src="docs/assets/images/screen-06.jpg" width="260" alt="Poker results and player statistics"> |

## Technical structure

| Layer | Repository evidence |
| --- | --- |
| Service | C++ Tars Application and Servant implementation |
| Contracts | `.tars` definitions for push, presence, game state and broadcasts |
| Data | Tars MySQL client and DBAgent proxies |
| Routing | User-hashed proxies and asynchronous state notifications |
| Operations | reload, CleanOnlineUser, ServerUpdate and DailyReset commands |
| Build | Linux Makefile with external Tars and internal module dependencies |

## Build requirements

The Makefile references `/home/tarsproto/XGame/DBAgentServer/DBAgentServer.mk` plus common headers and proxies not included here. A standalone `make` is therefore not sufficient. Prepare compatible Tars contracts, DBAgent, configuration and database services, and remove hard-coded deployment details and credentials before testing.

## Contact and due diligence

Telegram: [@xuzongbin001](https://t.me/xuzongbin001) · Email: masterai918@gmail.com

Verify source scope, dependencies, licensing and applicable laws before use. No concurrency, deployment, revenue or search-ranking outcome is guaranteed.

