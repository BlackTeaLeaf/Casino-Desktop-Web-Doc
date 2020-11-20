# 名詞

以下名詞用於縮短文件描述長度而定義
會用於所有文檔中

## presenter

存放於 presenters 裡面的 script ，與 casino-game-model 有進行互動的組件，資料與視圖的橋接腳色
類似於 '設計模式-MVP' 中的 P

## function root node {#fr-node}

所謂 'function root node' 是以 '一個組件、功能' 為單位的 'node 樹中的根'
例如：

```bash
BACCARAT_GAME_TABLE
    ├ ANNOUNCEMENT ( **function root node** )
    │   └ content
    │       └ label (修改此處)
    │
    └ TABLE_SELECTOR_LIST
        └ content
```

在 creator 中有掛載 [presenter](#presenter) 的 node 也是 function root node
