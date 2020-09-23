---
title: 資料來源物件 (OLE DB 驅動程式) | Microsoft Docs
description: 了解 OLE DB Driver for SQL Server 取用者如何針對提供者建立資料來源物件的執行個體。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], data source objects
- OLE DB Driver for SQL Server, data source objects
- MSOLEDBSQL, data source objects
- OLE DB Driver for SQL Server, data source objects
- OLE DB data source objects [OLE DB Driver for SQL Server]
- data source objects [OLE DB]
- CLSID
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9abdf54d533eab604ff564c9f32b99b2eba566d9
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862399"
---
# <a name="data-source-objects-ole-db"></a>資料來源物件 (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 會針對用於建立資料存放區連結的 OLE DB 介面集合，使用資料來源這個詞；例如，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 建立提供者資料來源物件的執行個體，是 OLE DB Driver for SQL Server 取用者的第一個工作。  
  
 每個 OLE DB 提供者都會為自己宣告一個類別識別碼 (CLSID)。 適用於 OLE DB Driver for SQL Server 的 CLSID 是 C/C++ GUID CLSID_MSOLEDBSQL (MSOLEDBSQL_CLSID 符號將在您參考之 msoledbsql.h 檔案中解析為正確的 progid)。 透過 CLSID，取用者會使用 OLE **CoCreateInstance** 函式來製造資料來源物件的執行個體。  
  
 OLE DB Driver for SQL Server 是一個同處理序伺服程式。 OLE DB Driver for SQL Server 物件的執行個體會使用 CLSCTX_INPROC_SERVER 巨集來建立，以便指示可執行的內容。  
  
 OLE DB Driver for SQL Server 資料來源物件會公開允許取用者連線到現有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的 OLE DB 初始化介面。  
  
 透過 OLE DB Driver for SQL Server 建立的每個連線都會自動設定這些選項：  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 此範例會使用類別識別碼巨集來建立 OLE DB Driver for SQL Server 資料來源物件，並取得其 **IDBInitialize** 介面的參考。  
  
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
  
 成功建立 OLE DB Driver for SQL Server 資料來源物件的執行個體之後，取用者應用程式就可以透過初始化資料來源並建立工作階段來繼續。 OLE DB 工作階段會顯示允許資料存取與操作的介面。  
  
 OLE DB Driver for SQL Server 會在成功初始化資料來源後，先建立指定之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的連線。 只要在任何資料來源初始化介面上維持參考，或是在呼叫 **IDBInitialize::Uninitialize** 方法前，都會維持連線。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [資料來源屬性 &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [資料來源資訊屬性](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [初始化和授權屬性](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [工作階段](../../oledb/ole-db-data-source-objects/sessions.md)  
  
-   [工作階段屬性 - OLE DB Driver for SQL Server](../../oledb/ole-db-data-source-objects/session-properties-oledb-driver-for-sql-server.md)  
  
-   [保存的資料來源物件](../../oledb/ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 程式設計](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
