# マッチャ

※ マッチャ (Matcher) とは、期待値と実際の値を比較して一致しているかどうかを返すオブジェクトのことです

## 基本構文

`expect(...).to {matcher}`  という流れで記述します。
否定の場合は `not_to` を使用します。

```ruby
it {
  user = ...
  expect(user.name).to eq('yamada')
}
```

## 様々なマッチャ

```ruby
# 完全一致
expect(...).to eq(...)

# false かどうか
expect(...).to be_falsey

# true かどうか
expect(...).to be_truthy

# 配列が空かどうか
expect(...).to be_empty

# 配列に指定値が含まれているかどうか
expect(...).to include 1

# 例外が発生するかどうか
expect(...).to raise_error XXXError
```
