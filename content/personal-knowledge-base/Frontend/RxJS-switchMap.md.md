```typescript
import { fromEvent } from 'rxjs';
import { switchMap } from 'rxjs/operators';

// Cancels previous search HTTP requests if a new input event occurs
const searchInput$ = fromEvent(document.getElementById('search'), 'input');
const result$= searchInput$.pipe(
  switchMap(event => fetchSearchResults(event.target.value))
);
```

```mermaid
sequenceDiagram
    autonumber
    User->>Input: Types "React"
    Input->>RxJS: switchMap() triggers Request 1
    User->>Input: Types "React Router"
    Input->>RxJS: switchMap() cancels Request 1
    RxJS->>API: Sends Request 2
    API-->>User: Returns "React Router" Results
```