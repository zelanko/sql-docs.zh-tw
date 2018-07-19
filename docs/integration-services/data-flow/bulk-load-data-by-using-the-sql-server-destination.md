---
title: 使用 SQL Server 目的地來大量載入資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: 8f982f85-a82e-4e2d-9cd8-cd2f85402d8e
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f5573f001e063cba0900015517ad65b65531d0e
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35406590"
---
# <a name="bulk-load-data-by-using-the-sql-server-destination"></a>使用 SQL Server 目的地來大量載入資料
  若要加入及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地，封裝至少必須包含一個「資料流程」工作及一個資料來源。  
  
### <a name="to-load-data-using-a-sql-server-destination"></a>使用 SQL Server 目的地載入資料  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 [資料流程] 索引標籤，然後將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地從 [工具箱] 拖曳到設計介面。  
  
4.  將連接子拖曳到目的地，以便將目的地連接到資料流程中的來源或前一個轉換。  
  
5.  按兩下目的地。  
  
6.  在 [連線管理員] 頁面上的 [SQL Server 目的地編輯器] 中，選取現有的 OLE DB 連線管理員，或按一下 [新增] 以新建連線管理員。 如需詳細資訊，請參閱 [OLE DB 連線管理員](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
7.  若要指定載入資料的資料表或檢視，請執行下列其中之一：  
  
    -   選取現有的資料表或檢視。  
  
    -   按一下 [新增]，然後在 [建立資料表] 對話方塊中撰寫建立資料表或檢視的 SQL 陳述式。  
  
        > [!NOTE]  
        >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式將不會包含 FILESTREAM 屬性，即使來源資料表包含有宣告 FILESTREAM 屬性的資料行亦然。 若要執行具有 FILESTREAM 屬性的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件，請先在目的地資料庫上實作 FILESTREAM 儲存體。 然後在 **[建立資料表]** 對話方塊中，將 FILESTREAM 屬性加入至 CREATE TABLE 陳述式。 如需詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
8.  按一下 [對應]，然後將一個清單中的資料行拖曳到另一個清單，來將 [可用的輸入資料行] 清單中的資料行對應到 [可用的目的地資料行] 清單中的資料行。  
  
    > [!NOTE]  
    >  目的地會自動對應名稱相同的資料行。  
  
9. 按一下 [進階]，然後設定大量載入選項：[保留識別]、[保留 Null]、[資料表鎖定]、[檢查條件約束] 和 [引發觸發程序]。  
  
     (選擇性) 指定要插入的第一個和最後一個輸入資料列，插入作業停止之前發生的最大錯誤數目，以及排序插入的資料行。  
  
    > [!NOTE]  
    >  排序次序是由資料行列出的順序決定的。  
  
10. 按一下 [確定] 。  
  
11. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md)   
 [Integration Services 轉換](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路徑](../../integration-services/data-flow/integration-services-paths.md)   
 [資料流程工作](../../integration-services/control-flow/data-flow-task.md)  
  
  
