---
title: OLE DB 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 601e3b906a8c10d6f073eb05b3f62857f8c79bac
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390459"
---
# <a name="ole-db-connection-manager"></a>OLE DB 連接管理員
  OLE DB 連接管理員可透過使用 OLE DB 提供者讓封裝連接到資料來源。 例如，與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接的 OLE DB 連線管理員可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 OLEDB 提供者不支援多重子網路容錯移轉叢集的新連接字串關鍵字 (MultiSubnetFailover=True)。 如需詳細資訊，請參閱 < [SQL Server 版本資訊](https://go.microsoft.com/fwlink/?LinkId=247824)部落格文章，以及[AlwaysOn 多重子網路容錯與 SSIS](https://go.microsoft.com/fwlink/?LinkId=247825)，www.mattmasson.com 上。  
  
 有數個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 工作和資料流程元件使用 OLE DB 連線管理員。 例如，OLE DB 來源和 OLE DB 目的地使用此連線管理員來擷取和載入資料，Execute SQL 工作則可以使用此連線管理員來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫以執行查詢。  
  
 OLE DB 連接管理員還可用來存取 Unmanaged 程式碼 (使用如 C++ 等語言) 撰寫之自訂工作中的 OLE DB 資料來源。  
  
 當您將 OLE DB 連接管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行階段解析為 OLE DB 連接的連接管理員、設定連接管理員屬性，並將連接管理員加入封裝上的 `Connections` 集合。  
  
 連接管理員的 `ConnectionManagerType` 屬性會設為 `OLEDB`。  
  
 您可以利用下列方式來設定 OLE DB 連接管理員：  
  
-   提供設定的特定連接字串，以符合所選取提供者的需求。  
  
-   視提供者而定，包含要連接的資料來源名稱。  
  
-   為所選的提供者提供適當的安全性認證。  
  
-   指示是否在執行階段保留從連接管理員建立的連接。  
  
## <a name="logging"></a>記錄  
 您可以記錄 OLE DB 連接管理員對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，疑難排解 OLE DB 連接管理員對外部資料來源執行的連接。 若要記錄 OLE DB 連線管理員對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷] 事件。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuration-of-the-oledb-connection-manager"></a>OLEDB 連接管理員的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請參閱 [設定 OLE DB 連線管理員](../configure-ole-db-connection-manager.md)。 如需以程式設計方式設定連線管理員的相關資訊，請參閱《開發人員指南》中 **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** 類別的文件集。  
  
## <a name="related-content"></a>相關內容  
  
-   social.technet.microsoft.com 上的 Wiki 文章： [SSIS with Oracle Connectors](https://go.microsoft.com/fwlink/?LinkId=220670) (SSIS 與 Oracle 連接器)。  
  
-   carlprothman.net 上的技術文件： [Connection Strings for OLE DB Providers](https://go.microsoft.com/fwlink/?LinkId=220744)(OLE DB 提供者的連接字串)。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 來源](../data-flow/ole-db-source.md)   
 [OLE DB 目的地](../data-flow/ole-db-destination.md)   
 [執行 SQL 工作](../control-flow/execute-sql-task.md)   
 [Integration Services &#40;SSIS&#41; 連接](integration-services-ssis-connections.md)  
  
  
