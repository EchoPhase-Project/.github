<p align="center">
  <img src="echophase.svg" width="96" height="96" alt="EchoPhase">
</p>

<h1 align="center">EchoPhase</h1>

<p align="center">
  Bots and services, connected in one place.
</p>

EchoPhase is an open-source platform for managing bots and connecting
services: link your Discord and Twitch accounts, automate tasks with
workflows, and reach everything through one API.

## What it does

- **Connections.** Link Discord and Twitch accounts once; EchoPhase keeps
  their tokens fresh and encrypted, and your bots use them.
- **Workflows.** Automate tasks from blocks that run on a schedule or on
  events, with storage that persists between runs.
- **API and API clients.** Everything the web app does is in the API. Each
  bot or script gets its own client, with only the permissions it needs.
- **Realtime gateway.** One WebSocket for events from your connections and
  workflows, as they happen.
- **Yours to run.** Self-host it with the Helm chart or Docker Compose.

## Repositories

| Repository | What |
|---|---|
| [server](https://github.com/EchoPhase-Project/server) | API, realtime gateway and workflows (.NET 10, PostgreSQL, ScyllaDB, Valkey) |
| [webapp](https://github.com/EchoPhase-Project/webapp) | The web client (SolidJS) |
| [charts](https://github.com/EchoPhase-Project/charts) | Helm chart and Docker Compose to run EchoPhase yourself |
| [deploy](https://github.com/EchoPhase-Project/deploy) | The project's own instance: Flux, cluster infrastructure, monitoring |
| [Isopoh.Cryptography.Argon2](https://github.com/EchoPhase-Project/Isopoh.Cryptography.Argon2) | A fork of the Argon2 library the server hashes passwords with |

## Run it yourself

```sh
helm install echophase oci://ghcr.io/echophase-project/charts/echophase \
  --namespace echophase --create-namespace \
  --set secrets.POSTGRES_PASSWORD=change-me \
  --set secrets.VALKEY_PASSWORD=change-me
```

Images are published to `ghcr.io/echophase-project`. Docker Compose, the
settings and what each one does are in
[charts](https://github.com/EchoPhase-Project/charts).

## License

EchoPhase is released under the
[BSD 3-Clause License](https://github.com/EchoPhase-Project/server/blob/main/LICENSE).
