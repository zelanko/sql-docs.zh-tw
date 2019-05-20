---
title: OLE DB 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbconnection.f1
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ee9368848e7c939bbc8d4bb14eb49014ef5efb48
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728166"
---
# <a name="ole-db-connection-manager"></a>OLE DB 連接管理員

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  OLE DB 連接管理員可透過使用 OLE DB 提供者讓封裝連接到資料來源。 例如，與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接的 OLE DB 連線管理員可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。    
    
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 OLEDB 提供者不支援多重子網路容錯移轉叢集的新連接字串關鍵字 (MultiSubnetFailover=True)。 如需詳細資訊，請參閱 [SQL Server 版本資訊](https://go.microsoft.com/fwlink/?LinkId=247824) 和 www.mattmasson.com 上的部落格文章： [AlwaysOn 多重子網路容錯與 SSIS](https://www.mattmasson.com/2012/03/alwayson-multi-subnet-failover-and-ssis/)。    
> 
> [!NOTE]
>  如果資料來源為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007，則資料來源需要舊版 Excel 或 Access 以外的資料提供者。 如需詳細資訊，請參閱 [連接至 Excel 活頁簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md) 和 [連接至 Access 資料庫](../../integration-services/connection-manager/connect-to-an-access-database.md)。    
    
 有數個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 工作和資料流程元件使用 OLE DB 連線管理員。 例如，OLE DB 來源和 OLE DB 目的地使用此連線管理員來擷取和載入資料，Execute SQL 工作則可以使用此連線管理員來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫以執行查詢。    
    
 OLE DB 連接管理員還可用來存取 Unmanaged 程式碼 (使用如 C++ 等語言) 撰寫之自訂工作中的 OLE DB 資料來源。    
    
 當您將 OLE DB 連線管理員加入封裝時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行階段解析為 OLE DB 連接的連線管理員、設定連線管理員屬性，並將連線管理員加入封裝上的 **Connections** 集合。    
    
 連線管理員的 **ConnectionManagerType** 屬性會設為 **OLEDB**。    
    
 您可以利用下列方式來設定 OLE DB 連接管理員：    
    
-   提供設定的特定連接字串，以符合所選取提供者的需求。    
    
-   視提供者而定，包含要連接的資料來源名稱。    
    
-   為所選的提供者提供適當的安全性認證。    
    
-   指示是否在執行階段保留從連接管理員建立的連接。    
    
## <a name="logging"></a>記錄    
 您可以記錄 OLE DB 連接管理員對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，疑難排解 OLE DB 連接管理員對外部資料來源執行的連接。 若要記錄 OLE DB 連線管理員對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷] 事件。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。    
    
## <a name="configuration-of-the-oledb-connection-manager"></a>OLEDB 連接管理員的組態    
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請參閱 [設定 OLE DB 連線管理員](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)。 如需以程式設計方式設定連線管理員的相關資訊，請參閱《開發人員指南》中 **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** 類別的文件集。    
    
## <a name="related-content"></a>相關內容    
    
-   social.technet.microsoft.com 上的 Wiki 文章： [SSIS with Oracle Connectors](https://go.microsoft.com/fwlink/?LinkId=220670) (SSIS 與 Oracle 連接器)。    
    
-   carlprothman.net 上的技術文件： [Connection Strings for OLE DB Providers](https://go.microsoft.com/fwlink/?LinkId=220744)(OLE DB 提供者的連接字串)。    
    
## <a name="configure-ole-db-connection-manager"></a>設定 OLE DB 連接管理員
  使用 **[設定 OLE DB 連接管理員]** 對話方塊將連接加入資料來源，此連接可以是新的連接或是現有連接的副本。  
  
> [!NOTE]  
>  如果資料來源為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007，則資料來源需要舊版 Excel 以外的連接管理員。 如需詳細資訊，請參閱 [連接至 Excel 活頁簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)。  
>   
>  如果資料來源為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007，則資料來源需要舊版 Access 以外的 OLE DB 提供者。 如需詳細資訊，請參閱 [連接至 Access 資料庫](../../integration-services/connection-manager/connect-to-an-access-database.md)。  
  
 若要深入了解 OLE DB 連接管理員，請參閱＜ [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)＞。  
  
### <a name="options"></a>選項。  
 **資料連接**  
 從清單中選取現有的 OLE DB 資料連接。  
  
 **資料連接屬性**  
 檢視選取之 OLE DB 資料連接的屬性和值。  
  
 **新增**  
 使用 [連線管理員] 對話方塊來建立 OLE DB 資料連線。  
  
 **刪除**  
 選取資料連接，然後使用 [刪除] 按鈕將其刪除。  
  
## <a name="see-also"></a>另請參閱    
 [OLE DB 來源](../../integration-services/data-flow/ole-db-source.md)     
 [OLE DB 目的地](../../integration-services/data-flow/ole-db-destination.md)     
 [執行 SQL 工作](../../integration-services/control-flow/execute-sql-task.md)     
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  
