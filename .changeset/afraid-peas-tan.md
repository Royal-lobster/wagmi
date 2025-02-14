---
'@wagmi/core': patch
---

**Breaking**: The configuration passed to the `writeContract` action now needs to be:

- prepared with the `prepareWriteContract` action **(new functionality)**, or
- dangerously unprepared **(previous functionality)**

> Why? [Read here](https://wagmi.sh/docs/prepare-hooks/intro)

### Prepared usage

```diff
import { prepareWriteContract, writeContract } from '@wagmi/core'

const tokenId = 69

+const config = await prepareWriteContract({
+ addressOrName: '0x...',
+ contractInterface: wagmiAbi,
+ functionName: 'mint',
+ args: [tokenId]
+})

const result = await writeContract({
- addressOrName: '0x...',
- contractInterface: wagmiAbi,
- functionName: 'mint',
- args: [tokenId],
+ ...config
})
```

### Dangerously unprepared usage

It is possible to use `writeContract` without preparing the configuration first by passing `mode: 'dangerouslyUnprepared'`.

```diff
import { writeContract } from '@wagmi/core'

const tokenId = 69

const result = await writeContract({
+ mode: 'dangerouslyUnprepared',
  addressOrName: '0x...',
  contractInterface: wagmiAbi,
  functionName: 'mint',
  args: [tokenId],
})
```
