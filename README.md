# GASをTypeScriptで書く方法をまとめるリポジトリ

## 環境構築の手順
①node.jsをインストール

②node.jsとパッケージマネージャーがインストールできたか確認
```
npm -v
node -v
```

③claspをインストール
`npm install -g @google/clasp`

④googleアカウントの認証を通す
`clasp login`

⑤プロジェクトディレクトリを作成
`mkdir gas_to_ts_practice`

⑥プロジェクトのセットアップ
```
cd gas_to_ts_practice
npm init -y
npm install typescript @types/google-apps-script --save-dev
clasp create --type standalone

```

⑦tsconfig.jsonを作成し、以下の内容を追加
```
{
  "compilerOptions": {
    "target": "ES5",
    "module": "commonjs",
    "outDir": "dist",
    "rootDir": "src",
    "strict": true,
    "skipLibCheck": true
  },
  "include": [
    "src/**/*.ts"
  ]
}
```

⑧appsscript.jsonの"timeZone"を "Asia/Tokyo"に修正

⑨package.jsonの"scripts"に下記を追加
`"build": "tsc && powershell Move-Item ./appsscript.json ./dist/"`

⑩.clasp.jsonの"rootDir"を"dist"に修正する

⑪ルートディレクトリにsrcフォルダを作成

⑫srcフォルダにtypescriptのソースコードを置く

⑬src内のtypescriptをgasに変換（新たに作成されたdistにgasのソースコードが配置される）
`npx tsc`

⑭appsscript.jsonをdistに移動する（移動しないとclasp pushできない）
`npm run build`

⑮gasのエディタにpush
`clasp push`

⑯gasのエディタを開く
`clasp open`
