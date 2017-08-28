---
title: "教學課程： 使用 OData 來源 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2c64cf8b-5edb-48df-8ffe-697096258f71
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: cbdc4a2e0719e65e378d232c5abcb5404e8342f1
ms.contentlocale: zh-tw
ms.lasthandoff: 08/23/2017

---
# <a name="tutorial-using-the-odata-source"></a>教學課程：使用 OData 來源
  本教學課程將逐步引導您進行從範例 **Northwind** OData 服務 (http://services.odata.org/V3/Northwind/Northwind.svc/) 擷取 **Employees** 集合，然後將該集合載入一般檔案的程序。  
  
## <a name="1-create-an-integration-services-project"></a>1.建立 Integration Services 專案  
  
1.  啟動 **[SQL Server Data Tools]** 或 [ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]]。  
  
2.  按一下 **[檔案]**、指向 **[新增]**，然後按一下 **[專案]**。  
  
3.  在 **[新增專案]** 對話方塊中，依序展開 **[已安裝的]**、 **[範本]**、 **[Business Intelligence]**，然後按一下 **[Integration Services]**。  
  
4.  選取該專案類型的 **[Integration Services 專案]** 。  
  
5.  輸入專案的 **[名稱]** 並選取 **[位置]** ，然後按一下 **[確定]**。  
  
## <a name="2-add-and-configure-an-odata-source"></a>2.加入及設定 OData 來源 
  
1.  從 [SSIS 工具箱] 將 [資料流程工作] 拖放至 SSIS 封裝的控制流程設計介面。  
  
2.  按一下**資料流程**索引標籤，或按兩下**Data Flow Task**開啟資料流程設計介面。  
  
3.  從 [SSIS 工具箱] 的 [Common] 群組中拖放 [OData 來源]。
  
4.  按兩下**OData 來源**元件，啟動**OData 來源編輯器** 對話方塊。  
  
5.  按一下 **[新增]** ，加入新的 OData 連接管理員。  
  
6.  輸入 **[服務文件位置]**的 OData 服務 URL。 這個 URL 可以是服務文件，或是特定摘要或實體的 URL。 為了此教學課程中，輸入服務文件的 URL: [http://services.odata.org/V3/Northwind/Northwind.svc/](http://services.odata.org/V3/Northwind/Northwind.svc/)。  
  
7.  確認已選取 **[Windows 驗證]** 做為用來存取 OData 服務的 **[驗證]** 。 **[Windows 驗證]** 預設為選取狀態。  
  
8.  按一下**測試連接**測試連接，並按一下**確定**完成建立 OData 連接管理員的執行個體。  
  
9. 在 **[OData 來源編輯器]** 對話方塊中，確認已針對 **[在資源路徑上使用集合]** 選項選取 **[集合]** 。  
  
10. 從**集合**下拉式清單中，選取**員工**。  
  
11. 針對 **[查詢選項]**輸入任何其他 OData 查詢選項或篩選。 例如， `$orderby=CompanyName&$top=100`。 為了此教學課程中，輸入`$top=5`。  
  
12. 按一下 **[預覽]** 預覽資料。  
  
13. 按一下左側功能窗格中的 **[資料行]** ，切換至 **[資料行]** 頁面。  
  
14. 透過選取核取方塊的方式，從 **[可用的外部資料行]**選取 **[EmployeeID]**、 **[FirstName]** 和 **[LastName]** 。  
  
15. 按一下 **[確定]** ，關閉 **[OData 來源編輯器]** 對話方塊。  
  
## <a name="3-add-and-configure-a-flat-file-destination"></a>3.加入和設定一般檔案目的地
  
1.  現在，從 [SSIS 工具箱] 將 [一般檔案目的地] 拖放至 [OData 來源] 元件下方的資料流程設計介面。  
  
2.  使用藍色箭頭連接 **[OData 來源]** 元件與 **[一般檔案目的地]** 元件。  
  
3.  按兩下 [一般檔案目的地]。 **[一般檔案目的地編輯器]** 對話方塊應會隨即出現。  
  
4.  在 **[一般檔案目的地編輯器]** 對話方塊中，按一下 **[新增]** 建立新的一般檔案連接管理員。  
  
5.  在 **[一般檔案格式]** 對話方塊中，選取 **[使用分隔符號]**。 然後您會看到**一般檔案連接管理員編輯器** 對話方塊。  
  
6.  在**一般檔案連接管理員編輯器**對話方塊中，針對**檔案名稱**，輸入`c:\Employees.txt`。  
  
7.  在左側功能窗格中，按一下 **[資料行]**。 您可以在此頁面上預覽資料。  
  
8.  按一下 [確定]，關閉 **[一般檔案連接管理員編輯器]** 對話方塊。  
  
9. 在 **[一般檔案目的地編輯器]** 對話方塊中，按一下左邊功能窗格中的 **[對應]** 。 檢閱對應。  
  
10. 按一下 [確定]，關閉 **[一般檔案目的地編輯器]** 對話方塊。  

## <a name="4-run-the-package"></a>4.執行封裝
執行 SSIS 封裝。 確認第一個名稱識別碼來建立輸出檔案，以及姓氏為五個員工從 OData 摘要。
  
  
