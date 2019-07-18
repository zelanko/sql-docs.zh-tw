---
title: 資料來源物件 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
ms.openlocfilehash: 6b602695720e0d6567e44e4fbe8fd06b6d496a6e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63130592"
---
# <a name="data-source-objects-ole-db"></a>資料來源物件 (OLE DB)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 介面，可用來建立連結到資料存放區，例如一組使用資料來源這個詞[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 建立資料來源物件的提供者的執行個體是第一項工作的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 取用者。  
  
 每個 OLE DB 提供者都會為自己宣告一個類別識別碼 (CLSID)。 CLSID [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者是 C /C++ GUID CLSID_SQLNCLI10 (sqlncli_clsid 符號將會正確解析您參考之 sqlncli.h 檔中的 progid)。 透過 CLSID，取用者會使用 OLE **CoCreateInstance** 函式來製造資料來源物件的執行個體。  
  
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
  
-   [資料來源屬性 &#40;OLE DB&#41;](data-source-properties-ole-db.md)  
  
-   [資料來源資訊屬性](data-source-information-properties.md)  
  
-   [初始化和授權屬性](initialization-and-authorization-properties.md)  
  
-   [工作階段](sessions.md)  
  
-   [工作階段屬性](session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [保存的資料來源物件](persisted-data-source-objects.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
