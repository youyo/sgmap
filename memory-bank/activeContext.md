# アクティブコンテキスト: sgmap

## 現在の作業の焦点

現在、sgmap の基本的な機能実装が完了し、ライブラリとしての利用も可能になりました。以下の機能が実装されています：

- VPC ID を指定してセキュリティグループの接続関係を取得する機能
- セキュリティグループ ID でフィルタリングする機能
- mermaid 記法でのフローチャート出力機能
- JSON 形式での出力機能
- CLI インターフェースの実装
- ライブラリとしての利用機能（公開 API の提供）

## 最近の変更

- プロジェクトの基本構造を作成
- コア機能モジュール（core.py）の実装
- CLI インターフェース（cli.py）の実装
- パッケージ設定ファイル（setup.py）の作成
- README の作成
- memory-bank の初期化
- ライブラリとしての利用を可能にするために `__init__.py` を更新
- README にライブラリとしての使用方法を追加
- バージョニングに関する説明を明確化（タグのバージョンがそのまま PyPI のバージョンになることを明記）
- `pyproject.toml`の設定を修正し、タグのバージョンがそのまま PyPI のバージョンになるように設定（`version_scheme = "release-branch-semver"`、`local_scheme = "no-local"`に変更）
- mermaid 図で inbound と outbound の線の色を区別するように修正（inbound は薄いグレー#aaaaaa、outbound は濃いグレー#777777）
- mermaid 図の色指定を linkStyle を使用した実装に修正し、エラーを解消

## 次のステップ

1. **テストの実装**: ユニットテストとインテグレーションテストを実装して、機能の正確性を確認する
2. **エラーハンドリングの強化**: より詳細なエラーメッセージと例外処理を追加する
3. **ドキュメントの拡充**: より詳細な使用例やトラブルシューティングガイドを追加する
4. **機能拡張の検討**:
   - 複数の VPC を一度に分析する機能
   - 出力形式の追加（SVG、PNG、DOT など）
   - フィルタリングオプションの追加（タグ、名前など）
   - AWS Organizations との統合（複数アカウントの分析）

## アクティブな決定事項と考慮事項

1. **出力形式**: 現在は mermaid 記法と JSON のみをサポートしていますが、ユーザーのニーズに応じて他の形式も検討する可能性があります。
2. **パフォーマンス**: 大規模な VPC や多数のセキュリティグループがある場合のパフォーマンスを最適化する必要があります。
3. **クロスアカウント分析**: 将来的に、複数の AWS アカウントにまたがるセキュリティグループの分析をサポートすることを検討しています。
4. **CI/CD**: 継続的インテグレーションと継続的デリバリーのパイプラインを設定して、品質を確保する必要があります。
5. **ユーザーフィードバック**: 初期バージョンをリリース後、ユーザーからのフィードバックを収集して機能改善に活かす予定です。
