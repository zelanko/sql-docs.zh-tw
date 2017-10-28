---
title: "什麼 &#39; 新的 SSMA for Access(AccessToSQL) s |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 09/22/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
caps.latest.revision: 37
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 7595c51bf8cc0ec07a464a65c992c2f3a56b15c2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/30/2017

---
# <a name="what39s-new-in-ssma-for-access-accesstosql"></a>什麼 &#39; s SSMA for Access (AccessToSQL) 的新功能
本主題列出 SSMA 存取每個版本中的變更。  

## <a name="ssma-v76"></a>SSMA v7.6
SSMA for Access v7.6 發行已經增強，改善品質和轉換的度量資訊的目標修正程式與 SQL Server 2017 （公開預覽狀態） 的支援。 支援在 Windows 和 Linux 上的 SQL Server 2017 是公開預覽狀態，而且不應該用於實際執行移轉。

> [!IMPORTANT]
> SSMA v7.4 和更新版本，.Net 4.5.2 為安裝必要元件，而 32 位元版本的工具已停用。

## <a name="ssma-v75"></a>SSMA v7.5
SSMA for Access v7.5 發行已經增強，以確保行動不便人士更大的存取範圍的數個增強功能。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.5 的必要條件。 此外，開頭 v7.4，32 位元版本的 SSMA 會停止。

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for Access v7.4 版本包含下列變更：
- **查詢逾時**選項現在時仍可使用在來源和目標結構描述物件探索。
![查詢逾時選項](../media/query-timeout_red.png)

- 品質和轉換的度量，而改善了目標的修正程式，根據客戶的意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.4 的必要條件。 此外，開頭 v7.4，32 位元版本的 SSMA 會停止。

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for Access v7.3 版本包含下列變更：
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
SSMA for Access v7.2 版本包含下列變更：
- 改善的品質和轉換的度量根據客戶的意見反應目標的修正程式。
- 遙測增強功能提供更好的資料點，來解決客戶問題，並改善 SSMA 的轉換比率。

## <a name="ssma-v71"></a>SSMA 7.1 版
SSMA for Access 的 7.1 版發行版本包含下列變更：
- 在 Windows 和 Linux CTP1 上的 SQL Server 2017 已移轉的支援的目標平台。 這項功能是 technical preview 中，並支援結構描述和資料移動到目標 SQL 伺服器。
- SSMA 現在支援自動更新，以下載最新版本的 SSMA，如有的話。
- SSMA 可安裝二進位檔現在都是透過 Windows installer 封裝檔案 (.msi) 提供。

**資源**

[擴充 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)
  
## <a name="may-2016"></a>2016 年  
2016 年版本的 SSMA for Access 包含下列變更：  
  
-  加入的 SQL Server 2016 的官方支援
-  移除安裝程式檢查適用於.Net 2.0。
-  修正 儲存專案 」 以及 「 開啟專案 」 SSMA 主控台命令。
-  SSMA 主控台的固定"securepassword"命令。
-  已修正的初始載入的物件計數。
-  固定資料表資料載入 UI 索引標籤的存取。
-  通用設定 中修正的 bug。 
   
## <a name="march-2016"></a>2016 年 3 月  
2016 年 3 月預覽版本的 SSMA for Access 包含下列變更：  
  
-  移轉至 SQL Server 2016 所加入的支援。  
   
## <a name="january-2016"></a>2016 年 1 月  
SSMA for Access 的 2016 年 1 月維護版本包含下列變更：  
  
-  固定函式無效的預設值是 GUID 欄位 (RFC 3894811)。  
-  在匯入至 SQL Database (Azure) (RFC 4919573) 的記錄固定的停止回應。  
-  加入的檢視要 SSMA (建議 RFC 5706203) 的記錄檔 功能表項目。  
-  加入的遙測。  
  
## <a name="july-2014"></a>2014 年 7 月  
SSMA for Access 的 2014 年 7 月版本包含下列變更：  
  
-   改善的 Azure SQL DB 程式碼轉換。  
-   會移至架構以支援 Azure SQL DB 延伸模組組件功能。  
-   針對具有超過 10 萬個物件的資料庫已測試的效能改進。  
-   已加入的 UI 增強功能來處理大量的物件。  
-   已新增的支援的反白顯示 「 已知 」 的 LOB 結構描述 （因此可在轉換中予以忽略）。  
-   加入轉換速度的改進。
-   UI 中的計數加入顯示物件的支援。
-   減少的報表的大小超過 25%。
-   未剖析建構的改良的錯誤訊息。  
  
## <a name="april-2014"></a>2014 年 4 月  
SSMA for Access 的 2014 年 4 月版本包含下列變更：  
  
-   已新增的支援 MS SQL Server 2014。  
-   關於 Azure 的轉換已經修正的 bug。  
-   關於不可見的報表頁面在 IE 10 中已修正的 bug。  
  
## <a name="january-2012"></a>2012 年 1 月  
SSMA for Access 的 2012 年 1 月版本包含下列變更：  
  
-   提供的選項不會保存使用者名稱和密碼的 MS 存取連結資料表，在移轉之後。  
-   設定對 No Action 循環參考的重疊顯示動作。  
-   提供適當的訊息，指出循環參考的重疊顯示動作，已設定為 No Action。  
  
## <a name="july-2011"></a>2011 年 7 月  
SSMA for Access 的 2011 年 7 月版本包含下列變更：  
  
-   在資料遷移期間報告改良的錯誤。  
  
## <a name="april-2011"></a>2011 年 4 月  
SSMA for Access 的 2011 年 4 月版本包含下列變更：  
  
-   新增可安裝的 「 SSMA 的存取 」，可支援單一[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005 年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"和 Azure SQL。  
-   加入連接的能力[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]"Denali"。  
-   加入的 SSMA for Access 主控台版本支援回溯相容性。 您可以開啟 SSMA v5.0 稍早的版本所建立的專案。
-   加入與舊版本的 SSMA 產品安裝 SSMA v5.0 產品並存 (SxS) 的能力。  
  
## <a name="july-2010"></a>2010 年 7 月  
SSMA for Access 2010 年 7 月版本包含下列變更：  
  
-   已新增的支援移轉至 SQL Server 2008 R2 和 SQL Azure。
-   加入 SQL Server 和 Azure SQL 的安全連線。  
-   已新增的支援的 Access 2010 資料庫。
-   加入新的 SSMA 主控台應用程式的命令列執行。
-   已新增的支援 SQL Server DateTime2 資料類型。
  
## <a name="june-2008"></a>2008 年 6 月  
SSMA for Access 的 2008 年 6 月版本包含下列變更：  
  
-   加入的 Access 2007 資料庫的支援。  
  
## <a name="may-2007"></a>May 2007  
SSMA for Access May 2007 版本包含下列變更：  
  
-   使用群組原則的 Access 資料庫的已加入的支援。  
-   提供了可從 SQL Server 中繼資料總管 刪除已轉換的物件。  
-   已新增的支援的 SQL Server 中的使用者輸入註解格式 SQL 模式。  
-   已加入的物件轉換中的增強功能。  
  
## <a name="november-2006"></a>2006 年 11 月  
SSMA for Access 的 2006 年 11 月版本包含下列變更：  
  
-   加入新的 Database 移轉精靈可引導您完成移轉單一資料庫的存取權從[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
-   加入新的轉換，負載，並將 Access 資料庫的移轉命令載入轉換的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，並移轉資料到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]所有以一個步驟。  
-   提升的查詢的移轉。 現在將更選取檢視的查詢，請查詢移轉。 如需詳細資訊，請參閱[轉換來存取資料庫物件](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)。  
-   加入編輯資料表和索引的屬性上的功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**資料表** 索引標籤。  
-   加入新的通用設定：  
    -   您可以選擇在編輯器視窗中顯示行號。  
    -   您可以設定 SSMA 提示來取代重複的物件，或一律或永遠不會取代重複的物件結構描述轉換期間。  
-   加入新的轉換選項可讓您指定複雜的查詢包含萬用字元時，SSMA 是否顯示警告。  
  
## <a name="july-2006"></a>2006 年 7 月  
2006 年 7 月版的 SSMA for Access 是最早的版本。

