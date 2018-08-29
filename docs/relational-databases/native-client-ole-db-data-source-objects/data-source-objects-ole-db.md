---
title: 資料來源物件 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d08de334abbef003712e27c4f16dd0ba408ac79a
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43075006"
---
# <a name="data-source-objects-ole-db"></a>資料來源物件 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 介面，可用來建立連結到資料存放區，例如一組使用資料來源這個詞[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 建立資料來源物件的提供者的執行個體是第一項工作的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 取用者。  
  
 每個 OLE DB 提供者都會為自己宣告一個類別識別碼 (CLSID)。 CLSID 為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者是 C/c + + GUID CLSID_SQLNCLI10 (sqlncli_clsid 符號將會正確解析您參考之 sqlncli.h 檔中的 progid)。 透過 CLSID，取用者會使用 OLE **CoCreateInstance** 函式來製造資料來源物件的執行個體。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 是同處理序伺服器。 執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者物件會建立使用 CLSCTX_INPROC_SERVER 巨集指示可執行檔的內容。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者資料來源物件會公開允許取用者連接到現有的 OLE DB 初始化介面[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。  
  
 每個連接都會透過[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會自動設定這些選項：  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 此範例會使用類別識別碼巨集來建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者資料來源物件，並取得參考其**IDBInitialize**介面。  
  
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
  
 成功建立的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者資料來源物件，取用者應用程式可以透過初始化資料來源，並建立工作階段來繼續。 OLE DB 工作階段會顯示允許資料存取與操作的介面。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會指定執行個體的第一個連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成功初始化資料來源的一部分。 只要在任何資料來源初始化介面上維持參考，或是在呼叫 **IDBInitialize::Uninitialize** 方法前，都會維持連線。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [資料來源屬性 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [資料來源資訊屬性](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [初始化和授權屬性](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [工作階段](../../relational-databases/native-client-ole-db-data-source-objects/sessions.md)  
  
-   [工作階段屬性 - SQL Server Native Client OLE DB 提供者](../../relational-databases/native-client-ole-db-data-source-objects/session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [保存的資料來源物件](../../relational-databases/native-client-ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
