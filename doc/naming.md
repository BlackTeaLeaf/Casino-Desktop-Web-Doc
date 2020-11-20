# 命名風格

## 實體檔案

專案中所有實體檔案皆使用 kebab case 風格命名，包含 script、圖片、文檔等等等

```bash
this-is-a-apple.ts
```

## creator

由於在 editor 觀看整個 scene 時，很難區分到底哪個 node 有實做功能，
故需要制定一個命名原則來規範，才不會浪費太多時間尋找 node，node 命名規範如下

| 命名風格      | 例子      | 使用範圍                                                                                                                    |
| ------------- | --------- | --------------------------------------------------------------------------------------------------------------------------- |
| constant-case | USER_INFO | 有掛載 [presenter](none.md#presenter) 腳本的 node，代表起到 scene 主要控制權的腳色                                          |
| pascal-case   | UserInfo  | "有特定功能、或者能影響其他 node" 的 node，類似於 [presenter](none.md#presenter)，但跟遊戲主邏輯無關，輔助控制 scene 的腳色 |
| kebab-case    | user-info | 其他只是作為素材的 node                                                                                                     |
