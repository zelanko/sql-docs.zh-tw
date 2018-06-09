---
title: 資料來源物件 (OLE DB) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], data source objects
- SQL Server Native Client, data source objects
- SQLNCLI, data source objects
- SQL Server Native Client OLE DB provider, data source objects
- OLE DB data source objects [SQL Server Native Client]
- data source objects [OLE DB]
- CLSID
ms.assetid: c1d4ed20-ad3b-4e33-a26b-38d7517237b7
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2c6d8057f9a85491a2936a78140e0da69299969f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34708136"
---
# <a name="data-source-objects-ole-db"></a>資料來源物件 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 介面，可用來建立連結至資料存放區中，例如一組使用資料來源這個詞[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 建立資料來源物件的提供者的執行個體是第一項工作的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 取用者。  
  
 每個 OLE DB 提供者都會為自己宣告一個類別識別碼 (CLSID)。 CLSID [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者是 C/c + + GUID CLSID_SQLNCLI10 (sqlncli_clsid 符號將會的解析的正確 progid 您參考之 sqlncli.h 檔中)。 透過 CLSID，取用者會使用 OLE **CoCreateInstance**函數來製造資料來源物件的執行個體。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 是同處理序伺服器。 執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者物件會建立使用 CLSCTX_INPROC_SERVER 巨集指示可執行檔的內容。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者資料來源物件會公開允許取用者連接到現有的 OLE DB 初始化介面[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。  
  
 每個連接是透過[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會自動設定這些選項：  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 這個範例會使用類別識別碼巨集來建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者資料來源物件，並取得參考其**IDBInitialize**介面。  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL, CLSCTX_INPROC_SERVER,  
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
  
 成功建立的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者資料來源物件，取用者應用程式可以透過初始化資料來源並建立工作階段來繼續。 OLE DB 工作階段會顯示允許資料存取與操作的介面。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會建立指定的執行個體其第一個連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成功的資料來源初始化的一部分。 只要在任何資料來源初始化介面上，或直到維護參考維持連線**Uninitialize**方法呼叫。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [資料來源屬性&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [資料來源資訊屬性](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [初始化和授權屬性](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [工作階段](../../relational-databases/native-client-ole-db-data-source-objects/sessions.md)  
  
-   [工作階段屬性 - SQL Server Native Client OLE DB 提供者](../../relational-databases/native-client-ole-db-data-source-objects/session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [保存的資料來源物件](../../relational-databases/native-client-ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
