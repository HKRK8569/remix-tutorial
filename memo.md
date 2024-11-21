# remixMemo

## routes

routes ディレクトリにファイル追加でルーティングを行える
<Outlet />の部分が url に応じたコンポーネントが呼び出される
contacts.$contactId.tsx

```
/contacts/${contactId}
```

contacts.$contactId\_.edit.tsx

```
/contacts/${alex-anderson}/edit
```

## Link

Link を利用してページ移動をおこなう

```
import { Link } from "@remix-run/react";

<Link to={`contacts/${contact.id}`}>hoge</Link>
```

## useLoaderData

loader 関数の結果をコンポーネントで取得するための Hook

```

export const loader = async () => {
  const contacts = await getContacts();
  return json({ contacts });
};

const { contact } = useLoaderData<typeof loader>();
```
