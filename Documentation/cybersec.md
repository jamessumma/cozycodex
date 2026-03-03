# Security Practices

### Handling keys
This section describes some general rules for handling keys that production systems use, including the conventions used in this project.
Some general rules for handling keys:
- Secret keys (such as API keys) are never hardcoded into the app. 
- Sensitive secrets are never shipped in the client app.
- Some client-keys must be exposed in the app, in this case they must be treated as public and protected using provider restrictions, least-privilege scopes, quotas, and monitoring.
- Production & staging secrets are stored in a secret manager and are injected at runtime. 

#### Less sensitive keys
A "less sensitive key" is a **client-exposed** key/identifier that cannot grant privileged access on its own, or is protected via app signing identity, APIs, and quotas. 
If a key is shipped with the app, even after it is shipped as an **.apk** or **.aab**, even if it is obfuscated, it can still be derived by a bad actor. 
Therefore, the only keys to be shipped with the app at any time are these "less sensitive" keys. 
Still, keys should never be committed to the repo. Standard practice is to use a `secrets.properties` file for storing keys in the root of the project. 
`build.gradle` can load variables from this `secrets.properties` file, so we don't have to hardcode the values. 
At that point, add the `secrets.properties` file to `.gitignore`.
Commit a `secrets.properties.example` with placeholder values to commit to the repo showing other developers examples of what needs to be present.

#### Secret keys and sensitive information
A secret key is a key/identifier that can grant privileged access on its own, or can cause damage if it is shipped with the app.
Sensitive information and secrets should never be shipped with the app. 
Instead, the client communicates with a backend server over TLS; the backend retrieves required secrets from the secret manager, validates requests, performs privileged operations, and returns only strictly necessary information to the client.
