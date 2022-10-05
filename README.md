# README

- 1. draft と open を切り替えたとき、ラベルを付け替える CI を実装
- 2. プルリクをマージした時、付与されている wip と review のラベルを削除する
- 3. issue を close した時、その issue に付与されている優先度に関するラベルを削除する

## キャプチャ

https://user-images.githubusercontent.com/64491435/193756945-289e113c-e188-4813-a150-c2ca5a8757e5.mov

## 作成手順

- [x] ラベルを 2 つ作成する
- [x] 以下のファイルを`.github/workflows/＊`に配置

### draft の場合

- add_wip_label.yml

```yml
name: "Add WIP Label && Remove Review Label"

on:
  pull_request:
    types: [opened, converted_to_draft]
jobs:
  add_wip_label:
    if: github.event.pull_request.draft == true
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions-ecosystem/action-remove-labels@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          labels: |
            👀 needs review
      - uses: actions-ecosystem/action-add-labels@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          labels: |
            ⚠ wip
```

### open の場合

- add_review_label.yml

```yml
name: "Add Review Label && Remove WIP Label"

on:
  pull_request:
    types: [opened, ready_for_review]
jobs:
  add_review_label:
    if: github.event.pull_request.draft != true
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions-ecosystem/action-remove-labels@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          labels: |
            ⚠ wip
      - uses: actions-ecosystem/action-add-labels@v1
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          labels: |
            👀 needs review
```

- [x] プルリクを作成し、open ⇄ draft を切り替えるときにラベルの付け替えができるか確認する
- [テスト用プルリク](https://github.com/fumi238000/github-test/pull/1)

## 参考資料

- https://zenn.dev/sh090/articles/8291abdb1be48f5765ec

## 補足

- draft の機能が Private だと使えない・・・。
