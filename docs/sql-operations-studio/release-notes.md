---
title: Microsoft SQL Operations Studio （預覽） 版本資訊 |Microsoft 文件
description: Microsoft SQL Operations Studio （預覽） 版本資訊
ms.custom: tools|sos
ms.date: 03/28/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba86403e791af25de4f7bcd8b1cbd7b5f188897b
ms.sourcegitcommit: d6881107b51e1afe09c2d8b88b98d075589377de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="sql-operations-studio-preview-release-notes"></a>SQL Operations Studio （預覽） 版本資訊

**[下載年 3 月公開預覽](download.md)**

## <a name="march-2018-march-public-preview"></a>年 3 月 2018 （年 3 月公開預覽）

發行日期： 2018 年 3 月 28，  
version: 0.27.3

*年 3 月公用預覽*繼續處理最上層的 GitHub 問題而重點在於提升擴充性故事。 特別啟用擴充功能管理員，改善儀表板管理，並提供 SQL 代理程式和 insights 擴充功能。 此版本包含下列增強功能：

- 增強的支援索引標籤式的深入資訊和組態窗格的儀表板擴充性模型。
   - 擴充管理員可讓簡單擷取的延伸模組。
   - 儀表板延伸從 sp_whoisactive [whoisactive.com](http://www.whoisactive.com)。
   - 如需詳細資訊，請參閱[擴充功能的 SQL 作業 Studio](extensions.md)。
- 請加入更多[連線和物件總管 中的擴充性 Api](https://github.com/Microsoft/sqlopsstudio/wiki/Extensibility-API)管理。
- 若要修正重要影響的客戶繼續[GitHub 問題](https://github.com/Microsoft/sqlopsstudio/issues)。

如需詳細資訊，請參閱[變更記錄](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md)。


## <a name="february-2018-february-public-preview"></a>2018 年 2 月版 （ 2 月公開預覽）

發行日期： 2018 年 2 月 15，  
版本： 0.26.7

*年 2 月公用預覽*含有一些功能建議和高優先順序的 bug 修正。 此版本包含下列增強功能：

- 簡介安裝自動更新，這樣會提供通知可用於下載新版本時 
- 連接對話方塊 'Database' 欄位現在是以動態方式填入的下拉式清單將包含從指定的伺服器填入資料庫清單。
- 修正[發出 6](https://github.com/Microsoft/sqlopsstudio/issues/6)： 使連接與選取的資料庫開啟新查詢索引標籤。
- 修正[發出 22](https://github.com/Microsoft/sqlopsstudio/issues/22): ' Server Name' 和資料庫名稱-可以這些是下拉式清單而不是文字方塊？
- 修正[發出 549](https://github.com/Microsoft/sqlopsstudio/issues/549)： 無訊息/非常無訊息安裝會導致在安裝之後開啟應用程式。
- 修正[發出 481](https://github.com/Microsoft/sqlopsstudio/issues/481)： 加入 「 檢查更新 」 選項。
- SQL 編輯器顏色標示和自動完成修正：
   - 修正[發出 584](https://github.com/Microsoft/sqlopsstudio/issues/584): 「 完整 」 不反白顯示的 intellisense 的關鍵字。
   - 修正[發出 345](https://github.com/Microsoft/sqlopsstudio/issues/345)： 以色彩標示 SQL 函式，在編輯器中的。
   - 修正[發出 300](https://github.com/Microsoft/sqlopsstudio/issues/300): [#tempData] 最新"]"將會顯示綠色。
   - 修正[發出 225](https://github.com/Microsoft/sqlopsstudio/issues/225)： 關鍵字色彩不相符。
   - 修正[發出 60](https://github.com/Microsoft/sqlopsstudio/issues/60)： 無效的 sql 語法色彩反白顯示時使用 from 子句中的暫存資料表。
- 導入連線擴充性 API。
- VS Code 編輯器 1.19 整合。
- 更新拾取幾項查詢計劃檢視器改良 JustinPealing/html-查詢計劃元件。


## <a name="january-2018-january-public-preview"></a>2018 年 1 月 （ 1 月公開預覽）

發行日期： 2018 年 1 月 17 日，  
版本： 0.25.4

*1 月公用預覽*含有一些功能建議和高優先順序的 bug 修正。 此版本包含下列增強功能：

- 在 [連接] 對話方塊中可使用儲存的伺服器連接。
- 啟用熱結束。 根據預設，若要啟用，請參閱熱結束已關閉[熱結束設定](settings.md#hot-exit)。
- 索引標籤著色依據伺服器群組。 根據預設，若要啟用，請參閱已關閉的索引標籤著色[索引標籤的色彩設定](settings.md#tab-color)。
- 變更*伺服器名稱*至*伺服器*連接對話方塊中。
- 修正中斷*執行目前查詢*命令。
- 修正 bug 的指令碼的拖放中斷。
- 修正不正確的 [開始] 功能表釘選的圖示。
- 修正遺失商標圖示的 Azure 帳戶。


## <a name="december-2017-december-public-preview"></a>2017 年 12 月（12 月公開預覽）

發行日期： 2017 年 12 月 19，  
版本： 0.24.1

*年 12 月公用預覽*跨所有功能區域，以及下列增強功能包括數個 bug 修正：

- 建立防火牆規則 對話方塊現在是可以協助您連接到 Azure SQL Database 和 Azure SQL 資料倉儲。
- 加入的 Windows 安裝程式，以及 Linux DEB 和 RPM 安裝封裝。
- 管理儀表板視覺化配置編輯器。
- *指令碼做為 Alter*和*指令碼做為執行*命令。
- *執行目前查詢的實際計畫*命令。
- 整合 VS Code 1.18.1 編輯器平台。
- 啟用側載的 VSIX 擴充功能檔案。
- 支援"GO N"批次反覆運算語法。


## <a name="november-2017"></a>2017 年 11 月

發行日期： 2017 年 11 月 15 日，  
版本： 0.23.6

- 初始版本的[!INCLUDE[name-sos](../includes/name-sos-short.md)]。


## <a name="next-steps"></a>後續步驟

請參閱下列快速入門，若要開始使用其中一項：
- [連接及查詢 SQL Server](quickstart-sql-server.md)
- [連接及查詢 Azure SQL Database](quickstart-sql-database.md)
- [連接及查詢 Azure 資料倉儲](quickstart-sql-dw.md)

參與[!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio)
