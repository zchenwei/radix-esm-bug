```bash
git clone git@github.com:zchenwei/radix-esm-bug.git
cd radix-esm-bug/
yarn install && yarn dev
```

Throws:

```
SyntaxError: Named export 'Track' not found. The requested module '@radix-ui/react-slider' is a CommonJS module, which may not support all module.exports as named exports.
CommonJS modules can always be imported via the default export, for example using:

import pkg from '@radix-ui/react-slider';

Node.js v18.12.0
```

The problem is that Node does not know `module` field in `package,json`. This proposal is adpoted by main build tools but not adopted by Node and instead use the `exports` field. So it will always fallback to the `main` field and treat it as a CJS package.
