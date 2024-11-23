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

\_index.tsx

```
/
```

## redirect

redirect 関数を利用するとリダイレクトが行える

```
return redirect(`/contacts/${params.contactId}`);
```

## Link

Link を利用してページ移動をおこなう

```
import { Link } from "@remix-run/react";

<Link to={`contacts/${contact.id}`}>hoge</Link>
```

## NavLink

to と同じ url にいる場合 isActive が true になる Link

```
<NavLink to="/tasks">
  {({ isActive, isPending }) => (
    <span className={isActive ? "active" : ""}>Tasks</span>
  )}
</NavLink>
```

## useNavigation

searchParams を取得

```
const navigation = useNavigation();
// ?hoge=testのような形で出力される
console.log(navigation.location.search)
```

保留中のページ遷移の情報を取得する

状態を取得

```
const navigation = useNavigation();
className={
  navigation.state === "loading" ? "loading" : ""
}
```

次の遷移先を取得

何も起こっていない際は undefined になる

```
const navigation = useNavigation();
console.log(navigation.location);
```

## useNavigate

ブラウザを一つ前に戻す

```
const navigate = useNavigate();

<button onClick={() => navigate(-1)} type="button">
  Cancel
</button>
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

## useSubmit

Form の submit をコード上で実行するための hook
オプションの replace が ture の際は現在の履歴を置き換える
※履歴が荒れてしまうのを防いだりする

```
const submit = useSubmit();

<Form
  onChange={(event) => {
    const isFirstSearch = q === null;
    submit(event.currentTarget, {
      replace: !isFirstSearch,
    });
  }}
/>
```

## action

データを更新する際に使う関数、POST,DELETE,PUT,PATCH リクエストが送られたタイミングでサーバー側で実行される

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
