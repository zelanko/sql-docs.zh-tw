---
title: 建立資料來源的連接 |Microsoft Docs
description: 建立資料來源使用 OLE DB Driver for SQL Server 的連接
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data sources [OLE DB Driver for SQL Server]
- connections [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, data source connections
- CoCreateInstance method
- OLE DB data sources [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 5a8af0b67c7998a9696f2451659901c79baaa8d9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813646"
---
# <a name="establishing-a-connection-to-a-data-source"></a>建立資料來源的連接
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  若要存取 OLE DB Driver for SQL Server，取用者必須先呼叫 **CoCreateInstance** 方法來建立資料來源物件的執行個體。 唯一類別識別項 (CLSID) 會識別每個 OLE DB 提供者。 OLE DB driver for SQL Server，類別識別項是 CLSID_MSOLEDBSQL。 您也可以使用該符號會解析為 OLE DB 驅動程式，會在您參考 msoledbsql.h 的 SQL server 的 MSOLEDBSQL_CLSID。  
  
 資料來源物件會公開 **IDBProperties** 介面，取用者可以使用這個介面來提供基本驗證資訊；例如，伺服器名稱、資料庫名稱、使用者識別碼和密碼。 呼叫 **IDBProperties::SetProperties** 方法可設定這些屬性。  
  
 如果有多個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體在電腦上執行，伺服器名稱會指定為 ServerName\InstanceName。  
  
 資料來源物件也會公開 **IDBInitialize** 介面。 屬性設定之後，就會呼叫 **IDBInitialize::Initialize** 方法來建立資料來源的連線。 例如：  
  
```cpp
CoCreateInstance(CLSID_MSOLEDBSQL,   
                 NULL,   
                 CLSCTX_INPROC_SERVER,  
                 IID_IDBInitialize,   
                 (void **) &pIDBInitialize)  
```
  
 呼叫 **CoCreateInstance** 會建立與 CLSID_MSOLEDBSQL 建立關聯之類別的單一物件 (與資料建立關聯的 CSLID 以及建立物件所使用的程式碼)。 IID_IDBInitialize 是介面 (**IDBInitialize**) 識別項的參考，用於與物件進行通訊。  
  
 下列範例示範如何初始化並建立資料來源的連接。
  
```cpp
#include "msoledbsql.h"
#include <stdio.h>

HRESULT InitializeAndEstablishConnection(IDBInitialize *&pIDBInitialize);

void main() {
    IDBInitialize       *pIDBInitialize = nullptr;
    HRESULT             hr = S_OK;

    // Initialize The Component Object Module Library
    CoInitialize(nullptr);

    hr = InitializeAndEstablishConnection(pIDBInitialize);
    if (FAILED(hr)) {
        printf("Failed to establish connection.\r\n");
        goto _ExitMain;
    }

    // Insert code that uses the established connection

_ExitMain:
    // Free Up All Allocated Memory
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
        pIDBInitialize = nullptr;
    }

    // Release The Component Object Module Library
    CoUninitialize();
}

HRESULT InitializeAndEstablishConnection(IDBInitialize *&pIDBInitialize) {
    IDBProperties   *pIDBProperties = nullptr;
    DBPROP          InitProperties[3] = { 0 };
    DBPROPSET       rgInitPropSet[1] = { 0 };
    HRESULT         hr = S_OK;

    // Obtain access to the OLE DB Driver for SQL Server.  
    hr = CoCreateInstance(CLSID_MSOLEDBSQL,
                          NULL,
                          CLSCTX_INPROC_SERVER,
                          IID_IDBInitialize,
                          (void **)&pIDBInitialize);
    if (FAILED(hr)) {
        printf("Failed to obtain access to the OLE DB Driver.\r\n");
        goto _ExitInitialize;
    }
    // Initialize property values needed to establish connection.  
    for (int i = 0; i < 3; i++) {
        VariantInit(&InitProperties[i].vValue);
    }

    // Server name.  
    // See DBPROP structure for more information on InitProperties  
    InitProperties[0].dwPropertyID = DBPROP_INIT_DATASOURCE;
    InitProperties[0].vValue.vt = VT_BSTR;
    InitProperties[0].vValue.bstrVal = SysAllocString(L"Server");
    InitProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;
    InitProperties[0].colid = DB_NULLID;

    // Database.  
    InitProperties[1].dwPropertyID = DBPROP_INIT_CATALOG;
    InitProperties[1].vValue.vt = VT_BSTR;
    InitProperties[1].vValue.bstrVal = SysAllocString(L"database");
    InitProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;
    InitProperties[1].colid = DB_NULLID;

    // Username (login).  
    InitProperties[2].dwPropertyID = DBPROP_AUTH_INTEGRATED;
    InitProperties[2].vValue.vt = VT_BSTR;
    InitProperties[2].vValue.bstrVal = SysAllocString(L"SSPI");
    InitProperties[2].dwOptions = DBPROPOPTIONS_REQUIRED;
    InitProperties[2].colid = DB_NULLID;

    // Construct the DBPROPSET structure(rgInitPropSet). The   
    // DBPROPSET structure is used to pass an array of DBPROP   
    // structures (InitProperties) to the SetProperties method.  
    rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;
    rgInitPropSet[0].cProperties = 3;
    rgInitPropSet[0].rgProperties = InitProperties;

    // Set initialization properties.  
    hr = pIDBInitialize->QueryInterface(IID_IDBProperties,
                                        (void **)&pIDBProperties);
    if (FAILED(hr)) {
        printf("Failed to obtain an IDBProperties interface.\r\n");
        goto _ExitInitialize;
    }
    hr = pIDBProperties->SetProperties(1, rgInitPropSet);
    if (FAILED(hr)) {
        printf("Failed to set initialization properties.\r\n");
        goto _ExitInitialize;
    }

    // Now establish the connection to the data source.  
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr)) {
        printf("Failed to establish connection with the server.\r\n");
        goto _ExitInitialize;
    }

_ExitInitialize:
    if (pIDBProperties)
    {
        pIDBProperties->Release();
        pIDBProperties = nullptr;
    }

    if (FAILED(hr))
    {
        if (pIDBInitialize)
        {
            pIDBInitialize->Release();
            pIDBInitialize = nullptr;
        }
    }

    return hr;
}
```  
  
## <a name="see-also"></a>另請參閱  
 [建立 OLE DB Driver for SQL Server 應用程式](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
