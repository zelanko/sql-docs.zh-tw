---
title: 資料來源物件 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d8bb984c789f759eb764ad580f971ab71c9fc946
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297622"
---
# <a name="data-source-objects-ole-db"></a>資料來源物件 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]這個機客戶端使用字語資料來源的 OLE DB 介面集,用於建立指向資料儲存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的連結,例如 。 創建提供程式的數據源物件的實例是本機用戶端消費者的第一個[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]任務。  
  
 每個 OLE DB 提供者都會為自己宣告一個類別識別碼 (CLSID)。 本機用戶端 OLE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB 提供程式的 CLSID 是 C/C++ GUID CLSID_SQLNCLI10(符號SQLNCLI_CLSID解析為您引用的 sqlncli.h 檔中的正確 progid)。 透過 CLSID，取用者會使用 OLE **CoCreateInstance** 函式來製造資料來源物件的執行個體。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端是進程中的伺服器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式物件的實例使用CLSCTX_INPROC_SERVER宏來指示可執行上下文。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式數據來源物件公開允許使用者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接到現有資料庫的 OLE DB 初始化介面。  
  
 透過[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機客戶端 OLE 資料庫提供程式進行的每個連線會自動設定這些選項:  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 本示例使用類識別符宏創建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式數據來源物件,並獲取對其**IDB 初始化介面的**引用。  
  
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
  
 成功創建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式數據來源物件的實例後,消費者應用程式可以通過初始化數據源和創建會話來繼續。 OLE DB 工作階段會顯示允許資料存取與操作的介面。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式首次連接到 指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的實例, 作為成功數據來源初始化的一部分。 只要在任何資料來源初始化介面上維持參考，或是在呼叫 **IDBInitialize::Uninitialize** 方法前，都會維持連線。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [資料來源屬性 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [資料來源資訊屬性](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [初始化和授權屬性](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [工作階段](../../relational-databases/native-client-ole-db-data-source-objects/sessions.md)  
  
-   [工作階段屬性 - SQL Server Native Client OLE DB 提供者](../../relational-databases/native-client-ole-db-data-source-objects/session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [保存的資料來源物件](../../relational-databases/native-client-ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
