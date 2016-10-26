# RSpec を書いてみる

まずは最小限の RSpec の構成を作ってみましょう。

## 作業ディレクトリ `rspec-sample` を作成する

ついでにテストコードを配置する `spec` ディレクトリも作っておきます。

```bash
$ mkdir -p path-to-path/rspec-sample/spec
$ cd path-to-path/rspec-sample
```

## Rakefile を作成する

RSpec は `rake` コマンドを用いて実行するため、Rakefile という rake コマンド用のタスク定義ファイルを作成します。

```Rakefile
require "rspec/core/rake_task"

RSpec::Core::RakeTask.new("spec")
task :default => :spec
```

## spec_helper.rb を作成する

以下の内容で `spec_helper.rb` ファイルを作成します。
ここにはテスト共通の設定、実装を記述します。

ちなみに `spec` ディレクトリ、および `spec_helper.rb` ファイルは RSpec のお約束です。

```spec/spec_helper.rb
require 'rspec'

RSpec.configure do |config|
end
```

## テストコードを作成する

動作確認のため、以下の内容でテストコードを作成します。
ファイル名には必ず `_spec` を含める、`spec_helper` を `require` するのも RSpec のお約束です。

```spec/app_spec.rb
require 'spec_helper'

describe 'app_spec' do
  it {
    expect(1).to eq(1)
  }
end
```

## RSpec を実行する

`rake spec` コマンドを実行します。
`1 example, 0 failures` と表示されれば成功です。

```bash
$ rake spec
.

Finished in 0.00244 seconds (files took 0.27435 seconds to load)
1 example, 0 failures
```

## Padrino で RSpec を書く

実際のテストコードでは、DB に接続したり依存ライブラリを読みこんだりする必要があります。
まちいろで採用しているフレームワーク Padrino では、その辺りの処理が事前に行われた状態で実行されるため、
基本的には上記の通り `spec` にテストコードを配置していくだけでテストが実行可能です。
