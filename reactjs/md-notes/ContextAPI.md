## Class base

```javascript
static contextType = AuthContext;

...

{this.context.isAuthenticated ? <p>Logged In</p> : <p>Not Logged In</p>}
```

## Function Component

```javascript
import React, { useContext } from "react";
import AuthContext from "...";
```

```javascript
...
const authContext = useContext(AuthContext);
...
<SomeThing onClick={authContext.login}>
        Login
</SomeThing>
...
```
