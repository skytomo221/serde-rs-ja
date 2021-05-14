<span style="float:right">
  [![GitHub]][repo]
  [![rustdoc]][docs]
  [![Latest Version]][crates.io]
</span>

[GitHub]: /img/github.svg
[repo]: https://github.com/serde-rs/serde
[rustdoc]: /img/rustdoc.svg
[docs]: https://docs.serde.rs/serde/
[Latest Version]: https://img.shields.io/crates/v/serde.svg?style=social
[crates.io]: https://crates.io/crates/serde

<div style="clear:both"></div>

# Serde

Serdeは、Rustデータ構造を効率的かつ一般的にシリアライズ（***ser***ializing）およびデシリアライズ（***de***serializing）するためのフレームワークです。

Serdeのエコシステムは、自分自身をシリアライズ/デシリアライズする方法を知っているデータ構造と、他のものをシリアライズ/デシリアライズする方法を知っているデータフォーマットで構成されています。
Serdeは、この2つのグループが相互に作用するためのレイヤーを提供し、サポートされているデータ構造を、サポートされているデータフォーマットを使用してシリアライズおよびデシリアライズできるようにします。

### デザイン

他の多くの言語では、データのシリアライズをランタイムリフレクションに頼っていますが、Serdeは代わりにRustの強力なトレイトシステムに基づいて構築されています。
自分自身をシリアライズ/デシリアライズする方法を知っているデータ構造は、Serdeの`Serialize`トレイトおよび`Deserialize`トレイトを実装している（または Serdeの`[#derive]`アトリビュートを使用してコンパイル時に実装を自動生成している）データ構造です。
これにより、リフレクションやランタイム型情報のオーバーヘッドを回避できます。
実際、多くの状況において、データ構造とデータフォーマットの間の相互作用は、Rustコンパイラによって完全に最適化され、Serdeシリアライズは、データ構造とデータフォーマットの特定の選択に対して、手書きのシリアライザと同じ速度で実行されます。

### データフォーマット

以下は、コミュニティによってSerdeに実装されたデータフォーマットの一部です。コミュニティによってSerdeに実装されたデータフォーマットの一部をご紹介します。

- [JSON]は、多くのHTTP APIで使用されているユビキタスなJavaScript Object Notationです。
- [Bincode]は、Servoレンダリングエンジン内のIPCに使用されるコンパクトなバイナリフォーマットです。
- [CBOR]は、小さなメッセージサイズのために設計されたConcise Binary Object Representation（簡潔なバイナリオブジェクト表現）です。
- [YAML]は、マークアップ言語ではない、人間に優しい設定言語と自称している言語です。
- [MessagePack]は、コンパクトなJSONに似た、効率的なバイナリフォーマットです。
- [TOML]は、[Cargo]が使用する最小限の設定フォーマットです。
- [Pickle]は、Pythonの世界では一般的なフォーマットです。
- [RON]は、Rusty Object Notationの略です。
- [BSON]は、MongoDBが使用するデータストレージおよびネットワーク転送フォーマットです。
- [Avro]は、Apache Hadoopで使用されているバイナリ形式で、スキーマ定義をサポートしています。
- [JSON5]は、JSONのスーパーセットで、ES5の生成規則（productions）も含まれています。
- [Postcard]は、no\_stdや組み込みシステムに適したコンパクトなバイナリフォーマットです。
- [URL]のクエリ文字列をx-www-form-urlencoded形式で表示します。
- [Envy]は、環境変数をRustの構造体にデシリアライズする方法です。*（デシリアライズのみ）*
- [Envy Store]は、[AWS Parameter Store]のパラメータをRustにデシリアライズするための構造体に変換します。*（デシリアライズのみ）*
- [S-expressions]は、Lisp言語ファミリーで使用されるコードとデータのテキスト表現です。
- [D-Bus]'s binary wire format.
- [FlexBuffers]は、GoogleのFlatBuffers zero-copy serialization formatのスキーマレスの従兄弟です。
- [Bencode]は、BitTorrentプロトコルで使用されるシンプルなバイナリフォーマットです。
- [DynamoDB Items]は、[rusoto_dynamodb]がDynamoDBとの間でデータを転送する際に使用するフォーマットです。
- [Hjson]は、人間が読んだり編集したりすることを前提に設計されたJSONの拡張構文です。*（デシリアライズのみ）*

[JSON]: https://github.com/serde-rs/json
[Bincode]: https://github.com/servo/bincode
[CBOR]: https://github.com/pyfisch/cbor
[YAML]: https://github.com/dtolnay/serde-yaml
[MessagePack]: https://github.com/3Hren/msgpack-rust
[TOML]: https://github.com/alexcrichton/toml-rs
[Pickle]: https://github.com/birkenfeld/serde-pickle
[RON]: https://github.com/ron-rs/ron
[BSON]: https://github.com/zonyitoo/bson-rs
[Avro]: https://github.com/flavray/avro-rs
[JSON5]: https://github.com/callum-oakley/json5-rs
[URL]: https://docs.rs/serde_qs
[Postcard]: https://github.com/jamesmunns/postcard
[Envy]: https://github.com/softprops/envy
[Envy Store]: https://github.com/softprops/envy-store
[Cargo]: http://doc.crates.io/manifest.html
[AWS Parameter Store]: https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-paramstore.html
[S-expressions]: https://github.com/rotty/lexpr-rs
[D-Bus]: https://docs.rs/zvariant
[FlexBuffers]: https://github.com/google/flatbuffers/tree/master/rust/flexbuffers
[Bencode]: https://github.com/P3KI/bendy
[DynamoDB Items]: https://docs.rs/serde_dynamo
[rusoto_dynamodb]: https://docs.rs/rusoto_dynamodb
[Hjson]: https://github.com/Canop/deser-hjson

### データ構造

Serdeはすぐに、Rustの一般的なデータ型を上記のいずれかの形式でシリアライズ/デシリアライズすることができます。
例えば、`String`,`&str`,`usize`,`Vec<T>`,`HashMap<K,V>`などがサポートされています。
さらに、Serdeは構造体のシリアライズ実装を自分のプログラムで生成するためのderiveマクロを提供しています。
deriveマクロの使い方は次のようになります。

!PLAYGROUND 72755f28f99afc95e01d63174b28c1f5
```rust
use serde::{Serialize, Deserialize};

#[derive(Serialize, Deserialize, Debug)]
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let point = Point { x: 1, y: 2 };

    // PointをJSON文字列に変換します。
    let serialized = serde_json::to_string(&point).unwrap();

    // serialized = {"x":1,"y":2} と表示
    println!("serialized = {}", serialized);

    // JSON文字列をPointに戻します。
    let deserialized: Point = serde_json::from_str(&serialized).unwrap();

    // deserialized = Point { x: 1, y: 2 } と表示
    println!("deserialized = {:?}", deserialized);
}
```
