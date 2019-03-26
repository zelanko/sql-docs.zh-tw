---
title: 使用 OLE DB 來源擷取資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: 4ca6eeb5-b60e-4b81-86dd-0674be8ae8d8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fd0adbfc5f2e7ea27a39758e81c0afaed0186123
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277168"
---
# <a name="extract-data-by-using-the-ole-db-source"></a>使用 OLE DB 來源來擷取資料
  若要加入及設定 OLE DB 來源，封裝必須已包含至少一個「資料流程」工作。  
  
### <a name="to-extract-data-using-an-ole-db-source"></a>若要使用 OLE DB 來源擷取資料  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[資料流程]** 索引標籤，然後將 OLE DB 來源從 **[工具箱]** 拖曳到設計介面。  
  
4.  按兩下 OLE DB 來源。  
  
5.  在 **[連接管理員]** 頁面上的 **[OLE DB 來源編輯器]** 對話方塊中，選取現有的 OLE DB 連接管理員，或按一下 **[新增]** 以新建連接管理員。 如需相關資訊，請參閱 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
6.  選取資料存取方法：  
  
    -   **資料表或檢視** ：選取 OLE DB 連接管理員連接之資料庫中的資料表或檢視。  
  
    -   **資料表名稱或檢視名稱變數** ：選取包含 OLE DB 連接管理員連接之資料庫中資料表或檢視名稱的使用者自訂變數。  
  
    -   **SQL 命令** ：輸入 SQL 命令，或按一下 **[建立查詢]** ，以使用 **[查詢產生器]** 撰寫 SQL 命令。  
  
        > [!NOTE]  
        >  命令可以包含參數。 如需詳細資訊，請參閱 [在資料流程元件中將查詢參數對應至變數](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)。  
  
    -   **來自變數的 SQL 命令** ：選取包含 SQL 命令的使用者自訂變數。  
  
        > [!NOTE]  
        >  變數必須在包含 OLE DB 來源之同一「資料流程」工作的範圍中定義，或在同一封裝的範圍中定義；此外，變數還必須具有字串資料類型。  
  
7.  若要更新外部及輸出資料行之間的對應，請按一下 **[資料行]** ，並在 **[外部資料行]** 清單中選取不同的資料行。  
  
8.  (選擇性) 藉由編輯 **[輸出資料行]** 清單中的值，更新輸出資料行的名稱。  
  
9. 若要設定錯誤輸出，請按一下 **[錯誤輸出]**。 如需詳細資訊，請參閱 [偵錯資料流程](../../integration-services/troubleshooting/debugging-data-flow.md)。  
  
10. 您可以按一下 **[預覽]** ，以檢視 OLE DB 來源擷取之最多 200 個資料列的資料。  
  
11. 按一下 [確定] 。  
  
12. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 來源](../../integration-services/data-flow/ole-db-source.md)   
 [Integration Services 轉換](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路徑](../../integration-services/data-flow/integration-services-paths.md)   
 [資料流程工作](../../integration-services/control-flow/data-flow-task.md)  
  
  
