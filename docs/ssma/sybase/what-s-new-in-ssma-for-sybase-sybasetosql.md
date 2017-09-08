---
title: "什麼 &#39; s SSMA for Sybase (SybaseToSQL) 的新功能 |Microsoft 文件"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
caps.latest.revision: 21
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 80642503480add90fc75573338760ab86139694c
ms.openlocfilehash: 1054c9279039eda01320e1afd9745b6a53200b3f
ms.contentlocale: zh-tw
ms.lasthandoff: 08/21/2017

---
# <a name="what39s-new-in-ssma--for-sybase-sybasetosql"></a>什麼 &#39; s SSMA for Sybase (SybaseToSQL) 的新功能
本主題列出 SSMA for Sybase 變更每個版本中。 

## <a name="ssma-v74"></a>SSMA v7.4
V7.4 版的 SSMA for Sybase 包含下列變更：
- **查詢逾時**選項現在時仍可使用在來源和目標結構描述物件探索。
![查詢逾時選項](../media/query-timeout_red.png)
- 品質和轉換的度量，而改善了目標的修正程式，根據客戶的意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.4 的必要條件。 此外，開頭 v7.4，32 位元版本的 SSMA 會停止。  

## <a name="ssma-v73"></a>SSMA v7.3
V7.3 版的 SSMA for Sybase 包含下列變更：
- 改善的品質和轉換的度量根據客戶的意見反應目標的修正程式。
- 透過下列項目公開 SSMA 擴充性架構：
  - 匯出至 SQL Server Data Tools (SSDT) 專案的功能。
    -   您現在可以在 SSDT 專案，從 SSMA 匯出結構描述指令碼。 您可以使用結構描述指令碼來進行額外的結構描述變更及部署您的資料庫。
![將儲存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  - 可供 SSMA 執行自訂轉換執行的程式庫。
    - 您現在可以建構自訂語法轉換和 SSMA 先前未處理的轉換可以處理的程式碼。
      - 這個部落格文章，指示如何建構自訂轉換子可用[擴充 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      - 轉換的範例專案可以是下載此[部落格文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。

## <a name="ssma-v72"></a>SSMA v7.2
V7.2 版的 SSMA for Sybase 包含下列變更：
- 改善的品質和轉換的度量根據客戶的意見反應目標的修正程式。
- 遙測增強功能提供更好的資料點，來解決客戶問題，並改善 SSMA 的轉換比率。

## <a name="ssma-v71"></a>SSMA 7.1 版
SSMA for Access 的 7.1 版發行版本包含下列變更：
- 在 Windows 和 Linux CTP1 上的 SQL Server 2017 已移轉的支援的目標平台。 這項功能是 technical preview 中，並支援結構描述和資料移動到目標 SQL 伺服器。
- SSMA 現在支援自動更新，以下載最新版本的 SSMA，如有的話。
- SSMA 可安裝二進位檔現在都是透過 Windows installer 封裝檔案 (.msi) 提供。

**資源**

[擴充 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[評估並將資料從非 Microsoft 資料平台移轉到 SQL Server *（與 Oracle 範例）*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 年  
2016 年版的 SSMA for Sybase 包含下列變更：  

-  已新增的支援 SQL Server 2016。
-  移除安裝程式檢查適用於.Net 2.0。
-  更新擴充功能組件相依性從.Net 3.5.net 4.0。
-  修正 儲存專案 」 以及 「 開啟專案 」 SSMA 主控台命令。
-  SSMA 主控台的固定"securepassword"命令。
-  已修正的初始載入的物件計數。
-  通用設定 中修正的 bug。

## <a name="march-2016"></a>2016 年 3 月  
2016 年 3 月 preview 版的 SSMA for Sybase 包含下列變更：  
  
-  移轉至 SQL Server 2016 所加入的支援。  
  
## <a name="january-2016"></a>2016 年 1 月  
2016 年 1 月維護版的 SSMA for Sybase 包含下列變更：  
  
-  加入的檢視要 SSMA (建議 RFC 5706203) 的記錄檔 功能表項目。  
-  加入的遙測。 
  
## <a name="july-2014"></a>2014 年 7 月  
2014 年 7 月版的 SSMA for Sybase 包含下列變更：  
  
-  改善的 Azure SQL DB 程式碼轉換。  
-  會移至架構以支援 Azure SQL DB 延伸模組組件功能。  
-  新增的效能改進測試包含超過 10k 之資料庫的物件。  
-  已加入的 UI 增強功能來處理大量的物件。  
-  加入 （因此可在轉換中予以忽略），反白顯示 「 已知 」 的 LOB 結構描述的能力。  
-  加入轉換速度的改進。  
-  加入要在 UI 中顯示物件計數的能力。 
-  減少的報表的大小超過 25%。  
-  未剖析建構的改良的錯誤訊息。  
  
## <a name="april-2014"></a>2014 年 4 月  
2014 年 4 月版的 SSMA for Sybase 包含下列變更：  
  
-   已新增的支援 MS SQL Server 2014。  
-   關於 Azure 的轉換已經修正的 bug。  
-   關於不可見的報表頁面在 IE 10 中已修正的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
2012 年 1 月版的 SSMA for Sybase 包含下列變更：  
  
-   已新增的支援回復觸發程序轉換。  
-   轉換提供修正@ROWCOUNT和 @@ERROR相同的 SET 陳述式。  
  
## <a name="july-2011"></a>2011 年 7 月  
2011 年 7 月版的 SSMA for Sybase 包含下列變更：  
  
-   在資料遷移期間報告改良的錯誤。  
  
## <a name="april-2011"></a>2011 年 4 月  
2011 年 4 月版的 SSMA for Sybase 包含下列變更：  
  
-   彙總支援的"SSMA for Sybase"產品[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005 年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"和 Azure SQL。  
-   加入連接及移轉至支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
-   加入轉換，並將 Sybase 資料庫移轉到 Azure SQL 的新功能。  
-   增強型的用戶端資料移轉引擎，支援平行的資料移轉。  
-   提升的資料移轉效能簡單與大量記錄復原模式。  
-   加入正確的轉換與區分大小寫的 Sybase 資料庫移轉到區分大小寫的 SQL Server 的能力。  
-   已新增的支援的 SQL Server ANSI 聯結陳述式 Sybase ASE 非 ANSI 聯結陳述式的轉換已經擴充成刪除及 UPDATE 陳述式。  
-   提供其他連接選項連接到 Sybase ASE 伺服器使用 Sybase ASE ODBC 提供者和 Sybase ASE ADO.Net 提供者。  
-   移除的相依性不同的資料庫稱為**SysDB**，其中包含 Sybase 模擬函式 （做為延伸模組組件的一部分安裝）。  
-   加上，安裝 SSMA for Sybase 延伸模組組件的功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]叢集。  
-   加入較早版本的 SSMA （v4.0 和 4.2 版） 所建立之專案的回溯相容性。  
-   加入與舊版本的 SSMA （v4.0 和 4.2 版） 安裝的 SSMA for Sybase v5.0 產品的並存 (SxS) 的能力。  
  
## <a name="july-2010"></a>2010 年 7 月  
2010 年 7 月版的 SSMA for Sybase 包含下列變更：  
  
-   已新增的支援移轉至 SQL Server 2008 R2。  
-   加入新的 SSMA 主控台應用程式的命令列執行。  
-   已加入的伺服器端和用戶端資料移轉引擎所使用的資料移轉的支援。  
-   新增 「 自訂選取 」 中的資料移轉的陳述式的支援。  
-   加入從 Sybase ASE 15.0.3 和 15.5 移轉的支援。  
  
## <a name="june-2008"></a>2008 年 6 月  
2008 年 6 月版的 SSMA for Sybase 包含下列變更：  
  
-   加入的 SSMA Tester 中，這會自動測試轉換資料庫物件和所做的 SSMA 資料移轉。 所有 SSMA 的移轉步驟都完成之後，請確認已轉換的物件運作的方式相同，而且已正確地傳送的所有資料使用 SSMA 軟體測試人員。  
-   加入的每個 SQL 轉換。 使用者現在可以指定暫存資料表 （和其他物件） 來轉換中每個來源程序的宣告。  
-   已加入的物件轉換中的增強功能：  
    -   聯結修訂的轉換。  
    -   彙總和非彙總而不需/群組 by 子句。  
    -   IDENTITY 函式使用 SELECT INTO 陳述式。  
    -   叢集條件約束和索引上的資料僅鎖定。  
    -   SELECT INTO 所建立的暫存資料表。  
    -   條件約束 / 索引的暫存資料表。  
    -   新[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年日期時間類型支援。  
    -   Sybase 15.0 連線和資料類型的支援。  
  
## <a name="may-2007"></a>May 2007  
May 2007 版的 SSMA for Sybase 包含下列變更：  
  
-   加入要儲存專案時更快載入資料庫內容的能力。  
-   已新增的支援的 SQL Server 中的使用者輸入註解格式 SQL 模式。  
-   已加入的物件轉換中的增強功能。  
  
此版本未更新的說明檔。 如需詳細資訊，請參閱本主題稍後的文件集注意事項 > 一節。  
  
## <a name="november-2006"></a>2006 年 11 月  
2006 年 11 月版的 SSMA for Sybase 包含下列變更：  
  
-   加入新的通用設定：  
    -   您可以選擇在編輯器視窗中顯示行號。  
    -   您可以設定 SSMA 提示來取代重複的物件，或一律或永遠不會取代重複的物件結構描述轉換期間。  
-   加入新的轉換選項可讓您設定 SSMA 如何處理在下列情況：  
    -   CAST 或 CONVERT 陳述式，其中包含二進位字串。  
    -   檢查相等運算式中的 null 值。  
    -   Proxy 的資料表。  
    -   使用者訊息 RAISERROR 的錯誤號碼。  
    -   包含無法解析識別項的 UPDATE 陳述式。  
-   加入新的移轉選項，可讓您指定 SSMA 應該如何處理外的日期[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]日期範圍。  
-   加入**格式化 SQL**上設定**SQL**索引標籤上，將格式化的程式碼，以改善可讀性。  
-   Bug 修正，包括：  
    -   SSMA 現在將轉換鎖定資料表*資料表*IN {共用 |TABLOCK 或 TABLOCKX 提示加入後續的 SELECT 查詢，在資料表上的獨佔} 模式陳述式。  
    -   在字元運算式中使用二進位類型時，現在會加入必要的轉型。  
    -   記憶體和效能增強功能。  
  
## <a name="july-2006"></a>2006 年 7 月  
2006 年 7 月版的 SSMA for Sybase 是最早的版本。  
  
## <a name="see-also"></a>另請參閱  
[開始使用 SSMA for Sybase &#40;SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
