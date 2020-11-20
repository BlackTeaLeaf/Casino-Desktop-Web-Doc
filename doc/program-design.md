# 編程設計

## creator

以下幾點是該專案在 creator 中的設計方向

* 發揮 creator IDE 所見即所得的優勢，盡可能的在 scene、prefab 裡將所有相關的元素全部直接放入，
  讓 scene 在 creator 中開啟時，就可以看到所有需要被使用到的 node (如果一開始就沒有顯示的東西，則加入 scene ，但 active = false)；
  盡可能不要透過動態加載 prefab 來導入遊戲元件，減少開發階段，需要在 creator 中尋找、查看 prefab 的次數

* 清單類的內容 node 採用這種放置模式

```txt
 XXXX_LIST                 (掛上 cc.ScrollView + presenters)
    └ content              (設為 cc.ScrollView.content)
        └ XXXX_ITEM
         (xxxx-item)
```

* 開發合作階段，**'製作、修改方'** 更改 node 時，最好將其 [function root node](./noun.md#fr-node) 設為 prefab 存放在 assets/prefabs 裡並分類，並在編輯 scene 完畢後，將修改結果存回 prefab，再將 git commit push 到自己的分支；

  **'管理、使用方'** 要合併別人的分支時，遇到 scene 衝突時，請優先保留自己版本的 scene ，只覆蓋 prefab，之後進入 creator 確認 prefab 的修改一切無誤時，再從自己版本的 scene 裡面 '回退' 到新的 prefab 上，用此方法更新 scene
  
> scene 通常結構複雜，牽一髮動全身，而在使用 git 版本管理時，scene 修改的 commit 通常無法直接合併使用 (因為 scene.fire 中 component id 是隨機的，直接合併會導致 id 衝突使 scene 破損)，所以要使用 prefab 作為合併手段

* 盡可能設計通用組件來完成遊戲中非 presenter 的功能，並保存在 assets/views

## script

* 請使用[這種](https://docs.cocos.com/creator/manual/zh/scripting/typescript.html?h=typescript#%E6%9B%B4%E5%A4%9A%E5%B1%9E%E6%80%A7%E7%B1%BB%E5%9E%8B%E5%A3%B0%E6%98%8E%E6%96%B9%E6%B3%95)方式獲取 node 參考，最好不要使用 node.getChildByName 或 cc.find 獲得的 node 參考，並藉此改變它們，除非有合理的理由
  
> 使用這種方式的弊端是:
>
> 1. 很難從 creator 中看出邏輯關係，需要 script 與 creator 對切著看
> 2. 改變 node 名子是很容易的，所以會更容易忘記要更改 script 對應的程式碼，因此容易滋生 bug
> 3. 取得 node 後大多數時間還需要 node.getComponent(MyComponent) ，不如 @property(MyComponent) 來的快

* 能使用 typescript 就不要使用 javascript
* 使用裝飾器 @property 的 property 請寫上明確的 type ，除非有預先賦值 ( null,undefined 例外 )
  
  ```typescript
    @ccclass('MyData')
    class MyData {}

    @ccclass()
    class MyComponent extends cc.Component {}

    @property(MyComponent)
    comp:MyComponent = null // 組件類只能賦值 null ，所以必須寫 type

    @property(MyData)
    data = new MyData() // 有預先賦值可不寫 type

    @property()
    label = '' // 有預先賦值可不寫 type

    @property()
    label:string = null // 賦值為 null 或 undefined 要寫 type
  ```
