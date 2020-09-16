---
title: 使用 Database Engine Tuning Advisor
description: 了解 SQL Server Database Engine Tuning Advisor GUI 如何微調資料庫、管理微調工作階段，以及顯示微調建議。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 3317d4f8-ed9e-4f2e-b5f1-a6bf3a9d6c8d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: bd60220151fb8f389ac7c82c1bdb0f10cf46bba1
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2020
ms.locfileid: "88713806"
---
# <a name="lesson-2-using-database-engine-tuning-advisor"></a>第 2 課：使用 Database Engine Tuning Advisor

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

您可以利用 Database Engine Tuning Advisor 來微調資料庫、管理微調工作階段，以及檢視微調建議。 非常了解實體設計結構的進階使用者可以利用這套工具來執行探勘資料庫微調分析。 資料庫微調新手也可以利用這套工具來尋找他們所微調之工作負載的實體設計結構的最佳組態。 這個課程提供基本練習來協助不熟悉 Database Engine Tuning Advisor 圖形化使用者介面的資料庫管理員，以及不太了解實體設計結構的系統管理員。  

## <a name="prerequisites"></a>必要條件 

若要完成本教學課程，您需要 SQL Server Management Studio、執行 SQL Server 伺服器的存取權，以及 AdventureWorks 資料庫。

- 安裝 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks2017 範例資料庫](../../samples/adventureworks-install-configure.md?view=sql-server-2017) \(機器翻譯\)。


如需在 SSMS 中還原資料庫的指示，請參閱：[還原資料庫。](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md?view=sql-server-2017)

  >[!NOTE]
  > 本教學課程適用於熟悉使用 SQL Server Management Studio 與基本資料庫管理工作的使用者。 
  
## <a name="tuning-a-workload"></a>微調工作負載
您可以利用 Database Engine Tuning Advisor 來找出最好的實體資料庫設計，以改進您選擇要微調的資料庫和資料表的查詢效能。  

1.  複製範例 [SELECT](../../t-sql/queries/select-examples-transact-sql.md) 陳述式，並將該陳述式貼入 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的 [查詢編輯器] 中。 在您很容易找到的目錄中，將檔案儲存成 **MyScript.sql**。 下方提供適用於 AdventureWorks2017 資料庫的範例。  

 ```sql
 Use [Adventureworks2017]; -- may need to modify database name to match database
 GO
 SELECT DISTINCT pp.LastName, pp.FirstName 
 FROM Person.Person pp JOIN HumanResources.Employee e
 ON e.BusinessEntityID = pp.BusinessEntityID WHERE pp.BusinessEntityID IN 
 (SELECT SalesPersonID 
 FROM Sales.SalesOrderHeader
 WHERE SalesOrderID IN 
 (SELECT SalesOrderID 
 FROM Sales.SalesOrderDetail
 WHERE ProductID IN 
 (SELECT ProductID 
 FROM Production.Product p 
 WHERE ProductNumber = 'BK-M68B-42')));
 GO
 ```

  ![儲存 SQL 查詢](media/dta-tutorials/dta-save-query.png)
  
2.  啟動 Database Engine Tuning Advisor。 從 SQL Server Management Studio (SSMS) 的 [工具] 功能表中選取 [Database Tuning Advisor]。  如需詳細資訊，請參閱[啟動 Database Engine Tuning Advisor](lesson-1-basic-navigation-in-database-engine-tuning-advisor.md#launch-database-tuning-advisor)。 在 [連線至伺服器] 對話方塊中，連線至 SQL Server。  
  
3.  在 Database Engine Tuning Advisor GUI 右窗格的 [一般] 索引標籤中，在 [工作階段名稱] 中輸入 **MySession**。 
  
4.  針對 [工作負載] 選取 [檔案]，然後選取望遠鏡圖示以**瀏覽工作負載檔案**。 找到您在步驟 1 中儲存的 **MyScript.sql** 檔案。  

   ![尋找先前儲存的指令碼](media/dta-tutorials/dta-script.png)
  
5.  在 [工作負載分析的資料庫]**** 清單中選取 [AdventureWorks2017]，在 [選取要微調的資料庫與資料表]**** 方格中選取 [AdventureWorks2017]，並選取 [儲存微調記錄]****。 [工作負載分析的資料庫] 指定在微調工作負載時 Database Engine Tuning Advisor 所連接的第一個資料庫。 在微調開始之後，Database Engine Tuning Advisor 會連接到工作負載包含的 `USE DATABASE` 陳述式所指定的資料庫。  

  ![資料庫的 DTA 選項](media/dta-tutorials/dta-select-db.png)
  
6.  按一下 [微調選項] 索引標籤。您將不會設定這個練習的任何微調選項，但會花一些時間來檢閱預設的微調選項。 請按 F1 鍵來檢視這個索引標籤頁的說明。 請按一下 [進階選項] 來檢視其他微調選項。 如需這裡所顯示之微調選項的相關資訊，請按一下 [進階微調選項] 對話方塊中的 [說明]。 請按一下 [取消] 來關閉 [進階微調選項] 對話方塊，保持選取預設的選項。  

  ![DTA 微調選項](media/dta-tutorials/dta-tuning-options.png)
  
7.  按一下工具列上的 **[開始分析]** 按鈕。 當 Database Engine Tuning Advisor 分析工作負載時，您可以在 [進度] 索引標籤中監視狀態。微調完成之後，會出現 [建議] 索引標籤。  
  
    如果您接收到關於微調停止日期和時間的錯誤，請檢查主要 [微調選項] 索引標籤上的 [停止時間]。確定 [停止時間] 的日期和時間大於目前的日期和時間，必要時，請變更它們。  

  ![啟動 DTA 分析](media/dta-tutorials/dta-start-analysis.png)

  
8.  完成分析之後，在 [動作] 功能表上，按一下 [儲存建議]，將建議儲存成一份 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 在 [另存新檔]**** 對話方塊中，導覽到用來儲存建議指令碼的目錄，再輸入 **MyRecommendations** 檔案名稱。  

  ![儲存 DTA 建議](media/dta-tutorials/dta-save-recommendations.png)

## <a name="view-tuning-recommendations"></a>檢視微調建議
  
1.  在 [建議] 索引標籤上，利用索引標籤頁面底端的捲軸來檢視所有 [索引建議] 資料行。 每個資料列都代表一個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 建議要卸除或建立的資料庫物件 (索引或索引檢視表)。 捲到最右側資料行，按一下 [定義]。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 會顯示一個 [SQL 指令碼預覽]**** 視窗，供您檢視在這個資料列上建立或卸除資料庫物件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 按一下 [關閉] 來關閉預覽視窗。  
  
    如果您在尋找包含連結的 [定義]**** 時遇到困難，請按一下索引標籤式頁面底端的 [顯示現有的物件]**** 核取方塊加以清除，以減少顯示的資料列數。 當您清除這個核取方塊時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 只會顯示它已產生建議的物件。 選取 [顯示現有的物件] 核取方塊，以檢視 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫目前已存在的所有資料庫物件。 請利用索引標籤頁面右側的捲軸來檢視所有物件。

  ![DTA 索引建議](media/dta-tutorials/dta-recommendation.png)  
  
2.  在 [索引建議] 窗格中，以滑鼠右鍵按一下方格。 這個右鍵功能表可讓您選取和取消選取各項建議。 您也可以利用它來變更方格文字的字型。  
 
   ![索引建議的 [選取] 功能表](media/dta-tutorials/dta-index-recommendation-options.png)
  
3.  在 [動作] 功能表上，按一下 [儲存建議]，將所有建議儲存在單一 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼中。 請將這份指令碼命名為 **MySessionRecommendations.sql**。  
  
    在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的查詢編輯器中，開啟 MySessionRecommendations.sql 指令碼來檢視它。 您可能會在查詢編輯器中執行這份指令碼，將建議套用在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫上，但請勿執行這個動作。 請在查詢編輯器中關閉這份指令碼，不要執行它。  
  
    或者，您也可以在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 的 [動作]**** 功能表上，按一下 [套用建議]**** 來套用建議，但現在請先不要在這個練習中套用這些建議。  
  
4.  如果 [建議]**** 索引標籤中存在多個建議，請清除某些在 [索引建議]**** 方格中列出資料庫物件的資料列。  
  
5.  在 **[動作]** 功能表上，按一下 **[評估建議]** 。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 就會建立一個新的微調工作階段，供您評估 MySession 的部分原始建議。  
  
6.  輸入 **EvaluateMySession** 來作為新的 [工作階段名稱]，並按一下工具列上的 [開始分析] 按鈕。 您可以針對這個新的微調工作階段，重複步驟 2 和 3 來檢視它的建議。  
  
### <a name="summary"></a>摘要  
如果您在執行工作階段之後，覺得必須變更微調選項，您可能需要評估部分微調建議。 例如，如果您要求 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 在指定工作階段的微調選項時考慮索引檢視表，但在產生建議之後，又決定不用索引檢視表。 接著，您可以利用 [動作] 功能表的 [評估建議] 選項，使 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 在不考慮索引檢視表的情況下，重新評估工作階段。 當您使用 [評估建議]**** 選項時，會以假設的方式，將先前產生的建議套用在目前的實體設計上，以達成第二個微調工作階段的實體設計。  
  
您可以在 [報表] 索引標籤中，檢視其他微調結果資訊。這個課程的下一項工作會描述這個索引標籤。  

## <a name="view-tuning-reports"></a>檢視微調報表
雖然檢視可用來實作微調結果的指令碼非常有用，但 Database Engine Tuning Advisor 也提供許多有用的報表供您檢視。 這些報表提供您在微調的資料庫其中之現有實體設計結構的相關資訊，以及所建議之結構的相關資訊。 您可以依照下列練習中的說明，按一下 [報表] 索引標籤來檢視這些微調報表。


1. 在 Database Tuning Advisor 中，選取 [報表] 索引標籤。 
2. 在 [微調摘要] 窗格中，您可以檢視這個微調工作階段的相關資訊。 請利用捲軸來檢視所有窗格內容。 請注意 [預期的改進百分比] 和 [建議使用的空間]。 當您設定微調選項時，可能會限制建議所用的空間。 在 [微調選項] 索引標籤上，選取 [進階選項]。 核取 [定義建議的最大空間]，並指定建議設定可以使用的最大空間 (以 MB 表示)。 請利用說明瀏覽器中的 [上一頁] 按鈕來返回這個教學課程。 

    ![DTA 微調摘要](media/dta-tutorials/dta-tuning-summary.png)
  
3.  在 [微調報表] 窗格中，按一下 [選取報表] 清單中的 [陳述式成本報表]。 如果您需要更多空間來檢視報表，請向左拖曳 [工作階段監視器] 窗格框線。 每個針對資料庫中某份資料表來執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式都有相關的效能成本。 您可以在資料表中常常存取的資料行上建立有效的索引來降低這個效能成本。 這份報表會顯示執行工作負載中某陳述式的原始成本和實作微調建議的成本之間的估計改進百分比。 請注意，報表所包含的資訊量以工作負載的長度和複雜度為基礎。  

    ![DTA 報表 - 陳述式成本](media/dta-tutorials/dta-statement-cost.png)
  
4.  以滑鼠右鍵按一下方格區域中的 [陳述式成本報表] 窗格，然後按一下 [匯出至檔案]。 將報表儲存成 **MyReport**。 檔案名稱會自動附加 .xml 副檔名。 您可以在喜愛的 XML 編輯器或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，開啟 MyReport.xml 來檢視報表內容。  
  
5.  返回 Database Engine Tuning Advisor 的 [報表] 索引標籤，然後以滑鼠右鍵按一下 [陳述式成本報表]。 檢視其他可用的選項。 請注意，您可以變更所檢視之報表的字型。 在這裡變更字型，也會變更其他索引標籤頁面的字型。  
  
6.  在 [選取報表] 清單中，按一下其他報表來熟悉它們。  
  
### <a name="summary"></a>摘要  
現在，您已在 Database Engine Tuning Advisor GUI 的 [報表] 索引標籤中，探索了 MySession 微調工作階段。 您可以利用這些相同的步驟來探索針對 EvaluateMySession 微調工作階段而產生的報表。 請在 [工作階段監視器] 窗格中，按兩下 [EvaluateMySession] 來開始作業。  


 ## <a name="next-lesson"></a>下一課  
[第 3 課：使用 DTA 命令提示字元公用程式](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
   
  
