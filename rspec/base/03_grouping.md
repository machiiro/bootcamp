# テストコードのグルーピング

## describe

テストをグルーピングして宣言します。

```ruby
describe 'User' do
  it {
    expect(1).to eq(1)
  }
end
```

## it/example

テスト単位を it/example で宣言します。
どちらを使用しても問題ありませんが、日本語を用いる場合は `example` を使う、という主張があるようです。

```ruby
it 'If the user ID, password is correct, the login is successful' do
end

example 'ユーザーID、パスワードが正しい場合はログインが成功する' do
end
```

## context

条件別のテストを記述する場合、`context` を使用することが推奨されます。

```ruby
describe 'ログイン' do
  context 'ユーザIDが間違っている' do
    it {
    }
  end

  context 'パスワードが間違っている' do
    it {
    }
  end

  context 'ログインID、パスワードが間違っている' do
    it {
    }
  end
end
```

## before/after

`describe` や `context` の前処理・後処理を実装する場合、`before`、`after` を使用します。

```ruby
describe 'ログイン' do
  before :each do
  end

  after :each do
  end
end
```
