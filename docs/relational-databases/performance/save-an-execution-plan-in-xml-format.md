---
title: "以 XML 格式儲存執行計畫 | Microsoft 文件"
ms.custom: 
ms.date: 08/21/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML query plans [SQL Server]
- opening execution plans
- XML Showplans [SQL Server]
- execution plans [SQL Server], saving
- saving execution plans
ms.assetid: c439e53b-56f3-4442-97c6-dabd48a203d8
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cc3f2b3a6efd75a97ca8e4198b0b375b55d598fa
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="save-an-execution-plan-in-xml-format"></a>以 XML 格式儲存執行計畫
  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 將執行計畫儲存為 XML 檔，並開啟它們來進行檢視。  
  
 若要使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的執行計畫功能，或使用 XML Showplan SET 選項，使用者必須具有適當的權限，才能執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢來產生執行計畫，同時使用者還必須具有查詢所參考之所有資料庫的 SHOWPLAN 權限。  
  
### <a name="to-save-a-query-plan-by-using-the-xml-showplan-set-options"></a>若要使用 XML Showplan SET 選項來儲存查詢計畫  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，開啟查詢編輯器並連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  利用下列陳述式開啟 [SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md)：  
  
    ```t-sql  
    SET SHOWPLAN_XML ON;  
    GO  
    ```  
  
     若要開啟 [STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md)，請使用下列陳述式：  
  
    ```t-sql  
    SET STATISTICS XML ON;  
    GO  
    ```  
  
     > [!NOTE] 
     > SHOWPLAN_XML 會產生查詢的編譯階段查詢執行計畫資訊，但不會執行查詢。 這就是所謂的**估計**執行計畫。 STATISTICS XML 會產生查詢的執行階段查詢執行計畫資訊，並且執行查詢。 這就是所謂的**實際**執行計畫。  
  
3.  執行查詢。 範例：  
  
    ```t-sql  
    USE AdventureWorks2012;  
    GO  
    SET SHOWPLAN_XML ON;  
    GO  
    -- Execute a query.  
    SELECT BusinessEntityID   
    FROM HumanResources.Employee  
    WHERE NationalIDNumber = '509647174';  
    GO  
    SET SHOWPLAN_XML OFF;  
    ```  
  
4.  在 [結果] 窗格中，以滑鼠右鍵按一下包含查詢計劃的 [Microsoft SQL Server XML 執行程序表]，然後按一下 [儲存結果]。  
  
5.  在 [儲存 \<方格或文字> 結果]  對話方塊的 [存檔類型] 方塊中，按一下 [所有檔案 (\*.\*)]。  
  
6.  在 [檔案名稱] 方塊中，提供格式為 \<名稱**>.sqlplan** 的名稱，然後按一下 [儲存]。  
  
### <a name="to-save-an-execution-plan-by-using-sql-server-management-studio-options"></a>若要使用 SQL Server Management Studio 選項來儲存執行計畫  
  
1.  使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]來產生一個評估的執行計畫或實際執行計畫。 如需詳細資訊，請參閱[顯示估計執行計畫](../../relational-databases/performance/display-the-estimated-execution-plan.md)和[顯示實際執行計畫](../../relational-databases/performance/display-an-actual-execution-plan.md)。  
  
2.  在結果窗格的 [執行計畫] 索引標籤中，以滑鼠右鍵按一下圖形執行計畫，然後選擇 [另存執行計畫為]。  
  
     您也可以從 [檔案] 功能表選擇 [另存執行計畫為]。  
  
3.  在 [另存新檔] 對話方塊中，請確認將 [檔案類型] 設為 [執行計畫檔案 (\*.sqlplan)]。  
  
4.  在 [檔案名稱] 方塊中，提供格式為 \<名稱**>.sqlplan** 的名稱，然後按一下 [儲存]。  
  
### <a name="to-open-a-saved-xml-query-plan-in-sql-server-management-studio"></a>若要在 SQL Server Management Studio 中開啟已儲存的 XML 查詢計畫  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的 [檔案] 功能表上，選擇 [開啟]，然後按一下 [檔案]。  
  
2.  在 [開啟檔案] 對話方塊中，將 [檔案類型] 設為 [執行計畫檔案 (\*.sqlplan)]，以產生已儲存之 XML 查詢計劃檔案的篩選清單。  
  
3.  選取您要檢視的 XML 查詢計劃檔案，然後按一下 [開啟]。  
  
     您也可以在 Windows 檔案總管中，按兩下副檔名為 **.sqlplan** 的檔案。 計畫會在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中開啟。  
  
## <a name="see-also"></a>另請參閱  
 [SET SHOWPLAN_XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)   
 [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md)  
  
  
