# WOOWTECH

Deployment recipes for the software stack we run in production — organised by
platform, one repository per target.

**每個軟體、每個平台一個倉庫。** 挑軟體、挑平台、直接部署。

---

## Software × platform matrix / 軟體 × 環境矩陣

| Software / 軟體 | Docker / Podman Compose | K3s / Kubernetes (Helm chart) | Home Assistant add-on |
|---|---|---|---|
| **anythingllm** | — | [Woow_k3s_anythingllm](https://github.com/WOOWTECH/Woow_k3s_anythingllm) | — |
| **emqx** | [Woow_podman_emqx](https://github.com/WOOWTECH/Woow_podman_emqx) | [Woow_k3s_emqx](https://github.com/WOOWTECH/Woow_k3s_emqx) | [Woow_ha_emqx](https://github.com/WOOWTECH/Woow_ha_emqx) |
| **hermes** | [Woow_podman_hermes](https://github.com/WOOWTECH/Woow_podman_hermes) | [Woow_k3s_hermes](https://github.com/WOOWTECH/Woow_k3s_hermes) | — |
| **homeassistant** | [Woow_podman_homeassistant](https://github.com/WOOWTECH/Woow_podman_homeassistant) | [Woow_k3s_homeassistant](https://github.com/WOOWTECH/Woow_k3s_homeassistant) | — |
| **immich** | [Woow_podman_immich](https://github.com/WOOWTECH/Woow_podman_immich) | [Woow_k3s_immich](https://github.com/WOOWTECH/Woow_k3s_immich) | [Woow_ha_immich](https://github.com/WOOWTECH/Woow_ha_immich) |
| **n8n** | [Woow_podman_n8n](https://github.com/WOOWTECH/Woow_podman_n8n) | [Woow_k3s_n8n](https://github.com/WOOWTECH/Woow_k3s_n8n) | [Woow_ha_n8n](https://github.com/WOOWTECH/Woow_ha_n8n) |
| **newapi** | [Woow_podman_newapi](https://github.com/WOOWTECH/Woow_podman_newapi) | [Woow_k3s_newapi](https://github.com/WOOWTECH/Woow_k3s_newapi) | — |
| **nextcloud** | [Woow_podman_nextcloud](https://github.com/WOOWTECH/Woow_podman_nextcloud) | [Woow_k3s_nextcloud](https://github.com/WOOWTECH/Woow_k3s_nextcloud) | [Woow_ha_nextcloud](https://github.com/WOOWTECH/Woow_ha_nextcloud) |
| **nginxpm** | [Woow_podman_nginxpm](https://github.com/WOOWTECH/Woow_podman_nginxpm) | [Woow_k3s_nginxpm](https://github.com/WOOWTECH/Woow_k3s_nginxpm) | [Woow_ha_nginxpm](https://github.com/WOOWTECH/Woow_ha_nginxpm) |
| **odoo** | [Woow_podman_odoo](https://github.com/WOOWTECH/Woow_podman_odoo) | [Woow_k3s_odoo](https://github.com/WOOWTECH/Woow_k3s_odoo) | [Woow_ha_odoo](https://github.com/WOOWTECH/Woow_ha_odoo) |
| **ollama** | [Woow_podman_ollama](https://github.com/WOOWTECH/Woow_podman_ollama) | [Woow_k3s_ollama](https://github.com/WOOWTECH/Woow_k3s_ollama) | — |
| **opendesign** | [Woow_podman_opendesign](https://github.com/WOOWTECH/Woow_podman_opendesign) | [Woow_k3s_opendesign](https://github.com/WOOWTECH/Woow_k3s_opendesign) | — |
| **portainer** | [Woow_podman_portainer](https://github.com/WOOWTECH/Woow_podman_portainer) | [Woow_k3s_portainer](https://github.com/WOOWTECH/Woow_k3s_portainer) | — |
| **supabase** | [Woow_podman_supabase](https://github.com/WOOWTECH/Woow_podman_supabase) | [Woow_k3s_supabase](https://github.com/WOOWTECH/Woow_k3s_supabase) | — |
| **vibekanban** | [Woow_podman_vibekanban](https://github.com/WOOWTECH/Woow_podman_vibekanban) | [Woow_k3s_vibekanban](https://github.com/WOOWTECH/Woow_k3s_vibekanban) | — |

*A `—` cell means we do not publish that platform for that software.*
*格中的 `—` 表示該軟體沒有該平台的部署。*

---

## How to use / 使用方式

**Docker / Podman Compose** — clone the `Woow_podman_<sw>` repo and run
`docker compose up -d` (or `podman-compose up -d`) after copying `.env.example`
to `.env`. Read the repo's README for per-software prerequisites (volumes,
external services, GPU, etc.).

**K3s / Kubernetes** — every `Woow_k3s_<sw>` repo now ships a **Helm chart at
the repo root**, so you can install without cloning:

```bash
helm install <release> https://github.com/WOOWTECH/Woow_k3s_<sw>/archive/refs/heads/main.tar.gz \
  --namespace <sw> --create-namespace
```

Override defaults with `--set` or a local `values.yaml`. Every chart follows
the same `namespace.{create,name}` + `<component>.{image,config,service,persistence,resources}`
value structure — see the chart's README for the full list.

**Home Assistant add-ons** — copy the `Woow_ha_<sw>` repository URL into
Settings → Add-ons → Add-on Store → three-dot menu → **Repositories**. The
add-on will appear in the list and can be installed with one click.

---

**Docker / Podman Compose** — `clone` 對應的 `Woow_podman_<軟體>` 倉庫,依照
README 複製 `.env.example`,然後 `docker compose up -d`(或
`podman-compose up -d`)。GPU、外部服務、掛載等前置作業請看該倉庫的說明。

**K3s / Kubernetes** — 每個 `Woow_k3s_<軟體>` 倉庫的根目錄都是一個 **Helm
chart**,不需要 clone 就能安裝:

```bash
helm install <release> https://github.com/WOOWTECH/Woow_k3s_<軟體>/archive/refs/heads/main.tar.gz \
  --namespace <軟體> --create-namespace
```

用 `--set` 或本地 `values.yaml` 覆寫預設值。所有 chart 都遵循相同的
`namespace.{create,name}` + `<元件>.{image,config,service,persistence,resources}` 值結構,
每個 chart 的 README 有完整的 values 對照表。

**Home Assistant add-on** — 到 設定 → 附加元件 → 附加元件商店 → 右上角三點選單
→ **儲存庫**,把 `Woow_ha_<軟體>` 的倉庫網址貼進去。列表就會出現該 add-on,可以
一鍵安裝。

---

## Migration notes / 遷移說明

Until August 2026 this stack lived in 15 `Woow_<sw>_docker_compose_all`
monorepos, one per software, with `podman` / `k3s` / `ha` branches. Those
repositories are now **archived**; each branch was extracted into its own
platform-specific repository above (K3s branches were rewritten as Helm
charts). Full git history is preserved on both sides.

If you had one of the archived repos cloned or added as a Home Assistant
add-on source, please update to the new URLs — archived repositories never
receive updates.

---

在 2026 年 8 月之前,這整套部署放在 15 個 `Woow_<軟體>_docker_compose_all`
單倉庫(每個軟體一個,分 `podman` / `k3s` / `ha` 分支)。那些倉庫現已**封存**,
內容都拆到上表的獨立倉庫中(K3s 分支已改寫為 Helm chart)。兩邊都保留完整
git 歷史。

若你之前有 clone 舊倉庫或把它加為 Home Assistant add-on 來源,請改用新網址 —
已封存的倉庫不會再收到更新。
