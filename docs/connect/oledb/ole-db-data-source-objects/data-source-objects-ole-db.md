---
title: 資料來源物件 (OLE DB) |Microsoft 文件
description: 資料來源物件 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], data source objects
- OLE DB Driver for SQL Server, data source objects
- MSOLEDBSQL, data source objects
- OLE DB Driver for SQL Server, data source objects
- OLE DB data source objects [OLE DB Driver for SQL Server]
- data source objects [OLE DB]
- CLSID
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1fd12d353e5c7ecc47852ea1ab570694312df1f
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2018
---
# <a name="data-source-objects-ole-db"></a>資料來源物件 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB 驅動程式適用於 SQL Server 會使用資料來源這個詞用來建立資料存放區的連結，例如 OLE DB 介面的集合[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 建立資料來源物件的提供者的執行個體是 SQL Server 取用者的 OLE DB 驅動程式第一項工作。  
  
 每個 OLE DB 提供者都會為自己宣告一個類別識別碼 (CLSID)。 SQL Server OLE DB 驅動程式的 CLSID 為 C/c + + GUID CLSID_MSOLEDBSQL (MSOLEDBSQL_CLSID 會解析為正確的符號 progid 您參考 msoledbsql.h 檔案中)。 透過 CLSID，取用者會使用 OLE **CoCreateInstance**函數來製造資料來源物件的執行個體。  
  
 OLE DB 驅動程式的 SQL Server 是在同處理序伺服器。 SQL Server 物件的執行個體的 OLE DB 驅動程式會建立使用 CLSCTX_INPROC_SERVER 巨集指示可執行檔的內容。  
  
 SQL Server 資料來源物件，OLE DB 驅動程式會公開允許取用者連接到現有的 OLE DB 初始化介面[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫。  
  
 透過適用於 SQL Server 的 OLE DB 驅動程式的每個連接都會自動設定這些選項：  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 此範例會使用類別識別碼巨集來建立 OLE DB 驅動程式，SQL Server 資料來源物件，並且取得參考其**IDBInitialize**介面。  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_MSOLEDBSQL, NULL, CLSCTX_INPROC_SERVER,  
    IID_IDBInitialize, (void**) &pIDBInitialize);  
  
if (SUCCEEDED(hr))  
{  
    //  Perform necessary processing with the interface.  
    pIDBInitialize->Uninitialize();  
    pIDBInitialize->Release();  
}  
else  
{  
    // Display error from CoCreateInstance.  
}  
```  
  
 成功建立 SQL Server 資料來源物件 OLE DB 驅動程式的執行個體，取用者應用程式可以透過初始化資料來源並建立工作階段來繼續。 OLE DB 工作階段會顯示允許資料存取與操作的介面。  
  
 SQL Server OLE DB 驅動程式會建立指定的執行個體其第一個連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]成功的資料來源初始化的一部分。 只要在任何資料來源初始化介面上，或直到維護參考維持連線**Uninitialize**方法呼叫。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [資料來源屬性 &#40; OLE DB &#41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [資料來源資訊屬性](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [初始化和授權屬性](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [工作階段](../../oledb/ole-db-data-source-objects/sessions.md)  
  
-   [工作階段屬性-SQL Server 的 OLE DB 驅動程式](../../oledb/ole-db-data-source-objects/session-properties-oledb-driver-for-sql-server.md)  
  
-   [保存資料來源物件](../../oledb/ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 的 OLE DB 驅動程式&#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
  
  
