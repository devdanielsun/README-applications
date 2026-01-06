# Grafana Query Best Practices

## 📑 Inhoudsopgave
- [Dashboard Performance Tips](#-resource-optimalisatie)
- [Kritieke Optimalisaties](#-kritieke-performance-optimalisaties)
- [Kosten Optimalisatie](#-kosten-optimalisatie)
- [Quick Checklist](#-quick-implementation-checklist)

## ⚡ Resource Optimalisatie

- **Auto-refresh:** Zet alleen aan voor kritieke monitoring - verspilt anders resources en geld
- **Environment switching:** Vermijd snel wisselen tussen (sub)omgevingen - elke switch triggert nieuwe queries
- **Panel lazy loading:** Klap niet-kritieke panelen standaard in - data wordt pas geladen bij uitklappen

## 🚨 Kritieke Performance Optimalisaties

### 1. **Tijd Filtering - ALTIJD Verplicht**

**Impact:** 90-99% minder data processing, 10-100x sneller

```kql
| where TimeGenerated > ago(1h)      // Partitioning optimization
| where $__timeFilter(TimeGenerated) // Grafana auto-filtering
```

**Zonder tijd filter:** Scant TB's data → €50+ per query, 30+ seconden  

**Met tijd filter:** Alleen relevante partitions → €0.50 per query, 2-3 seconden

### 2. **Filter Volgorde + Early Projection**

**Impact:** 20-80% sneller door optimale query execution

```kql
AppMetrics
| where TimeGenerated > ago(1h)           // 99% data reductie eerst
| where Name == "metric_name"             // Index lookup O(1)  
| project TimeGenerated, AppRoleName, Sum // 90% memory reductie
| where AppRoleName startswith "prefix"   // String ops op kleine dataset
```

### 3. **Efficient String Matching**

**Performance:** `== (1μs)` → `has (10μs)` → `startswith (50μs)` → `contains (1000μs)`

```kql
| where Name == "exact_match"        // Hash index: snelst
| where AppRoleName has "substring"  // Inverted index  
| where Url startswith "/api/"       // Prefix index
// VERMIJD: contains, regex (geen index mogelijk)
```

## 💰 Kosten Optimalisatie

### 4. **Result Limits + Smart Aggregatie**

**Grafana max:** 10K datapoints - meer = verspilling + browser crash risk

```kql
| top 100 by TimeGenerated desc                        // Voor trends
| summarize count() by bin(TimeGenerated, $__interval) // Grafana adaptive
| limit 1000                                           // Safety net
```

### 5. **Herbruikbare Variabelen**

**Problem:** Environment filter herhaald in 10+ queries = maintenance hell

```kql
let EnvironmentFilter = case('${SubEnvironment}' == 'o2-', 'xyz-o2-', 'xyz--');
AppMetrics | where AppRoleName startswith EnvironmentFilter  // Single source of truth
```

## 📊 Grafana Specifiek

### 6. **Template Variables & Caching**

```kql
| where $__timeFilter(TimeGenerated)  // Auto tijd range from dashboard
| where Environment == '$environment' // Cached dropdown values
| summarize avg(Duration) by bin(TimeGenerated, $__interval) // Adaptive binning
```

**Pro tip:** Enable query caching 5-60 min in dashboard settings

### 7. **Data Transformation Strategy**

- **In KQL:** Complex logic, aggregations, filtering (distributed processing)
- **In Grafana:** UI formatting, simple unit conversions, multi-query joins

## ⚠️ Performance Killers - VERMIJD ALTIJD

```kql
// 💀 DESASTREUS - geen tijd filter  
AppMetrics | where Name == "metric"  // Scant alle TB's data

// 💀 CPU KILLER - regex operations
| where AppRoleName matches regex ".*pattern.*" // 100x langzamer dan startswith

// 💀 INDEX BREAKER - multiple OR  
| where Name == "a" or Name == "b" or Name == "c"  // 3 separate lookups
| where Name has_any ("a", "b", "c")              // ✅ GOED: hash set lookup
```

**Performance impact:** Regex vs startswith

## 🎯 Monitoring Best Practices

### Health Checks (high frequency)

```kql
AppRequests
| where TimeGenerated > ago(5m)        // Real-time window
| where Url endswith "/api/health"     // Index lookup
| summarize by AppRoleName, ResultCode // Minimal aggregation
```

### Error Monitoring (intelligent alerting)  

```kql
AppExceptions
| where TimeGenerated > ago(15m)    // Balance tussen freshness vs noise
| where SeverityLevel >= 3          // Skip debug/info logs
| summarize count() by OperationName  
| top 5 by count_ desc             // Focus op grootste problemen
```

## 📋 Quick Implementation Checklist

### 🚨 Critical (Do First)

 - `$__timeFilter()` of `ago()` in ELKE query
 - Tijd filter staat bovenaan where clauses
 - `project` direct na filtering voor memory optimization
 - `limit`/`top` voor queries die veel rijen kunnen retourneren

### 🔧 Optimization (Do Second)

- [ ] `==`/`has`/`startswith` gebruiken i.p.v. `contains`/`regex`
- [ ] `has_any()` voor multiple OR conditions
- [ ] Template variables voor dynamic filtering
- [ ] Query caching enabled (5-60min) in Grafana

### 📈 Monitoring Targets

- [ ] Query tijd: <15 sec (95th percentile)
- [ ] Cost per query: <€0.10
- [ ] Zero timeouts during normale operatie
- [ ] Dashboard load tijd: <5 sec

### 🚨 Emergency Troubleshooting

**Query te langzaam?**

1. Voeg tijd filter toe (meest waarschijnlijke fix)
2. Verplaats tijd filter naar boven  
3. Add `limit 1000` als quick fix
4. Check of indexed columns gebruikt worden

**Kosten te hoog?**

1. Check data volume van grootste queries
2. Implementeer result limits eerst
3. Optimaliseer high-frequency queries (health checks)
4. Enable query caching

**Meer diepte**

Voor meer diepgaande informatie, bekijk deze nuttige links:

- **[Query Optimization in Grafana](https://grafana.co.za/query-optimization-in-grafana-best-practices-examples/)** - Best practices met voorbeelden
- **[Azure Monitor Service Limits](https://learn.microsoft.com/en-us/azure/azure-monitor/fundamentals/service-limits)** - Rate limits en quotas
