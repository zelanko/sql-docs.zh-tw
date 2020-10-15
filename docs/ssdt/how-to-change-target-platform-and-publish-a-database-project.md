---
title: 變更目標平台及發佈資料庫專案
description: 了解如何將 SQL Server Data Tools 資料庫專案其平台變更為支援的 SQL Server 執行個體。 了解如何發佈資料庫專案。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- sql.data.tools.publish.dialog
- sql.data.tools.publishdacproject
ms.assetid: 6012e120-5f72-4f4f-ae6e-f9a57ae1dea7
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: c5ee0b9febeec7da287e26a40adcb6910b80991d
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987214"
---
# <a name="how-to-change-target-platform-and-publish-a-database-project"></a>如何：變更目標平台及發佈資料庫專案

您可以將您的 SQL Server Data Tools (SSDT) 資料庫專案的目標 SQL Server 版本變更為任何支援之 SQL Server (SQL Server 2005、2008、2008 R2、Microsoft SQL Server 2012 或 SQL Azure) 的執行個體。 如此一來，您就可以將資料庫開發工作集中於一個專案，但視需要再將它發行到多個 SQL Server 執行個體。  
  
SSDT 透過對目標平台的認知以及自動偵測程式碼中的任何錯誤 (例如為即將發行到 SQL Azure 的專案使用未支援的功能)，也讓這項工作變得簡單一些。  
  
> [!WARNING]  
> 下列程序利用先前在[連接的資料庫開發](../ssdt/connected-database-development.md)和[專案導向的離線資料庫開發](../ssdt/project-oriented-offline-database-development.md)小節中的程序所建立的實體。  
  
### <a name="to-change-a-projects-target-platform"></a>變更專案的目標平台  
  
1.  以滑鼠右鍵按一下 [方案總管] 中的專案，再選取 [屬性]。 按一下左邊的 [專案設定]  索引標籤存取 [專案設定]  屬性頁。  
  
2.  此頁面的 [目標平台]  下拉式清單包含可以將資料庫專案發行到其中的所有支援 SQL Server 平台。 請為這個程序選取 [SQL Azure] 。  
  
### <a name="to-use-platform-validation-when-editing-scripts"></a>若要在編輯指令碼時使用平台驗證  
  
1.  以滑鼠右鍵按一下 [方案總管] 中的 [Products] 資料表，再選取 [檢視程式碼] 將它在 Transact\-SQL 編輯器中開啟。  
  
2.  將 `ON [PRIMARY]` 附加到 `CREATE TABLE` 陳述式結尾。  
  
3.  請注意，下列錯誤顯示在 [錯誤清單]**** 窗格中：SQL70015: SQL Azure 不支援 '檔案群組參考和資料分割配置'。  
  
    SSDT 會自動根據目標平台來驗證指令碼。 在這種情況下，由於 SQL Azure 不支援檔案群組，SSDT 傳回錯誤。 如需在 SQL Azure 中不支援的 Transact\-SQL 陳述式清單，請參閱[部分支援的 Transact-SQL 陳述式 (Microsoft Azure SQL Database)](/previous-versions/azure/ee336267(v=azure.100))。  
  
4.  移除 `ON` 子句。 請注意，該錯誤隨即從 [錯誤清單] 中消失。  
  
### <a name="to-publish-a-database-project"></a>若要發行資料庫專案  
  
1.  如果您有 SQL Azure 執行個體的存取權，可以略過下一個步驟。 否則，以滑鼠右鍵按一下 [方案總管] 中的 [TradeDev] 專案，再選取 [屬性] 存取 [專案設定] 屬性頁。 使用 [目標平台] 下拉式清單選取要將專案發行到其中的 SQL Server 平台。  
  
2.  以滑鼠右鍵按一下 [方案總管] 中的 [TradeDev] 專案，再選取 [發行]。 SSDT 將開始建置專案。 如果沒有發生建置錯誤，[發行資料庫]  對話方塊隨即出現。  
  
3.  按一下 [發行資料庫]  對話方塊中的 [編輯]  編輯目標資料庫連接。  
  
4.  在 [連接屬性] 對話方塊中，輸入 SQL Server 執行個體名稱和您的認證進行驗證。 在 [連接到資料庫] 中輸入 **NewTrade**。 這會嘗試將資料庫專案發行到新的資料庫。 您也可以選擇要發行到現有的資料庫。 例如，如果選擇現有的 **TradeDev** 資料庫，則在離線 **TradeDev** 專案中對物件 (如指令碼) 所做的所有變更將傳播至即時 **TradeDev** 資料庫。  
  
    如果您有權限可以對要發行的資料庫進行任何變更，請按 [發行]  按鈕。 不過，如果您沒有生產資料庫的寫入權限，可以按一下 [產生指令碼]**** 按鈕產生稍後可以遞交給 DBA 的 Transact\-SQL 發行指令碼。 DBA 就可以執行該指令碼來更新實際執行伺服器，使其結構描述與資料庫專案同步。  
  
5.  [資料工具作業]   視窗會顯示發行作業的進度，並在發生任何錯誤時通知您。 在這個新的視窗中，您還可以視需要選擇檢視部署預覽、產生的指令碼或完整的發行結果。  
  
6.  您還可以將發行設定儲存在設定檔中，讓日後的發行作業可以重複使用相同的設定。 若要如此，請按一下 [發行資料庫]  對話方塊中的 [另存設定檔]  按鈕。 以後您想要重新載入現有的設定時，就可以按一下 [載入設定檔]  按鈕。  
  
7.  請留意 [資料工具作業]  視窗中的訊息。 按一下 [正在建立發行預覽...] 右邊的 [檢視預覽] 連結右邊的 [檢視預覽] 連結。這將會開啟部署預覽報表。 如果專案的目標平台與專案發行的目標資料庫伺服器不同，SSDT 會在此報表中發出警告。  例如，如果專案的目標平台為 Microsoft SQL Server 2012，而您嘗試將專案發行至 SQL Server 2008 R2 伺服器執行個體，則會在 [輸出] 視窗中看到下列警告：  
  
**指定目標平台為 Microsoft SQL Server 2012 的專案可能會與 SQL Server 2008 產生相容性問題**    如果這類專案包含 Microsoft SQL Server 2012 中引入的實體 (例如序列物件)，則發行作業將會失敗。  
  
如果物件述詞在新建立的全文檢索索引上使用 **CONTAINS** 或 **FREETEXT**，且使用了異動指令碼，則部署將會失敗。 如果在部署期間啟用了 [包括異動指令碼] 的選項，則程序和檢視表會定義在交易內部，而全文檢索索引會定義在交易外部 (位於部署指令碼的結尾)。 由於指令碼的這種排序次序，所以系統將無法根據全文檢索索引解析使用 CONTAINS 或 FREETEXT 的程序或檢視表，因而產生部署錯誤。  
