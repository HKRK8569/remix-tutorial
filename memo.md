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

## action

データを更新する際に使う関数、POST,DELETE,PUT,PATCH リクエストが送られたタイミングで実行される

```
export const action = async ({ params, request }: ActionFunctionArgs) => {
  invariant(params.contactId, "Missing contactId param");
  const formData = await request.formData();
  const updates = Object.fromEntries(formData);
  await updateContact(params.contactId, updates);
  return redirect(`/contacts/${params.contactId}`);
};

<Form key={contact.id} id="contact-form" method="post">
    <button type="submit">Save</button>
</Form>
```
