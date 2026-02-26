# clay-queue

SQLite-backed persistent job queue for Clay.

## Usage

```clay
db = Db open("app.db")
queue = JobQueue new(db, "jobs")
```

## Methods

### `new(db, tableName)`

Creates a new JobQueue backed by the given database. Automatically creates the
table if it does not exist.

```clay
db = Db open("app.db")
queue = JobQueue new(db, "jobs")
```

### `push(type, payload)`

Adds a new pending job to the queue.

```clay
queue push("email", "user_id=42")
queue push("report", "month=june")
```

### `pop()`

Retrieves the next pending job, marks it as `'processing'`, and returns it as a
Dict with keys `id`, `type`, `payload`, and `status`. Returns `nil` if no
pending jobs exist.

```clay
job = queue pop()
(job != nil) ifTrue {
  job get("type")    // => "email"
  job get("payload") // => "user_id=42"
}
```

### `complete(job)`

Marks a job as `'done'`.

```clay
job = queue pop()
// ... do work ...
queue complete(job)
```

### `fail(job, reason)`

Marks a job as `'failed'` and stores the reason in the payload.

```clay
job = queue pop()
queue fail(job, "connection timeout")
```

### `pending()`

Returns the count of pending jobs.

```clay
queue pending() // => 3
```

### `processing()`

Returns the count of jobs currently being processed.

```clay
queue processing() // => 1
```

### `failed()`

Returns the count of failed jobs.

```clay
queue failed() // => 2
```

### `retry()`

Resets all failed jobs back to `'pending'` so they can be processed again.

```clay
queue retry()
queue pending() // failed jobs are now pending again
```

### `clear()`

Deletes all completed (`'done'`) jobs from the queue.

```clay
queue clear()
```

### `size()`

Returns the total count of all jobs in the queue regardless of status.

```clay
queue size() // => 10
```

## Schema

The backing table has the following columns:

| Column       | Type    | Description                          |
|--------------|---------|--------------------------------------|
| `id`         | INTEGER | Auto-incrementing primary key        |
| `type`       | TEXT    | Job type identifier                  |
| `payload`    | TEXT    | Job data / arguments                 |
| `status`     | TEXT    | `pending`, `processing`, `done`, or `failed` |
| `created_at` | TEXT    | Timestamp when the job was created   |
| `updated_at` | TEXT    | Timestamp of last status change      |
