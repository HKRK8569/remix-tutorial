# remixMemo

## routes

routes ディレクトリにファイル追加でルーティングを行える

例:contacts.$contactId.tsx

```
/contacts/${contactId}
```

## Link

Link を利用してページ移動をおこなう

```
import { Link } from "@remix-run/react";

<Link to={`contacts/${contact.id}`}>hoge</Link>
```
