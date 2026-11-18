# Xlarva-RULE_CN-Direct_Final-Proxy
Xlarva enforces a 500 KB config limit (~2,000 domain rules max OR ~7000 ip-CIDR max). Routing CN traffic to Direct and everything else to Proxy uses the fewest rules.

## Setup

### 1. CN IP (`Direct`)
**Network** -> **Route** -> **Excluded Routes** -> **Import from URL**
```text
https://raw.githubusercontent.com/soffchen/GeoIP2-CN/release/CN-ip-cidr.txt
```

### 2. CN Domains (`Direct`)
**Advanced** -> **Traffic Splitting** -> **Enable PAC Splitting** (ON) -> **Domain Rules** -> **Import Domains** -> **URL**
* **Match Type**: `Host and Subdomains`
* **Action**: `Direct`
```text
https://raw.githubusercontent.com/entr0pia/SwitchyOmega-Whitelist/master/white-mini.sorl
```

### 3. Fallback (`Proxy`)
**Advanced** -> **Traffic Splitting** -> **Rules**
* **Default Action**: `Proxy`
* **Bare IP Requests**: `Proxy`

---

## Notes
* **Size Limit**: Max **500 KB**. Current usage: **~450 KB** (IP: ~315 KB, Domain: ~135 KB), leaving **~50 KB** (~200 domains) for custom rules.
* **Custom Lists**: The URLs above are ready-made compact lists. Any list works within **IPs ≤ 4,500** + **Domains ≤ 700**.
* **No Auto-Update**: URL import is one-time only; rules do not update automatically.
* **Priority**: **Excluded Routes** override **Bare IP Requests** (CN IPs stay direct).
* **DNS Check**: Add `ipleak.net` (`Direct`) to verify no DNS leaks.
