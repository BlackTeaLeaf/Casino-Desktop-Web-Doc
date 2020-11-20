# Casino Desktop Web

遊戲 Casino 的 Cocos Creator 桌機 web 專案

* 版本需求為 Creator 2.4.3 版以上
* 編程語言以 typescript 為大宗，少量 javascript

該專案主要以 vscode 開發
所有主要、輔助功能都已 vscode 優先

## 專案結構

| 目錄     | 描述                              |
| -------- | --------------------------------- |
| .vscode  | vscode 專案設定，包含除錯模式設定 |
| assets   | 遊戲所有資源                      |
| doc      | 文檔                              |
| font     | 用來產生最小化字體的來源字體      |
| packages | cocos creator 插件                |
| settings | cocos creator 專案設定            |
| tool     | 專案工具                          |

| 檔案              | 描述                                                            |
| ----------------- | --------------------------------------------------------------- |
| deploy.json       | 發佈到線上平台的設定，只有基本位置訊息                          |
| cover-deploy.json | 發佈到線上平台的設定，包含私密資訊 (預設不存在，請跟負責人索取) |

### assets/scripts

| 目錄       | 描述                                                                                  |
| ---------- | ------------------------------------------------------------------------------------- |
| model      | 非視圖類的組件、功能。與 utils 不同的是，model 包含的是有兩個檔案以上、一個體系的功能 |
| presenters | 存放 [presenter](doc/noun.md#presenter) 的目錄                 |
| typing     | 全域的 typescript declaration file (d.ts)                                             |
| utils      | 非視圖類的小型功能件                                                                  |
| view-model | 通常嫁接於 casino-game-model ，處理視圖類的資料及功能提供給視圖                       |
| views      | creator 的通用型視圖類組件                                                            |

| 檔案             | 描述                                                                    |
| ---------------- | ----------------------------------------------------------------------- |
| creator-tools.ts | 提供在 preview、editor 階段，使用開發者工具存取遊戲引擎的一些程式小工具 |
| main.ts          | 整個遊戲的主要進入點，負責初始化主要遊戲邏輯                            |

該專案使用以下幾個 library 作為核心去延伸開發

| library           | 實做功能                          |
| ----------------- | --------------------------------- |
| I18next           | 多國語系                          |
| NodePlayer        | 現場直播播放器                    |
| FontCarrier       | 最小化字體產生器                  |
| casino-game-model | Casino 遊戲業務邏輯、資料的核心庫 |
| casino-login      | Casino 自動登入的代理伺服器       |

## package scripts

| 名稱               | 描述                                                                  |
| ------------------ | --------------------------------------------------------------------- |
| start:login-server | 啟動 casino-login ，讓本地運行的遊戲不需要 URL 參數，即可自動登入遊戲 |
| deploy             | 將 creator 生成的遊戲發行版 (/build/web-desktop) 同步到線上的存儲桶   |
| subfont            | 調用 tool/subfont/index.js 來生成遊戲用的最小化字體                   |

## 開發

[命名風格](doc/naming.md)
[編程設計](doc/program-design.md)
