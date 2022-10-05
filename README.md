# README

- 1. draft と open を切り替えたとき、ラベルを付け替える CI を実装
- 2. プルリクをマージした時、付与されている wip と review のラベルを削除する

## キャプチャ

https://user-images.githubusercontent.com/64491435/193756945-289e113c-e188-4813-a150-c2ca5a8757e5.mov

## 作成手順

- [x] ラベルを 2 つ作成する
- [x] 以下のファイルを`.github/workflows/＊`に配置

### draft の場合

- [add_wip_label.yml](https://github.com/fumi238000/github-add-label-ci/blob/master/.github/workflows/add_wip_label.yml)


### open の場合

- [add_review_label.yml](https://github.com/fumi238000/github-add-label-ci/blob/master/.github/workflows/add_review_label.yml)


- [x] プルリクを作成し、open ⇄ draft を切り替えるときにラベルの付け替えができるか確認する
- [テスト用プルリク](https://github.com/fumi238000/github-test/pull/1)

## 参考資料

- https://zenn.dev/sh090/articles/8291abdb1be48f5765ec

## 補足

- draft の機能が Private だと使えない・・・。
