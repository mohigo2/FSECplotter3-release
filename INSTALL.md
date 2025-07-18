# FSECplotter3 インストール手順

## 🚀 かんたんインストール (推奨)

### macOS用ネイティブアプリ

1. **DMGファイルをダウンロード**
   - `FSECplotter3_Installer.dmg` をダウンロード

2. **インストール**
   - DMGファイルをダブルクリックで開く
   - FSECplotter3.appをApplicationsフォルダにドラッグ&ドロップ

3. **起動**
   - LaunchpadまたはApplicationsフォルダからFSECplotter3を起動

### 初回起動時のセキュリティ設定

macOSの初回起動時に「開発元が未確認」の警告が表示される場合：

1. システム設定 → プライバシーとセキュリティ を開く
2. 「このまま開く」をクリック
3. または、右クリック → 開く で起動

## 📁 配布ファイル

- **FSECplotter3_Installer.dmg** (60MB) - インストール用ディスクイメージ
- **dist/FSECplotter3.app** (137MB) - アプリケーション本体

## ✨ 特徴

- **ゼロ設定**: Python環境構築不要
- **スタンドアロン**: 全ての依存関係を内包
- **ネイティブ統合**: macOSアプリケーションとして完全統合
- **ファイル関連付け**: .txtファイルの自動認識
- **Apple Silicon対応**: M1/M2 Macで最適化

## 🔧 開発者向け

### ソースコードからの実行

```bash
# 仮想環境の作成と依存関係インストール
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# アプリケーションの起動
python3 run_fsecplotter.py
```

### ビルド手順 (macOS)

#### 1. 環境準備
```bash
# 仮想環境の作成
python3 -m venv venv
source venv/bin/activate

# 依存関係のインストール
pip install -r requirements.txt
pip install pyinstaller
```

#### 2. アプリケーションビルド
```bash
# 軽量版アプリのビルド (137MB)
pyinstaller --clean FSECplotter3_lite.spec

# 結果: dist/FSECplotter3.app
```

#### 3. 配布用DMG作成
```bash
# インストーラー付きDMG作成
mkdir -p dmg_build
cp -R dist/FSECplotter3.app dmg_build/
ln -s /Applications dmg_build/Applications
hdiutil create -volname "FSECplotter3 Installer" -srcfolder dmg_build -ov -format UDZO FSECplotter3_Installer.dmg
rm -rf dmg_build
```

#### 4. ビルド仕様
- **バンドルID**: `com.fsecplotter.fsecplotter3`
- **アーキテクチャ**: Apple Silicon (ARM64) 対応
- **最小システム要件**: macOS 10.15 (Catalina) 以降
- **セキュリティ**: コードサイニング、entitlements設定済み

### 実施した改善内容

#### 依存関係の現代化
- matplotlib 1.5.0 → 3.7.0+ (セキュリティ修正、macOS互換性)
- numpy 1.10.1 → 1.24.0+ (Apple Siliconサポート)
- PyQt5 → 5.15.0+ (macOS Monterey以降対応)

#### macOS固有改善
- ドラッグ&ドロップのmacOSファイルURL処理改善
- クロスプラットフォームファイルパス処理
- Retina ディスプレイ対応

## 📋 システム要件

- **macOS**: 10.15 (Catalina) 以降
- **アーキテクチャ**: Apple Silicon (M1/M2) 推奨、Intel対応
- **ディスク容量**: 約200MB
- **メモリ**: 512MB以上推奨

## 🐛 トラブルシューティング

### アプリが起動しない
- macOSのセキュリティ設定を確認
- コンソール.app でエラーログを確認

### ファイルが開けない
- ファイル形式が島津(.txt)または日立(.rw?)形式か確認
- ファイルのアクセス権限を確認

## 📞 サポート

- **ライセンス**: GPLv2
- **プロジェクト**: FSECplotter3
- **バージョン**: 3.0.0