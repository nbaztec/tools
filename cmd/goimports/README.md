## Notes

The goimports file is modified from its original behavior, to incorporate the following tweaks. 

### Ignore Line Breaks
Original `goimports` would leave the new lines within the imports intact. The modification squeezes all imports
into a single block before running `goimports`

```
$ goimports ./my-app
```

```
import (
    "fmt"

    "github.com/protos/types"

    "github.com/third-party/http"

    "github.com/john-doe/fmt/strings"

    "github.com/john-doe/my-app/foo"
)
```

```
import (
    "fmt"
    
    "github.com/protos/types"
    "github.com/third-party/http"

    "github.com/john-doe/fmt/strings"
    "github.com/john-doe/my-app/foo"
)
```

### Local Sub-Groups
 `-local` is able to separate sub-groups via `;` delimiter

```
$ goimports -w -local github.com/john-doe/http;github.com/john-doe/fmt,github.com/john-doe/my-app
```

```
import (
    "github.com/john-doe/fmt/strings"
    "github.com/john-doe/http/client"
    "github.com/john-doe/my-app/foo"
)
```

```
import (
    "github.com/john-doe/http/client"
   
    "github.com/john-doe/fmt/strings"
    "github.com/john-doe/my-app/foo"
)
```

### Forced Third-Party Groups
The modified `goimports` will also force a grouping for all third-party libs that are repeated 3 or more times.

```
$ goimports ./my-app
```

```
import (
    "fmt"

    "github.com/protos/types"
    "github.com/alice/foo"
    "github.com/bob/bar"
    "github.com/third-party/http"
    "github.com/third-party/http/transport"
    "github.com/third-party/http/transport/udp"
    "github.com/third-party/http/log"

    "github.com/john-doe/my-app/foo"
)
```

```
import (
    "fmt"

    "github.com/protos/types"
    "github.com/alice/foo"
    "github.com/bob/bar"

    "github.com/third-party/http"
    "github.com/third-party/http/transport"
    "github.com/third-party/http/transport/udp"
    "github.com/third-party/http/log"

    "github.com/john-doe/my-app/foo"
)
```