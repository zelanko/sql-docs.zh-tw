---
title: 資料來源物件（OLE DB） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63130592"
---
# <a name="data-source-objects-ole-db"></a>資料來源物件 (OLE DB)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 會針對用於建立資料存放區連結的一組 OLE DB 介面（例如），使用「資料來源」一[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]詞。 建立提供者之資料來源物件的實例是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 取用者的第一個工作。  
  
 每個 OLE DB 提供者都會為自己宣告一個類別識別碼 (CLSID)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者的 CLSID 是 C/c + + GUID CLSID_SQLNCLI10 （符號 SQLNCLI_CLSID 會解析成您所參考之 SQLNCLI 檔中的正確 progid）。 透過 CLSID，取用者會使用 OLE **CoCreateInstance** 函式來製造資料來源物件的執行個體。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 是同進程伺服器。 Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB 提供者物件的實例是使用 CLSCTX_INPROC_SERVER 宏所建立，以指出可執行檔內容。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者資料來源物件會公開允許取用者連接到現有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫的 OLE DB 初始化介面。  
  
 透過 Native Client OLE DB 提供[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]者所建立的每個連接都會自動設定這些選項：  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 這個範例會使用類別識別碼宏來建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者資料來源物件，並取得其**IDBInitialize**介面的參考。  
  
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
  
 成功建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者資料來源物件的實例之後，取用者應用程式就可以透過初始化資料來源並建立會話來繼續。 OLE DB 工作階段會顯示允許資料存取與操作的介面。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會在成功初始化資料來源時，使[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]其第一次連接到指定的實例。 只要在任何資料來源初始化介面上維持參考，或是在呼叫 **IDBInitialize::Uninitialize** 方法前，都會維持連線。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [&#40;OLE DB 的資料來源屬性&#41;](data-source-properties-ole-db.md)  
  
-   [資料來源資訊屬性](data-source-information-properties.md)  
  
-   [初始化和授權屬性](initialization-and-authorization-properties.md)  
  
-   [工作階段](sessions.md)  
  
-   [工作階段屬性](session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [保存的資料來源物件](persisted-data-source-objects.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
