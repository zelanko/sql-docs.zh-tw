---
title: 第 2 課：定義父報表的資料連線和資料表 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 395ef1f5189678892433de01f47dd04d08e1d1df
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270324"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>第 2 課：定義父報表的資料連接和資料表
  使用 Visual C# 的 ASP.NET 網站範本建立新的網站專案後，下一步是要建立父報表的資料連接和資料表。 在本教學課程中，資料連接是指 AdventureWorks2008 資料庫。 您也可以選擇連接到 AdventureWorks2012 資料庫。  
  
### <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>若要藉由加入 DataSet 定義資料連接和資料表 (針對父報表)  
  
1.  在 [網站] 功能表上選取 [新增項目]。  
  
2.  在 **加入新項目**對話方塊中，選取**資料集**，按一下 **新增**。 當系統提示您應該將項目加入**App_Code**資料夾，依序按一下**是**。  
  
     這樣會將新的 XSD 檔 **DataSet1.xsd** 新增至專案，並開啟 DataSet 設計工具。  
  
3.  從 [工具箱] 視窗中，拖曳**[TableAdapter](http://msdn.microsoft.com/library/bz9tthwx\(v=vs.100\).aspx)** 控制項至設計介面。 這樣會啟動 [ **TableAdapter** 組態精靈]。  
  
4.  在 **選擇資料連接**頁面上，按一下**新的連接**。  
  
5.  如果您是第一次在 Visual Studio 中建立資料來源，則會看見 [選擇資料來源] 頁面。 在 [資料來源] 方塊中，選取 [Microsoft SQL Server]。  
  
6.  在 [新增連線] 對話方塊中，執行下列步驟：  
  
    1.  在 **伺服器名稱**方塊中，輸入伺服器位置**AdventureWorks2008**資料庫所在。  
  
         預設的 SQL Server Express 執行個體為 **(local)\sqlexpress**。  
  
    2.  在 [登入伺服器] 區段中，選取提供資料存取的選項。 [使用 Windows 驗證] 是預設值。  
  
    3.  從**選取或輸入資料庫名稱**下拉式清單中，按一下**AdventureWorks2008**。  
  
    4.  按一下 [確定]，然後按一下 [下一步]。  
  
7.  如果您已在步驟 6 (b) 中選取 [使用 SQL Server 驗證]，請選取在字串中包含敏感性資料或在應用程式程式碼中設定資訊的選項。  
  
8.  在 **儲存連接字串儲存到應用程式組態檔**頁面上，輸入連接字串的名稱或接受預設值**AdventureWorks2008ConnectionString**。 按 [下一步] 。  
  
9. 在 [**選擇命令類型**頁面上，選取**使用 SQL 陳述式**，然後按一下**下一步]**。  
  
10. 在 [**輸入 SQL 陳述式**頁面上，輸入下列 TRANSACT-SQL 查詢，以從中擷取資料**AdventureWorks2008**資料庫，然後再按**下一步]**。  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
     您也可以建立查詢，即可**查詢產生器**，然後按一下 驗證查詢**執行查詢**。 如果查詢未傳回預期的資料，表示您可能使用較舊的 AdventureWorks 版本。 如需安裝的詳細資訊**AdventureWorks2008**版本的 AdventureWorks，請參閱[逐步解說： 安裝 AdventureWorks 資料庫](http://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx)。  
  
11. 在上**選擇要產生的方法**頁面上，務必取消核取**建立方法，以便將更新傳送至資料庫 (GenerateDBDirectMethods) 直接**，然後按一下 **完成**.  
  
    > [!WARNING]  
    >  務必取消核取建立  
  
     現在您已完成設定 ADO.NET DataTable 物件做為報表的資料來源。 在 Visual Studio 中的 DataSet 設計工具頁面上，應該會看到您加入的 DataTable 物件，並且列出查詢中指定的資料行。 根據查詢，DataSet1 包含 Product 資料表中的資料。  
  
12. 儲存檔案。  
  
13. 若要預覽資料，請按一下**預覽資料**上**Data**功能表，然後再按一下**預覽**。  
  
## <a name="next-task"></a>下一項工作  
 您已成功建立父報表的資料連接和資料表。 接下來您將使用 [報表精靈] 設計父報表。  
  
  
