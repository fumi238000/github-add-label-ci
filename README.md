# README
- draft と open を切り替えたとき、ラベルを付け替えるCIをテスト

## 作成手順
- [ ] ラベルを2つ作成する
- [ ] 以下のファイルを`.github/workflows/add_review_label.yml`に配置

```yml
name: "Add Review Label"

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
- [ ] プルリクを作成し、open ⇄ draft を切り替えるときにラベルの付け替えができるか確認する

## 参考資料
- https://zenn.dev/sh090/articles/8291abdb1be48f5765ec

## 補足
- draftの機能がPrivateだと使えない・・・。
