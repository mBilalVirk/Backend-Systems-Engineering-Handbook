# Backend & Systems Engineering Handbook

A developer-focused guide to 111 concepts you meet when building, scaling, securing and operating real production systems. Each entry has **What it is**, **Why it matters**, and a **Practical example** (mostly Laravel/PHP, plus config/YAML/shell where that fits better).

> **How to maintain this file**
> - Add new concepts at the end of the matching `## Part`, using the same template (`### N. Name` → What / Why / Example).
> - Add a `Last reviewed` note to any entry you re-verify.
> - Regenerate the table of contents with the script in **Maintaining the TOC** at the bottom of this file.
> - Keep examples small and runnable; link to real files in your project when possible.

---

## Table of Contents


**[Part 1: Traffic, Delivery & Runtime Basics](#part-1-traffic-delivery--runtime-basics)**

- [1. Rate Limiting](#1-rate-limiting)
- [2. Caching](#2-caching)
- [3. Load Balancing](#3-load-balancing)
- [4. Reverse Proxies](#4-reverse-proxies)
- [5. API Gateways](#5-api-gateways)
- [6. CI/CD](#6-cicd)
- [7. Docker](#7-docker)
- [8. Kubernetes](#8-kubernetes)

**[Part 2: Resilience & Messaging](#part-2-resilience--messaging)**

- [9. Service Discovery](#9-service-discovery)
- [10. Circuit Breakers](#10-circuit-breakers)
- [11. Timeouts](#11-timeouts)
- [12. Retries](#12-retries)
- [13. Exponential Backoff](#13-exponential-backoff)
- [14. Idempotency](#14-idempotency)
- [15. Message Queues](#15-message-queues)
- [16. Pub/Sub](#16-pubsub)
- [17. Event-Driven Architecture](#17-event-driven-architecture)
- [18. Distributed Transactions](#18-distributed-transactions)
- [19. Saga Pattern](#19-saga-pattern)
- [20. Dead Letter Queues](#20-dead-letter-queues)

**[Part 3: Scheduling & Real-Time](#part-3-scheduling--real-time)**

- [21. Cron Jobs](#21-cron-jobs)
- [22. WebSockets](#22-websockets)
- [23. Long Polling](#23-long-polling)
- [24. Server-Sent Events](#24-server-sent-events)

**[Part 4: Databases](#part-4-databases)**

- [25. Database Indexing](#25-database-indexing)
- [26. Query Optimization](#26-query-optimization)
- [27. N+1 Queries](#27-n1-queries)
- [28. Connection Pooling](#28-connection-pooling)
- [29. Read Replicas](#29-read-replicas)
- [30. Sharding](#30-sharding)
- [31. Partitioning](#31-partitioning)
- [32. Replication](#32-replication)
- [33. Leader Election](#33-leader-election)

**[Part 5: Consistency & Concurrency](#part-5-consistency--concurrency)**

- [34. CAP Theorem](#34-cap-theorem)
- [35. Eventual Consistency](#35-eventual-consistency)
- [36. Optimistic Locking](#36-optimistic-locking)
- [37. Pessimistic Locking](#37-pessimistic-locking)
- [38. Distributed Locks](#38-distributed-locks)
- [39. Race Conditions](#39-race-conditions)
- [40. Deadlocks](#40-deadlocks)
- [41. Memory Leaks](#41-memory-leaks)
- [42. Garbage Collection](#42-garbage-collection)
- [43. Thread Safety](#43-thread-safety)
- [44. Backpressure](#44-backpressure)

**[Part 6: Scaling & Edge](#part-6-scaling--edge)**

- [45. Autoscaling](#45-autoscaling)
- [46. Horizontal Scaling](#46-horizontal-scaling)
- [47. Vertical Scaling](#47-vertical-scaling)
- [48. CDN](#48-cdn)
- [49. Edge Caching](#49-edge-caching)
- [50. Cache Invalidation](#50-cache-invalidation)

**[Part 7: Deployment & Release](#part-7-deployment--release)**

- [51. Feature Flags](#51-feature-flags)
- [52. Blue-Green Deployment](#52-blue-green-deployment)
- [53. Canary Releases](#53-canary-releases)
- [54. Rolling Deployments](#54-rolling-deployments)
- [55. Rollbacks](#55-rollbacks)
- [56. Health Checks](#56-health-checks)
- [57. Liveness & Readiness Probes](#57-liveness--readiness-probes)

**[Part 8: Observability & Reliability Targets](#part-8-observability--reliability-targets)**

- [58. Monitoring](#58-monitoring)
- [59. Logging](#59-logging)
- [60. Distributed Tracing](#60-distributed-tracing)
- [61. Metrics](#61-metrics)
- [62. Alerts](#62-alerts)
- [63. SLOs](#63-slos)
- [64. SLIs](#64-slis)
- [65. Error Budgets](#65-error-budgets)
- [66. Observability](#66-observability)

**[Part 9: Security](#part-9-security)**

- [67. Secrets Management](#67-secrets-management)
- [68. IAM](#68-iam)
- [69. OAuth](#69-oauth)
- [70. JWT Rotation](#70-jwt-rotation)
- [71. TLS](#71-tls)
- [72. Encryption at Rest](#72-encryption-at-rest)
- [73. Encryption in Transit](#73-encryption-in-transit)
- [74. WAF](#74-waf)
- [75. DDoS Protection](#75-ddos-protection)
- [76. CORS](#76-cors)
- [77. CSRF](#77-csrf)
- [78. SQL Injection](#78-sql-injection)
- [79. XSS](#79-xss)
- [80. SSRF](#80-ssrf)

**[Part 10: Data Safety & Resilience](#part-10-data-safety--resilience)**

- [81. Database Migrations](#81-database-migrations)
- [82. Schema Versioning](#82-schema-versioning)
- [83. Disaster Recovery](#83-disaster-recovery)
- [84. Backups](#84-backups)
- [85. Failover](#85-failover)
- [86. Multi-Region Deployment](#86-multi-region-deployment)
- [87. Chaos Engineering](#87-chaos-engineering)

**[Part 11: Performance & Networking](#part-11-performance--networking)**

- [88. Cost Optimization](#88-cost-optimization)
- [89. Cold Starts](#89-cold-starts)
- [90. Serverless Limits](#90-serverless-limits)
- [91. Latency](#91-latency)
- [92. Throughput](#92-throughput)
- [93. P99 Latency](#93-p99-latency)
- [94. Tail Latency](#94-tail-latency)
- [95. Network Partitions](#95-network-partitions)
- [96. Clock Skew](#96-clock-skew)
- [97. DNS](#97-dns)
- [98. TCP vs UDP](#98-tcp-vs-udp)
- [99. HTTP/2 & HTTP/3](#99-http2--http3)
- [100. gRPC](#100-grpc)

**[Part 12: Integration & Tooling](#part-12-integration--tooling)**

- [101. Webhooks](#101-webhooks)
- [102. API Versioning](#102-api-versioning)
- [103. Semantic Versioning](#103-semantic-versioning)
- [104. Infrastructure as Code](#104-infrastructure-as-code)
- [105. Terraform](#105-terraform)
- [106. Helm Charts](#106-helm-charts)
- [107. Build Caching](#107-build-caching)
- [108. Dependency Hell](#108-dependency-hell)

**[Part 13: Operations & Incident Response](#part-13-operations--incident-response)**

- [109. Production Incidents](#109-production-incidents)
- [110. On-Call](#110-on-call)
- [111. Postmortems](#111-postmortems)

---

## Part 1: Traffic, Delivery & Runtime Basics

### 1. Rate Limiting
**What:** Restricting how many requests a client can make in a time window.
**Why it matters:** Protects against abuse, brute force, and noisy neighbours; keeps the system fair and stable.
**Example (Laravel):**
```php
// app/Providers/AppServiceProvider.php
RateLimiter::for('api', fn (Request $r) =>
    Limit::perMinute(60)->by($r->user()?->id ?: $r->ip())
);

// routes/api.php
Route::middleware('throttle:api')->group(function () {
    Route::get('/tasks', [TaskController::class, 'index']);
});
```
Clients exceeding the limit receive `429 Too Many Requests` with a `Retry-After` header.

### 2. Caching
**What:** Storing the result of expensive work (queries, API calls, renders) so it can be reused.
**Why it matters:** Cuts latency and database load dramatically.
**Example:**
```php
$stats = Cache::remember("project:{$project->id}:stats", now()->addMinutes(5), function () use ($project) {
    return $project->tasks()->selectRaw('status, count(*) c')->groupBy('status')->pluck('c', 'status');
});
```

### 3. Load Balancing
**What:** Spreading incoming traffic across several identical app instances.
**Why it matters:** Higher capacity and availability; one instance dying does not take you down.
**Example (nginx):**
```nginx
upstream app {
    least_conn;
    server 10.0.0.11:8080;
    server 10.0.0.12:8080;
    server 10.0.0.13:8080 backup;
}
server { location / { proxy_pass http://app; } }
```
Prerequisite: stateless apps. Store sessions and cache in Redis, not on local disk.

### 4. Reverse Proxies
**What:** A server that sits in front of your app and forwards requests (nginx, Caddy, HAProxy, Traefik).
**Why it matters:** TLS termination, compression, static files, buffering slow clients, hiding internals.
**Example:** nginx → PHP-FPM. Tell Laravel to trust the proxy so `request()->ip()` and `https` detection work:
```php
// bootstrap/app.php
->withMiddleware(fn (Middleware $m) => $m->trustProxies(at: ['10.0.0.0/8']))
```

### 5. API Gateways
**What:** A single entry point for many services that handles auth, routing, rate limits, logging and transformation.
**Why it matters:** Clients talk to one URL; cross-cutting concerns live in one place.
**Example:** `api.taskflow.com/billing/*` → billing service, `/tasks/*` → core app. Tools: Kong, AWS API Gateway, Traefik, Envoy.
```yaml
# Kong declarative config (simplified)
services:
  - name: billing
    url: http://billing:8000
    routes: [{ name: billing-route, paths: [/billing] }]
    plugins: [{ name: rate-limiting, config: { minute: 100 } }]
```

### 6. CI/CD
**What:** Continuous Integration (auto build and test every push) and Continuous Delivery/Deployment (auto ship passing builds).
**Why it matters:** Small, frequent, safe releases; regressions are caught before users see them.
**Example (GitHub Actions):**
```yaml
name: ci
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    services:
      postgres: { image: postgres:16, env: { POSTGRES_PASSWORD: secret }, ports: ['5432:5432'] }
    steps:
      - uses: actions/checkout@v4
      - uses: shivammathur/setup-php@v2
        with: { php-version: '8.3' }
      - run: composer install --no-interaction --prefer-dist
      - run: php artisan test --parallel
```

### 7. Docker
**What:** Packages your app and its dependencies into an image that runs identically anywhere.
**Why it matters:** "Works on my machine" disappears; deploys become reproducible.
**Example:**
```dockerfile
FROM php:8.3-fpm-alpine
RUN docker-php-ext-install pdo_pgsql opcache
WORKDIR /var/www
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer
COPY . .
RUN composer install --no-dev --optimize-autoloader
CMD ["php-fpm"]
```

### 8. Kubernetes
**What:** An orchestrator that runs containers across a cluster, restarting, scaling and routing for you.
**Why it matters:** Self-healing, declarative deployments, autoscaling, rolling updates.
**Example:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata: { name: taskflow-web }
spec:
  replicas: 3
  selector: { matchLabels: { app: taskflow-web } }
  template:
    metadata: { labels: { app: taskflow-web } }
    spec:
      containers:
        - name: app
          image: registry.example.com/taskflow:1.4.2
          ports: [{ containerPort: 8080 }]
          resources: { requests: { cpu: 250m, memory: 256Mi }, limits: { memory: 512Mi } }
```

---

## Part 2: Resilience & Messaging

### 9. Service Discovery
**What:** How services find each other when instances come and go and IPs change.
**Why it matters:** Hard-coded IPs break the moment you scale or redeploy.
**Example:** In Kubernetes, a `Service` gives a stable DNS name. Your app calls `http://billing.default.svc.cluster.local` and never cares which pod answers. Outside k8s: Consul, AWS Cloud Map, or plain DNS.
```php
Http::baseUrl(config('services.billing.url'))->get('/invoices'); // url comes from env, resolved via DNS
```

### 10. Circuit Breakers
**What:** After repeated failures calling a dependency, "open" the circuit and fail fast instead of piling up requests. Later, allow a trial request ("half-open").
**Why it matters:** Prevents cascading failures and gives the broken service room to recover.
**Example (minimal, using cache):**
```php
function callWithBreaker(string $key, Closure $call, Closure $fallback) {
    if (Cache::get("cb:$key:open")) return $fallback();
    try {
        $r = $call();
        Cache::forget("cb:$key:fails");
        return $r;
    } catch (Throwable $e) {
        $fails = Cache::increment("cb:$key:fails");
        if ($fails >= 5) Cache::put("cb:$key:open", true, 30); // open 30s
        return $fallback();
    }
}
```

### 11. Timeouts
**What:** A maximum time you will wait for an operation.
**Why it matters:** Without timeouts, one slow dependency ties up every worker and the whole app stalls.
**Example:**
```php
Http::connectTimeout(2)->timeout(5)->get('https://api.partner.com/rates');
```
Also set DB `statement_timeout`, queue job `$timeout`, and nginx/PHP-FPM `request_terminate_timeout`.

### 12. Retries
**What:** Re-attempting an operation that failed for transient reasons (network blips, 503s).
**Why it matters:** Many failures are temporary; retries hide them from users. Only retry safe or idempotent operations.
**Example:**
```php
Http::retry(3, 200, throw: false)->post($url, $payload);

class SendInvoice implements ShouldQueue {
    public int $tries = 5;
}
```

### 13. Exponential Backoff
**What:** Increasing the wait between retries (1s, 2s, 4s, 8s...), usually with jitter (random offset).
**Why it matters:** Prevents a "retry storm" where all clients hammer a recovering service simultaneously.
**Example:**
```php
class SyncToCrm implements ShouldQueue {
    public int $tries = 6;
    public function backoff(): array { return [1, 5, 30, 120, 600]; }
}
// With jitter:
$delay = min(300, (2 ** $attempt) + random_int(0, 1000) / 1000);
```

### 14. Idempotency
**What:** Doing an operation many times has the same effect as doing it once.
**Why it matters:** Retries, double-clicks and duplicate webhooks must not charge a customer twice.
**Example (idempotency key):**
```php
public function charge(Request $r) {
    $key = $r->header('Idempotency-Key') ?? abort(422);
    return Cache::lock("idem:$key", 10)->block(5, function () use ($key, $r) {
        if ($saved = Cache::get("idem:result:$key")) return $saved;
        $result = $this->stripe->charge($r->validated());
        Cache::put("idem:result:$key", $result, now()->addDay());
        return $result;
    });
}
```
Also: unique DB constraints, `updateOrCreate`, `ShouldBeUnique` jobs.

### 15. Message Queues
**What:** Work is placed on a queue and processed asynchronously by workers.
**Why it matters:** Fast HTTP responses, smoothing traffic spikes, isolating slow tasks (emails, PDFs, imports).
**Example:**
```php
SendWeeklyReport::dispatch($user)->onQueue('emails');
// php artisan queue:work redis --queue=emails,default --tries=3
```
Use Horizon to monitor Redis queues.

### 16. Pub/Sub
**What:** Publishers emit messages to a topic; any number of subscribers receive them, with no direct coupling.
**Why it matters:** Many consumers react to one event independently.
**Example (Redis):**
```php
Redis::publish('task.completed', json_encode(['id' => $task->id]));

// subscriber (artisan command)
Redis::subscribe(['task.completed'], function ($message) {
    // update analytics, notify Slack...
});
```
Laravel Reverb/Echo broadcasting is Pub/Sub to browsers.

### 17. Event-Driven Architecture
**What:** Components communicate by emitting and reacting to events ("TaskCompleted") instead of calling each other directly.
**Why it matters:** Loose coupling; new behaviour is added by adding listeners.
**Example:**
```php
event(new TaskCompleted($task));

class TaskCompleted { public function __construct(public Task $task) {} }

// Listeners: NotifyAssignee, UpdateBurndown, AwardPoints (each ShouldQueue)
```

### 18. Distributed Transactions
**What:** One logical operation that spans multiple databases or services and must succeed or fail as a whole.
**Why it matters:** A local `DB::transaction` cannot cover "charge Stripe + create subscription + email user".
**Example:** Avoid 2PC where possible. Prefer: local transaction + outbox + events, or a Saga (below).
```php
DB::transaction(function () use ($order) {
    $order->update(['status' => 'paid']);
    OutboxMessage::create(['type' => 'order.paid', 'payload' => $order->toArray()]); // published later by a worker
});
```

### 19. Saga Pattern
**What:** A long operation is split into local steps, each with a compensating action to undo it on failure.
**Why it matters:** Gives you "all or nothing" semantics across services without global locks.
**Example:** Checkout saga: reserve stock → charge card → create shipment. If shipment fails: refund card → release stock.
```php
Bus::chain([
    new ReserveStock($order),
    new ChargeCard($order),
    new CreateShipment($order),
])->catch(fn (Throwable $e) => dispatch(new CompensateOrder($order)))->dispatch();
```

### 20. Dead Letter Queues
**What:** A holding place for messages/jobs that failed too many times.
**Why it matters:** Poison messages do not block the queue, and nothing is silently lost; you can inspect and replay.
**Example:**
```bash
php artisan queue:failed          # list
php artisan queue:retry <uuid>    # replay one
php artisan queue:retry all
```
```php
public function failed(Throwable $e): void { Log::error('Invoice job dead', ['id' => $this->id]); }
```

---

## Part 3: Scheduling & Real-Time

### 21. Cron Jobs
**What:** Commands scheduled to run at fixed times.
**Why it matters:** Reports, cleanups, billing runs, reminders.
**Example:**
```php
// routes/console.php
Schedule::command('invoices:send')->dailyAt('02:00')->onOneServer()->withoutOverlapping();
```
```cron
* * * * * cd /var/www && php artisan schedule:run >> /dev/null 2>&1
```
`onOneServer()` stops duplicates when you run multiple instances.

### 22. WebSockets
**What:** A persistent, two-way connection between browser and server.
**Why it matters:** Instant updates (chat, live boards, tracking) with low overhead.
**Example (Reverb + Echo):**
```php
class TaskMoved implements ShouldBroadcast {
    public function __construct(public Task $task) {}
    public function broadcastOn() { return new PrivateChannel("board.{$this->task->board_id}"); }
}
```
```js
Echo.private(`board.${boardId}`).listen('TaskMoved', e => moveCard(e.task));
```

### 23. Long Polling
**What:** Client sends a request; the server holds it open until there is data or a timeout, then the client immediately asks again.
**Why it matters:** Near-real-time without WebSockets; works through restrictive proxies.
**Example:**
```php
public function poll(Request $r) {
    $until = now()->addSeconds(25);
    while (now()->lt($until)) {
        if ($msgs = Message::where('id', '>', $r->last_id)->get()) return $msgs;
        usleep(500_000);
    }
    return response()->noContent();
}
```
Costly on PHP-FPM (a worker is held per client); prefer SSE or WebSockets at scale.

### 24. Server-Sent Events
**What:** A one-way stream from server to browser over plain HTTP (`text/event-stream`).
**Why it matters:** Simple live feeds (progress bars, notifications, AI token streaming) with auto-reconnect.
**Example:**
```php
return response()->stream(function () {
    while (true) {
        echo "data: " . json_encode(['progress' => Cache::get('import:progress')]) . "\n\n";
        ob_flush(); flush();
        sleep(1);
    }
}, 200, ['Content-Type' => 'text/event-stream', 'Cache-Control' => 'no-cache']);
```
```js
new EventSource('/import/stream').onmessage = e => update(JSON.parse(e.data));
```

---

## Part 4: Databases

### 25. Database Indexing
**What:** A data structure (usually a B-tree) that lets the DB find rows without scanning the whole table.
**Why it matters:** The #1 fix for slow queries. Costs: extra storage and slower writes.
**Example:**
```php
Schema::table('tasks', function (Blueprint $t) {
    $t->index(['project_id', 'status', 'due_at']); // matches WHERE project_id=? AND status=? ORDER BY due_at
});
```
Column order matters: put equality columns first, range/sort last. PostgreSQL extras: partial, GIN (JSONB), expression indexes.

### 26. Query Optimization
**What:** Making queries do less work: select fewer columns/rows, use indexes, avoid functions on indexed columns.
**Why it matters:** Query time dominates most request time.
**Example:**
```sql
EXPLAIN (ANALYZE, BUFFERS)
SELECT id, title FROM tasks WHERE project_id = 42 AND status = 'open' ORDER BY due_at LIMIT 20;
```
Look for `Seq Scan` on big tables, huge row estimates vs. actuals, and sorts spilling to disk.
```php
Task::select('id', 'title')->where('project_id', 42)->cursorPaginate(20); // avoid OFFSET on huge tables
```

### 27. N+1 Queries
**What:** One query to load a list, then one extra query per item for a relation.
**Why it matters:** 100 rows = 101 queries; it kills performance silently.
**Example:**
```php
// Bad
foreach (Task::all() as $t) echo $t->assignee->name;

// Good
foreach (Task::with('assignee:id,name')->get() as $t) echo $t->assignee->name;

// Catch it in dev
Model::preventLazyLoading(! app()->isProduction());
```

### 28. Connection Pooling
**What:** Reusing a limited set of DB connections instead of opening one per request.
**Why it matters:** PostgreSQL connections are heavy (~10MB each); hundreds of PHP workers can exhaust `max_connections`.
**Example:** Put **PgBouncer** between Laravel and Postgres (transaction pooling mode).
```ini
; pgbouncer.ini
pool_mode = transaction
default_pool_size = 20
max_client_conn = 1000
```
In transaction mode avoid session features like advisory locks and prepared statements (set `PDO::ATTR_EMULATE_PREPARES`).

### 29. Read Replicas
**What:** Copies of the primary DB that serve read-only queries.
**Why it matters:** Scales read-heavy workloads and offloads reporting.
**Example:**
```php
// config/database.php
'pgsql' => [
    'read'  => ['host' => ['10.0.0.21', '10.0.0.22']],
    'write' => ['host' => ['10.0.0.20']],
    'sticky' => true, // reads right after a write use the primary
],
```
Beware replication lag: a user may not see data they just saved.

### 30. Sharding
**What:** Splitting data across multiple databases by a key (e.g. `tenant_id`).
**Why it matters:** Scales writes and storage beyond one machine; adds major complexity (cross-shard queries, rebalancing).
**Example:**
```php
function connectionFor(Tenant $t): string {
    return 'shard_' . ($t->id % 4);
}
DB::connection(connectionFor($tenant))->table('tasks')->get();
```
Exhaust indexing, caching, replicas and partitioning before sharding.

### 31. Partitioning
**What:** Splitting one big table into smaller physical pieces inside the same database.
**Why it matters:** Faster scans, easy deletion of old data (drop a partition), better maintenance.
**Example (PostgreSQL):**
```sql
CREATE TABLE events (id bigserial, created_at timestamptz NOT NULL, payload jsonb)
  PARTITION BY RANGE (created_at);
CREATE TABLE events_2026_10 PARTITION OF events
  FOR VALUES FROM ('2026-10-01') TO ('2026-11-01');
```

### 32. Replication
**What:** Continuously copying changes from a primary to one or more replicas.
**Why it matters:** High availability, read scaling, backups, analytics.
**Example:** PostgreSQL streaming replication (physical) or logical replication per table.
```sql
-- on primary
CREATE PUBLICATION app_pub FOR TABLE tasks, projects;
-- on subscriber
CREATE SUBSCRIPTION app_sub CONNECTION 'host=primary dbname=app' PUBLICATION app_pub;
```
Sync = safer but slower; async = faster but may lose last transactions on failover.

### 33. Leader Election
**What:** A group of nodes agrees on one "leader" to perform a task or accept writes.
**Why it matters:** Avoids two nodes doing the same exclusive job (split-brain).
**Example:** Postgres HA with Patroni (etcd/Consul decides the primary), Redis Sentinel, Kubernetes leases. In app code, a lightweight form:
```php
if (Cache::lock('scheduler-leader', 60)->get()) {
    // this instance is the leader for 60s; renew while alive
}
```

---

## Part 5: Consistency & Concurrency

### 34. CAP Theorem
**What:** During a network **P**artition, a distributed store must choose **C**onsistency or **A**vailability.
**Why it matters:** Frames every trade-off in distributed data design.
**Example:** A bank ledger chooses CP (reject requests rather than show wrong balances). A social feed or like counter chooses AP (always respond, reconcile later). Postgres primary = CP-leaning; Cassandra/DynamoDB = tunable AP-leaning.

### 35. Eventual Consistency
**What:** If no new updates arrive, all replicas eventually converge to the same value.
**Why it matters:** Enables speed and availability at scale; the UI must tolerate stale reads.
**Example:** After saving a profile, the read replica or search index lags by ~1s. Mitigate with `sticky` reads, optimistic UI updates, or reading from the primary right after a write.
```php
dispatch(new IndexTaskInSearch($task))->afterCommit(); // search catches up shortly after
```

### 36. Optimistic Locking
**What:** Assume conflicts are rare; detect them at save time using a version check.
**Why it matters:** No locks held, high throughput; the loser retries or is told to refresh.
**Example:**
```php
$updated = Task::where('id', $id)->where('version', $request->version)
    ->update(['title' => $request->title, 'version' => DB::raw('version + 1')]);

if (! $updated) abort(409, 'Task was changed by someone else. Reload and retry.');
```

### 37. Pessimistic Locking
**What:** Lock the row up front so nobody else can change it until you finish.
**Why it matters:** Right choice when conflicts are likely (stock, balances).
**Example:**
```php
DB::transaction(function () use ($id, $qty) {
    $product = Product::lockForUpdate()->findOrFail($id);
    if ($product->stock < $qty) throw new OutOfStock;
    $product->decrement('stock', $qty);
});
```
Keep transactions short; lock in a consistent order to avoid deadlocks.

### 38. Distributed Locks
**What:** A lock shared across servers (usually Redis) so only one process runs a critical section.
**Why it matters:** Prevents duplicate cron runs, double processing, concurrent imports.
**Example:**
```php
Cache::lock("import:{$account->id}", 300)->block(10, function () use ($account) {
    $this->runImport($account);
});
```
Always set an expiry. Locks can still expire mid-work, so combine with idempotency or fencing tokens.

### 39. Race Conditions
**What:** Outcome depends on unlucky timing between concurrent operations.
**Why it matters:** Causes oversold stock, double charges, lost updates; hard to reproduce.
**Example:**
```php
// Bad: read-modify-write
$c = Counter::find(1); $c->value = $c->value + 1; $c->save();

// Good: atomic in the database
Counter::where('id', 1)->increment('value');

// Good: unique constraint + firstOrCreate to dedupe
```

### 40. Deadlocks
**What:** Two (or more) transactions each hold a lock the other needs, so none can proceed.
**Why it matters:** The DB kills one transaction with an error; users see failures.
**Example:** T1 locks row A then B; T2 locks B then A. Fix: lock in the same order, keep transactions short, and retry on deadlock.
```php
DB::transaction(fn () => $this->transfer($a, $b, $amount), attempts: 3); // retries on deadlock
```

### 41. Memory Leaks
**What:** Memory that is allocated and never released, so usage grows until the process dies.
**Why it matters:** Long-running workers (queue, Octane, Reverb) are especially vulnerable.
**Example:** Common PHP causes: static arrays that keep growing, unbounded in-memory collections, event listeners registered repeatedly, loading huge result sets.
```php
Task::chunkById(1000, fn ($chunk) => $this->process($chunk)); // not ->get() on 5M rows
```
```bash
php artisan queue:work --max-jobs=1000 --max-time=3600 --memory=256
```

### 42. Garbage Collection
**What:** Automatic reclaiming of memory no longer referenced.
**Why it matters:** PHP uses reference counting plus a cycle collector; understanding it explains odd memory spikes.
**Example:**
```php
gc_collect_cycles();                     // force a cycle collection
echo memory_get_usage(true) / 1048576;   // MB in use
unset($bigArray);                        // drop references so memory can be freed
```
JVM/Go/Node use tracing GC with pauses that affect tail latency; PHP-FPM sidesteps it by resetting per request.

### 43. Thread Safety
**What:** Code behaves correctly when run by several threads at once.
**Why it matters:** Shared mutable state is the enemy. Classic PHP-FPM is share-nothing, but Octane/Swoole/FrankenPHP keep state between requests.
**Example:**
```php
// Dangerous under Octane: a singleton holding per-request data
$this->app->singleton(CurrentTenant::class);   // leaks tenant across requests!

// Safe: scoped binding, reset every request
$this->app->scoped(CurrentTenant::class);
```

### 44. Backpressure
**What:** A mechanism for a slow consumer to tell producers to slow down.
**Why it matters:** Prevents unbounded queues and out-of-memory crashes.
**Example:** Bound your queue depth and reject or delay when full; limit worker concurrency; stream with `cursor()`/`lazy()` so you only read what you can process.
```php
if (Queue::size('imports') > 10_000) {
    return response()->json(['message' => 'Busy, try later'], 503)->header('Retry-After', 60);
}
```

---

## Part 6: Scaling & Edge

### 45. Autoscaling
**What:** Automatically adding or removing instances based on load.
**Why it matters:** Handles spikes without paying for peak capacity all day.
**Example (Kubernetes HPA):**
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata: { name: taskflow-web }
spec:
  scaleTargetRef: { apiVersion: apps/v1, kind: Deployment, name: taskflow-web }
  minReplicas: 3
  maxReplicas: 20
  metrics:
    - type: Resource
      resource: { name: cpu, target: { type: Utilization, averageUtilization: 65 } }
```
For queue workers, scale on queue length (KEDA) instead of CPU.

### 46. Horizontal Scaling
**What:** Adding more machines/instances ("scale out").
**Why it matters:** Practically unlimited growth and better fault tolerance.
**Example:** 1 server → 5 identical app servers behind a load balancer. Requirements: stateless app, shared Redis for sessions/cache, shared object storage (S3) instead of local disk, centralized logs.

### 47. Vertical Scaling
**What:** Giving one machine more CPU/RAM ("scale up").
**Why it matters:** Simplest first step, no code changes; has a ceiling and is a single point of failure.
**Example:** Upgrade the Postgres host from 4 vCPU/16GB to 16 vCPU/64GB and raise `shared_buffers`/`work_mem`. Often the right answer for databases before sharding.

### 48. CDN
**What:** A global network of edge servers that serve cached content close to users.
**Why it matters:** Lower latency, less origin load, built-in DDoS absorption.
**Example:** Serve `/build/*` (Vite assets), images and fonts from Cloudflare/CloudFront.
```php
// config/filesystems.php: store uploads on S3, front with CDN
'url' => env('AWS_URL'), // https://cdn.example.com
```
```
Cache-Control: public, max-age=31536000, immutable   # for hashed asset filenames
```

### 49. Edge Caching
**What:** Caching full responses (or computing) at CDN edge nodes, not just static files.
**Why it matters:** Public API/HTML responses return in milliseconds from the nearest region.
**Example:**
```php
return response($html)->header('Cache-Control', 'public, s-maxage=300, stale-while-revalidate=60');
```
`s-maxage` is for shared caches (CDN); `stale-while-revalidate` serves stale content while refreshing in the background. Never edge-cache personalized responses without `Vary`.

### 50. Cache Invalidation
**What:** Removing or refreshing cached data when the source changes.
**Why it matters:** Famously hard; stale data is a bug, no caching is slow.
**Example:**
```php
// Tags: flush a group (Redis/Memcached)
Cache::tags(["project:{$id}"])->remember('stats', 600, fn () => $this->stats($id));
Cache::tags(["project:{$id}"])->flush();

// Event-based: bust on change
protected static function booted() {
    static::saved(fn ($t) => Cache::forget("project:{$t->project_id}:stats"));
}
```
Strategies: TTL, write-through, event-based busting, versioned keys (`stats:v7:...`).

---

## Part 7: Deployment & Release

### 51. Feature Flags
**What:** Toggles that turn features on/off at runtime without deploying.
**Why it matters:** Ship dark, roll out gradually, instant kill-switch, A/B tests.
**Example (Laravel Pennant):**
```php
Feature::define('new-board', fn (User $u) => $u->isBetaTester() || lottery(odds: 10, outOf: 100));

if (Feature::active('new-board')) { return view('board-v2'); }
```
Remove stale flags: they become tech debt.

### 52. Blue-Green Deployment
**What:** Two identical environments: Blue (live) and Green (new). Switch traffic after Green passes checks.
**Why it matters:** Near-zero downtime and instant rollback by switching back.
**Example:** Deploy v2 to Green → run smoke tests → flip load balancer/DNS to Green → keep Blue warm for rollback. DB migrations must be backward compatible with both versions.

### 53. Canary Releases
**What:** Send a small percentage of traffic to the new version first and watch metrics.
**Why it matters:** A bad release only hurts 1-5% of users.
**Example (nginx weights):**
```nginx
upstream app {
    server v1.internal:8080 weight=95;
    server v2.internal:8080 weight=5;
}
```
Promote to 25%, 50%, 100% if error rate and latency stay healthy; otherwise roll back.

### 54. Rolling Deployments
**What:** Replace instances gradually (a few at a time) with the new version.
**Why it matters:** No downtime and no need for double infrastructure.
**Example (Kubernetes default):**
```yaml
strategy:
  type: RollingUpdate
  rollingUpdate: { maxUnavailable: 0, maxSurge: 1 }
```
Both versions run side-by-side during rollout, so APIs and DB schema must be compatible.

### 55. Rollbacks
**What:** Returning to the previous known-good version.
**Why it matters:** The fastest mitigation for a bad release is usually undoing it.
**Example:**
```bash
kubectl rollout undo deployment/taskflow-web
```
Keep previous images, make migrations reversible or additive (expand/contract pattern), and never rely on `migrate:rollback` in production for destructive changes.

### 56. Health Checks
**What:** An endpoint or command that reports whether the app is working.
**Why it matters:** Load balancers and orchestrators use it to route traffic and restart failures.
**Example:** Laravel 11 ships a `/up` route. A deeper custom check:
```php
Route::get('/healthz', function () {
    DB::select('select 1');
    Redis::ping();
    return response()->json(['status' => 'ok']);
});
```
Keep it fast and cheap.

### 57. Liveness & Readiness Probes
**What:** Kubernetes checks: **liveness** = "is the process stuck? restart it"; **readiness** = "can it take traffic right now?".
**Why it matters:** Prevents routing traffic to booting/overloaded pods and restarts hung ones.
**Example:**
```yaml
livenessProbe:
  httpGet: { path: /up, port: 8080 }
  periodSeconds: 10
  failureThreshold: 3
readinessProbe:
  httpGet: { path: /healthz, port: 8080 }   # checks DB/Redis
  periodSeconds: 5
```
Do not put dependency checks in liveness, or a DB outage restarts every pod.

---

## Part 8: Observability & Reliability Targets

### 58. Monitoring
**What:** Continuously collecting health and performance data and watching it.
**Why it matters:** You find problems before customers tell you.
**Example:** CPU, memory, queue depth, DB connections, error rate, request latency on a Grafana/Datadog/Nightwatch dashboard; Laravel Pulse and Horizon for app-level views.

### 59. Logging
**What:** Recording events the app emits.
**Why it matters:** Primary tool for debugging what happened.
**Example (structured, with context):**
```php
Log::withContext(['request_id' => $requestId, 'user_id' => auth()->id()]);
Log::warning('payment.failed', ['order' => $order->id, 'reason' => $e->getMessage()]);
```
Log JSON to stdout, ship centrally (Loki, ELK), never log passwords/tokens/card data.

### 60. Distributed Tracing
**What:** Following one request across many services as a tree of timed "spans".
**Why it matters:** Pinpoints which service or query made the request slow.
**Example:** Generate/propagate a trace ID (`traceparent` header, OpenTelemetry).
```php
Http::withHeaders(['traceparent' => request()->header('traceparent')])->get($billingUrl);
```
View in Jaeger, Tempo, Honeycomb, Datadog APM.

### 61. Metrics
**What:** Numeric time-series (counters, gauges, histograms).
**Why it matters:** Cheap to store, great for dashboards and alerts.
**Example:**
```
http_requests_total{route="/tasks",status="500"} 12
http_request_duration_seconds_bucket{le="0.5"} 9812
queue_depth{queue="emails"} 340
```
Prefer histograms for latency (so you can compute P95/P99). Avoid high-cardinality labels like `user_id`.

### 62. Alerts
**What:** Automatic notifications when a metric crosses a threshold.
**Why it matters:** Humans cannot stare at dashboards; bad alerts cause fatigue.
**Example (Prometheus):**
```yaml
- alert: HighErrorRate
  expr: sum(rate(http_requests_total{status=~"5.."}[5m])) / sum(rate(http_requests_total[5m])) > 0.02
  for: 10m
  labels: { severity: page }
```
Alert on symptoms users feel (errors, latency), not every CPU blip. Each alert should be actionable.

### 63. SLOs
**What:** Service Level **Objectives**: the reliability target you promise internally.
**Why it matters:** Turns "be reliable" into a measurable goal that guides priorities.
**Example:** "99.9% of API requests succeed and 95% finish under 300ms over 30 days."

### 64. SLIs
**What:** Service Level **Indicators**: the actual measurements that SLOs are based on.
**Why it matters:** You cannot hit a target you do not measure.
**Example:** `SLI = successful_requests / total_requests`; latency SLI = share of requests faster than 300ms.

### 65. Error Budgets
**What:** The allowed unreliability: `100% - SLO`.
**Why it matters:** Balances shipping speed and stability. Budget left → ship faster; budget burned → freeze features, fix reliability.
**Example:** 99.9% over 30 days = ~43 minutes of allowed downtime. Incident used 30 minutes → only ~13 left this month.

### 66. Observability
**What:** Ability to understand internal state from outputs (logs, metrics, traces) and ask new questions without shipping new code.
**Why it matters:** Monitoring tells you *that* something broke; observability helps you find *why*.
**Example:** A spike in 500s → trace shows `/export` slow → span shows a missing index on `tasks.project_id` → log line carries the offending tenant ID. Correlate all three with a shared `request_id`.

---

## Part 9: Security

### 67. Secrets Management
**What:** Storing and distributing credentials (API keys, DB passwords) securely.
**Why it matters:** Leaked secrets are a top cause of breaches.
**Example:** Never commit `.env`. Use a vault (AWS Secrets Manager, HashiCorp Vault, Doppler, Kubernetes Secrets with encryption). Rotate regularly.
```bash
php artisan env:encrypt --env=production   # encrypted file safe to commit; key stored elsewhere
```
Add secret scanning (gitleaks) to CI.

### 68. IAM
**What:** Identity and Access Management: who (identity) can do what (permissions) on which resource.
**Why it matters:** Least privilege limits the blast radius of any compromise.
**Example (AWS policy: app can only read/write one bucket prefix):**
```json
{ "Effect": "Allow", "Action": ["s3:GetObject", "s3:PutObject"],
  "Resource": "arn:aws:s3:::taskflow-uploads/tenants/*" }
```
In-app equivalent: Laravel Gates/Policies and roles/permissions.

### 69. OAuth
**What:** A protocol for delegated access: "let this app act on my behalf" without sharing my password (OAuth 2.0; OpenID Connect adds identity).
**Why it matters:** "Login with Google/GitHub", API access for third parties.
**Example:**
```php
// Laravel Socialite
return Socialite::driver('github')->redirect();

$ghUser = Socialite::driver('github')->user();
$user = User::updateOrCreate(['github_id' => $ghUser->id], ['email' => $ghUser->email]);
```
Use Authorization Code flow with PKCE for SPAs/mobile. Laravel Passport/Sanctum for your own API.

### 70. JWT Rotation
**What:** Regularly replacing signing keys and issuing short-lived access tokens with refresh tokens.
**Why it matters:** Limits damage when a token or key leaks; JWTs cannot be easily revoked once issued.
**Example:** Access token lifetime 15 min; refresh token 30 days, single-use (rotated on every refresh); publish keys via JWKS with a `kid` header so old and new keys overlap during rotation.
```php
$payload = ['sub' => $user->id, 'iat' => time(), 'exp' => time() + 900];
JWT::encode($payload, $privateKey, 'RS256', keyId: 'key-2026-10');
```

### 71. TLS
**What:** The protocol behind HTTPS: encrypts traffic and authenticates the server.
**Why it matters:** Stops eavesdropping and tampering; required by browsers and compliance.
**Example:**
```nginx
ssl_protocols TLSv1.2 TLSv1.3;
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
```
Automate certificates with Let's Encrypt/Caddy/cert-manager. Force HTTPS in Laravel: `URL::forceScheme('https')`.

### 72. Encryption at Rest
**What:** Data is encrypted while stored on disk/DB/backups.
**Why it matters:** Protects from stolen disks, leaked backups, and some insider risks.
**Example:** Enable disk/volume encryption (LUKS, EBS KMS, RDS encryption). Field-level for sensitive data:
```php
protected function casts(): array {
    return ['tax_id' => 'encrypted', 'api_token' => 'encrypted'];
}
```
Hash passwords (never encrypt): `Hash::make($password)`.

### 73. Encryption in Transit
**What:** Data is encrypted while moving between systems.
**Why it matters:** Internal networks are not automatically safe.
**Example:** HTTPS to clients; TLS for Postgres (`sslmode=verify-full`), Redis TLS (`rediss://`), service mesh mTLS between services, SMTP with STARTTLS.
```env
DB_SSLMODE=verify-full
REDIS_SCHEME=tls
```

### 74. WAF
**What:** Web Application Firewall: filters malicious HTTP traffic (SQLi, XSS, bad bots) before it reaches your app.
**Why it matters:** Cheap, fast protection layer and virtual patching during incidents.
**Example:** Cloudflare WAF, AWS WAF, ModSecurity + OWASP Core Rule Set. Rule: block requests where a query string matches SQLi patterns; rate-limit `/login` per IP. A WAF complements, not replaces, secure code.

### 75. DDoS Protection
**What:** Defences against floods of traffic meant to knock you offline.
**Why it matters:** Availability is a security property.
**Example:** Put a CDN/proxy in front (Cloudflare, AWS Shield), hide origin IP, enable rate limiting and bot challenges, cache aggressively, auto-scale, and restrict the origin firewall to the CDN's IP ranges only. Application-layer floods (expensive endpoints) need per-route limits too.

### 76. CORS
**What:** Browser rule controlling which *other origins* may call your API from JavaScript.
**Why it matters:** Misconfiguration (`*` with credentials) exposes user data; too strict breaks your frontend.
**Example:**
```php
// config/cors.php
'paths' => ['api/*'],
'allowed_origins' => ['https://app.taskflow.com'],
'allowed_methods' => ['GET', 'POST', 'PUT', 'DELETE'],
'supports_credentials' => true,
```
CORS is enforced by browsers only; it does not protect your API from curl/servers.

### 77. CSRF
**What:** Cross-Site Request Forgery: a malicious site makes the victim's browser send an authenticated request to your site.
**Why it matters:** Cookie-based sessions are sent automatically, enabling unwanted actions.
**Example:**
```blade
<form method="POST" action="/tasks/1/delete">
    @csrf
    <button>Delete</button>
</form>
```
Laravel's `VerifyCsrfToken` checks the token. Add `SameSite=Lax/Strict` cookies. Token-based APIs (Bearer header) are not CSRF-prone.

### 78. SQL Injection
**What:** Attacker input is interpreted as SQL.
**Why it matters:** Can leak or destroy the entire database.
**Example:**
```php
// Vulnerable
DB::select("SELECT * FROM users WHERE email = '$email'");

// Safe: bindings
DB::select('SELECT * FROM users WHERE email = ?', [$email]);
User::where('email', $email)->first();

// Careful with raw column names/order by: whitelist them
$col = in_array($req->sort, ['title', 'due_at']) ? $req->sort : 'id';
```

### 79. XSS
**What:** Cross-Site Scripting: attacker-supplied script runs in another user's browser.
**Why it matters:** Steals sessions, performs actions as the victim.
**Example:**
```blade
{{ $comment->body }}      {{-- escaped, safe --}}
{!! $comment->body !!}    {{-- raw, dangerous unless sanitized --}}
```
Sanitize rich text (HTMLPurifier), set a Content-Security-Policy, mark cookies `HttpOnly`. In Livewire/Alpine, avoid `x-html` with user data.

### 80. SSRF
**What:** Server-Side Request Forgery: attacker makes *your server* fetch internal URLs (cloud metadata, admin panels).
**Why it matters:** Can expose cloud credentials (`http://169.254.169.254/...`).
**Example (webhook URL feature):**
```php
$host = parse_url($url, PHP_URL_HOST);
$ip = gethostbyname($host);
if (! filter_var($ip, FILTER_VALIDATE_IP, FILTER_FLAG_NO_PRIV_RANGE | FILTER_FLAG_NO_RES_RANGE)) {
    abort(422, 'URL not allowed');
}
Http::withoutRedirecting()->timeout(5)->post($url, $payload); // also re-check after DNS to avoid rebinding
```
Use allowlists, block redirects, and require IMDSv2 on AWS.

---

## Part 10: Data Safety & Resilience

### 81. Database Migrations
**What:** Versioned, repeatable scripts that change the DB schema.
**Why it matters:** Schema changes travel with code across all environments.
**Example:**
```php
Schema::table('tasks', function (Blueprint $t) {
    $t->timestamp('archived_at')->nullable()->after('status');
});
```
Zero-downtime: add nullable column → deploy code → backfill in batches → add constraint/index (`CREATE INDEX CONCURRENTLY`) → later drop old columns (expand/contract).

### 82. Schema Versioning
**What:** Tracking the schema's version and keeping app and DB compatible over time.
**Why it matters:** Rolling deploys run old and new code at once.
**Example:** Laravel's `migrations` table records applied migrations. For events/APIs/queues, include a version: `{"type":"task.created","v":2,...}` and support the previous version during transition. Never rename a column in one step; add the new one, dual-write, switch reads, drop the old.

### 83. Disaster Recovery
**What:** The plan and tooling to restore service after a major failure (region outage, corruption, ransomware).
**Why it matters:** Defines how long you are down and how much data you lose.
**Example:** Define **RTO** (max downtime, e.g. 1h) and **RPO** (max data loss, e.g. 5 min). Write a runbook, store backups in another region/account, and **practice** restores quarterly. An untested backup is a hope, not a backup.

### 84. Backups
**What:** Copies of data that can be restored later.
**Why it matters:** Protects against deletion, bugs, corruption and attacks; replication alone does *not* (it copies mistakes).
**Example:**
```bash
pg_dump -Fc -h db -U app taskflow | gzip > taskflow_$(date +%F).dump.gz
aws s3 cp taskflow_*.dump.gz s3://backups-eu/ --sse
```
Better: continuous WAL archiving (pgBackRest/Barman) for point-in-time recovery. Follow 3-2-1 (3 copies, 2 media, 1 offsite) and test restores. Package: `spatie/laravel-backup`.

### 85. Failover
**What:** Automatically switching to a standby when the primary fails.
**Why it matters:** Cuts downtime from hours to seconds.
**Example:** Patroni promotes a Postgres replica; Redis Sentinel promotes a replica; load balancer removes unhealthy app nodes. Laravel reconnects if you handle exceptions and keep timeouts short. Beware split-brain: ensure the old primary is fenced.

### 86. Multi-Region Deployment
**What:** Running the system in multiple geographic regions.
**Why it matters:** Survives regional outages and gives users lower latency.
**Example:** Active-passive (standby region takes over via DNS/Global Load Balancer) is simpler. Active-active needs data replication and conflict resolution (CAP trade-offs). Route users with GeoDNS; keep data residency laws in mind.

### 87. Chaos Engineering
**What:** Deliberately injecting failures in a controlled way to test resilience.
**Why it matters:** Finds weaknesses before real incidents do.
**Example:** Kill a random pod, add 500ms latency to Redis, drop the replica, then verify alerts fire and users see degraded but working behaviour. Tools: Chaos Mesh, Gremlin, AWS FIS. Start in staging with a clear hypothesis and a stop button.
```bash
kubectl delete pod -l app=taskflow-web --field-selector=status.phase=Running --wait=false
```

---

## Part 11: Performance & Networking

### 88. Cost Optimization
**What:** Getting the same outcomes for less cloud spend.
**Why it matters:** Infrastructure bills grow quietly and can sink a SaaS margin.
**Example:** Right-size instances, use autoscaling, buy reserved/savings plans for steady load, spot instances for queue workers, S3 lifecycle rules (move old files to cold storage), cap log retention, cache to avoid DB upgrades, tag resources per team/tenant to see who spends what, and set budget alerts.

### 89. Cold Starts
**What:** The delay when a new instance (serverless function, new pod, cold cache) handles its first request.
**Why it matters:** Causes slow first responses, especially after scale-to-zero.
**Example:** Lambda/Vapor PHP function boot adds hundreds of ms. Reduce: smaller package, `php artisan config:cache route:cache event:cache`, OPcache preloading, provisioned concurrency, warm-up requests, and Octane to keep the app booted.

### 90. Serverless Limits
**What:** Hard constraints of serverless platforms: max execution time, memory, payload size, concurrency, ephemeral disk.
**Why it matters:** Designs that ignore them fail at scale or cost a lot.
**Example (AWS Lambda/Laravel Vapor):** ~15 min max runtime, 6 MB sync payload, `/tmp` only, concurrency cap per account, no long-lived connections (use RDS Proxy for DB). Long imports → break into queued chunks; big uploads → pre-signed S3 URLs; WebSockets → managed service.

### 91. Latency
**What:** Time for one request to complete (or one hop to travel).
**Why it matters:** Directly affects user experience and conversion.
**Example:** Total = DNS + TLS + network + app + DB + external calls. Improve by caching, indexing, fewer round trips (eager loading), parallel calls, CDN, keep-alive connections, compression.
```php
$responses = Http::pool(fn (Pool $p) => [$p->get($a), $p->get($b), $p->get($c)]); // concurrent
```

### 92. Throughput
**What:** Work completed per unit time (requests/second, jobs/minute).
**Why it matters:** Capacity planning; related to latency but not the same (batching can raise throughput and latency).
**Example:** Little's Law: concurrency = throughput × latency. If each request takes 200ms and you have 20 PHP-FPM workers, max ≈ 100 req/s. Measure with k6/wrk/Apache Bench.
```bash
k6 run --vus 50 --duration 60s loadtest.js
```

### 93. P99 Latency
**What:** The 99th percentile: 99% of requests are faster than this; 1% are slower.
**Why it matters:** Averages hide pain. A 100ms average can coexist with a 3s P99.
**Example:** Report P50/P95/P99 per endpoint. If P99 = 2.4s on `/dashboard`, find the slow 1% (large tenants? cold cache? lock waits?) with traces and histograms.

### 94. Tail Latency
**What:** The slowest slice of requests (P99, P99.9).
**Why it matters:** In fan-out systems, one slow call among many makes the whole request slow, so tail dominates real experience.
**Example:** A page calling 10 services, each with 1% slow chance, is slow ~10% of the time. Mitigate with timeouts, hedged requests, caching, reducing fan-out, avoiding GC/lock pauses, and load shedding.

### 95. Network Partitions
**What:** Network failure splits a system into groups that cannot talk to each other (though each may be healthy).
**Why it matters:** Causes split-brain and inconsistent data; it is the "P" in CAP.
**Example:** Two DB nodes both think they are primary after a link failure. Prevent with quorum (majority required, e.g. 2 of 3), fencing, and leader leases. In app code: timeouts, retries with idempotency, and graceful degradation.

### 96. Clock Skew
**What:** Different machines' clocks disagree.
**Why it matters:** Breaks ordering, token expiry, locks, cache TTLs, and "last write wins".
**Example:** A JWT looks "not yet valid" because the server is 3 seconds behind. Fix: run NTP/chrony, allow small leeway, use DB time for ordering, or use logical clocks/sequence numbers.
```php
JWT::$leeway = 30; // seconds
```

### 97. DNS
**What:** The system that turns names (`app.example.com`) into IP addresses.
**Why it matters:** Misconfigured DNS or TTLs cause outages and slow failovers.
**Example:** Records: A/AAAA (IP), CNAME (alias), MX (mail), TXT (SPF/DKIM/verification). Lower TTL before migrations (e.g. 60s). Debug:
```bash
dig +short app.example.com
dig app.example.com @1.1.1.1 +trace
```
"It's always DNS" is a joke with truth in it.

### 98. TCP vs UDP
**What:** TCP = reliable, ordered, connection-based. UDP = fast, connectionless, no guarantees.
**Why it matters:** Choose by need: correctness vs. latency.
**Example:** HTTP/1.1, HTTP/2, Postgres, Redis, SSH → TCP. DNS lookups, VoIP/video, games, and HTTP/3 (QUIC) → UDP.
```php
$sock = stream_socket_client('udp://127.0.0.1:8125');
fwrite($sock, "taskflow.jobs.processed:1|c"); // StatsD metric: loss is acceptable
```

### 99. HTTP/2 & HTTP/3
**What:** HTTP/2 multiplexes many requests over one TCP connection (header compression, server push dropped). HTTP/3 runs on QUIC (UDP) avoiding TCP head-of-line blocking and speeding up connection setup.
**Why it matters:** Faster page loads, especially on mobile/lossy networks.
**Example:**
```nginx
listen 443 ssl;
http2 on;
listen 443 quic reuseport;       # HTTP/3
add_header Alt-Svc 'h3=":443"; ma=86400';
```
With HTTP/2 stop domain sharding and giant sprite/bundle hacks.

### 100. gRPC
**What:** A high-performance RPC framework using HTTP/2 and Protocol Buffers (binary, typed contracts, streaming).
**Why it matters:** Efficient service-to-service calls with generated clients.
**Example:**
```proto
service Billing { rpc CreateInvoice (InvoiceRequest) returns (InvoiceReply); }
message InvoiceRequest { string customer_id = 1; int64 amount_cents = 2; }
```
In PHP use the `grpc` extension or RoadRunner; browsers need gRPC-Web. Choose REST for public APIs, gRPC for internal, latency-sensitive calls.

---

## Part 12: Integration & Tooling

### 101. Webhooks
**What:** HTTP callbacks: a service POSTs to your URL when an event happens.
**Why it matters:** Real-time integration without polling (Stripe, GitHub, Slack).
**Example (receive safely):**
```php
Route::post('/webhooks/stripe', function (Request $r) {
    $sig = $r->header('Stripe-Signature');
    $event = \Stripe\Webhook::constructEvent($r->getContent(), $sig, config('services.stripe.webhook_secret')); // verify signature

    ProcessStripeEvent::dispatch($event->id, $event->toArray()); // ack fast, work async
    return response()->noContent();
});
```
Make handlers idempotent (events can repeat), store event IDs, and respond 2xx quickly.

### 102. API Versioning
**What:** Evolving an API without breaking existing clients.
**Why it matters:** Mobile apps and integrators cannot update instantly.
**Example:**
```php
Route::prefix('v1')->group(base_path('routes/api_v1.php'));
Route::prefix('v2')->group(base_path('routes/api_v2.php'));
```
Other styles: header (`Accept: application/vnd.taskflow.v2+json`) or date-based (Stripe). Prefer additive changes; announce deprecations with `Deprecation`/`Sunset` headers.

### 103. Semantic Versioning
**What:** `MAJOR.MINOR.PATCH`: major = breaking, minor = backwards-compatible feature, patch = bug fix.
**Why it matters:** Lets consumers judge upgrade risk.
**Example:** `1.4.2 → 1.4.3` (fix), `1.5.0` (feature), `2.0.0` (breaking). In Composer: `"vendor/pkg": "^1.4"` allows `>=1.4.0 <2.0.0`; `~1.4.2` allows `>=1.4.2 <1.5.0`. Tag releases: `git tag v1.5.0`.

### 104. Infrastructure as Code
**What:** Defining infrastructure (servers, networks, DBs) in version-controlled files.
**Why it matters:** Reproducible environments, code review for infra, easy disaster recovery.
**Example:** Terraform/Pulumi/CloudFormation for cloud; Ansible for configuration; Docker/Compose/Helm for runtime. Workflow: PR → `plan` reviewed → `apply` by CI. Avoid manual console changes (drift).

### 105. Terraform
**What:** A declarative IaC tool: describe desired state, Terraform computes and applies the diff.
**Why it matters:** Multi-cloud, huge provider ecosystem, plan-before-apply safety.
**Example:**
```hcl
resource "aws_db_instance" "main" {
  identifier        = "taskflow-prod"
  engine            = "postgres"
  engine_version    = "16"
  instance_class    = "db.t4g.large"
  allocated_storage = 100
  storage_encrypted = true
  multi_az          = true
}
```
```bash
terraform init && terraform plan -out=tfplan && terraform apply tfplan
```
Store state remotely (S3 + locking), never commit state or secrets.

### 106. Helm Charts
**What:** The package manager for Kubernetes: templated manifests plus values.
**Why it matters:** Deploy the same app to dev/staging/prod with different configs; versioned releases and easy rollback.
**Example:**
```yaml
# values.yaml
image: { repository: registry.example.com/taskflow, tag: "1.4.2" }
replicaCount: 3
ingress: { host: app.taskflow.com }
```
```bash
helm upgrade --install taskflow ./chart -f values-prod.yaml -n prod
helm rollback taskflow 3
```

### 107. Build Caching
**What:** Reusing results of previous builds (layers, dependencies, compiled assets).
**Why it matters:** Faster CI and deploys, lower cost.
**Example:** Order Dockerfile so rarely-changing steps come first:
```dockerfile
COPY composer.json composer.lock ./
RUN composer install --no-dev --no-scripts   # cached until lockfile changes
COPY . .
```
```yaml
- uses: actions/cache@v4
  with: { path: vendor, key: composer-${{ hashFiles('composer.lock') }} }
```
Use BuildKit cache mounts and cache `node_modules`/Vite output too.

### 108. Dependency Hell
**What:** Conflicting, outdated or transitive dependency requirements that you cannot satisfy simultaneously.
**Why it matters:** Blocks upgrades, causes security gaps and weird bugs.
**Example:**
```bash
composer why-not laravel/framework 12.0   # who blocks the upgrade?
composer outdated --direct
composer audit                             # known vulnerabilities
```
Commit `composer.lock`, upgrade regularly in small steps, avoid abandoned packages, keep few dependencies, and use Dependabot/Renovate.

---

## Part 13: Operations & Incident Response

### 109. Production Incidents
**What:** Unplanned events that degrade or break the live service.
**Why it matters:** How you respond determines user trust.
**Example lifecycle:** Detect (alert) → Triage and declare severity (SEV1-SEV3) → Assign roles (incident commander, comms, fixer) → **Mitigate first** (rollback, feature-flag off, scale up) → Communicate on a status page → Resolve → Postmortem. Root-cause analysis comes *after* users are unblocked.

### 110. On-Call
**What:** A rotation where engineers are reachable to respond to alerts outside normal hours.
**Why it matters:** Sustained reliability needs coverage without burning people out.
**Example:** Weekly primary/secondary rotation (PagerDuty/Opsgenie), clear escalation policy, a runbook per alert, handoff notes, compensation/time off after a bad week, and a rule: if an alert wakes you up and needs no action, fix or delete the alert.
```markdown
## Runbook: HighQueueDepth
1. Check Horizon: failed vs processed jobs
2. If a single job class is failing → `php artisan queue:pause` that queue, inspect logs
3. Scale workers: `kubectl scale deploy/worker --replicas=10`
```

### 111. Postmortems
**What:** A written, blameless review after an incident: what happened, why, and how to prevent repeats.
**Why it matters:** Turns failures into lasting improvements.
**Example template:**
```markdown
# Postmortem: Checkout failures on 2026-10-12
**Impact:** 18% of checkouts failed for 47 min (~$12k)
**Timeline (UTC):** 14:02 deploy → 14:09 alert → 14:20 rollback started → 14:49 recovered
**Root cause:** Migration added a NOT NULL column without default; old pods crashed on insert.
**What went well / badly:** Alert fired in 7 min / rollback was manual and slow
**Action items:** 
- [ ] CI check for unsafe migrations (owner: Bilal, due: 11/15)
- [ ] One-click rollback in pipeline
```
Blameless means asking "how did the system allow this?", not "who did this?".

---

## Appendix: Quick Cheat Sheet

| Problem | Reach for |
|---|---|
| Slow page | Caching, indexes, N+1 fix, CDN |
| Traffic spikes | Autoscaling, queues, rate limits, backpressure |
| Flaky dependency | Timeouts, retries + backoff, circuit breaker |
| Duplicate side effects | Idempotency keys, unique constraints, locks |
| Cross-service workflows | Events, outbox, saga |
| Risky release | Feature flags, canary, rollback plan |
| "What just broke?" | Logs + metrics + traces, `request_id` |
| Data loss fear | Backups + tested restores + PITR |
| Security basics | Least privilege, TLS, parameterized queries, escaping, CSRF tokens |

## Changelog
- 2026-10-30: Initial version covering 111 concepts.

## Maintaining the TOC

Save as `build_toc.py` next to this file and run `python3 build_toc.py`. It rebuilds the table of contents from the `##` and `###` headings (skipping code blocks) and rewrites the README in place.

```python
import re, pathlib

FENCE = "`" * 3
p = pathlib.Path("README.md")
text = p.read_text()
# drop the old TOC: it sits between the first and second "---" separators
head, _, rest = text.partition("\n---\n")
_, _, body = rest.partition("\n---\n")

def slug(t):
    return re.sub(r"[^\w\- ]", "", t.strip().lower()).replace(" ", "-")

toc, in_code = ["## Table of Contents", ""], False
for line in body.splitlines():
    if line.startswith(FENCE):
        in_code = not in_code
    if in_code:
        continue
    if line.startswith("## ") and not line.startswith(("## Appendix", "## Changelog", "## Maintaining")):
        toc.append(f"\n**[{line[3:]}](#{slug(line[3:])})**\n")
    elif line.startswith("### "):
        toc.append(f"- [{line[4:]}](#{slug(line[4:])})")

p.write_text(head + "\n---\n\n" + "\n".join(toc) + "\n\n---\n" + body)
```
