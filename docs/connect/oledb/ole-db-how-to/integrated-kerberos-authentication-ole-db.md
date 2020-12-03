---
title: 整合式 Kerberos 驗證 (OLE DB Driver) | Microsoft Docs
description: 透過此範例，了解如何使用 OLE DB Driver for SQL Server 中的 OLE DB 取得交互 Kerberos 驗證。
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e7ba7469d01b75397f706df403041ec68c1ed5f9
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506372"
---
# <a name="integrated-kerberos-authentication-ole-db"></a>整合式 Kerberos 驗證 (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  此範例顯示如何使用 OLE DB Driver for SQL Server 中的 OLE DB 取得交互 Kerberos 驗證。 此範例適用於 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 或更新版本。  
  
 如需 SPN 和 Kerberos 驗證的詳細資訊，請參閱[用戶端連接中的服務主體名稱 &#40;SPN&#41; 支援](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)。  
  
## <a name="example"></a>範例  
 您必須指定一個伺服器。 在 .cpp 檔案中，將 "MyServer" 變更為擁有 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (或更新版本) 執行個體的電腦名稱。  
  
 您也必須指定一個客戶提供的 SPN。 在 .cpp 檔案中，將 "CPSPN" 變更為客戶提供的 SPN。  
  
 請確認您的 INCLUDE 環境變數包含的目錄內含 msoledbsql.h。 使用 ole32.lib oleaut32.lib 編譯。  
  
```cpp
// compile with: ole32.lib oleaut32.lib
#pragma once

#define WIN32_LEAN_AND_MEAN   // Exclude rarely-used stuff from Windows headers
#include <stdio.h>
#include <tchar.h>
#include <msoledbsql.h>

#define CHECKHR(stmt) \
do\
{\
    hr = (stmt);\
    if (FAILED(hr))\
    {\
       printf("CHECK_HR " #stmt " failed at (%hs, %d), hr=0x%08X\r\n", __FILE__, __LINE__, hr); \
       goto CleanUp; \
    } \
} while (0)

#define SAFERELEASE(p) \
do\
{\
    if ((p) != nullptr)\
    {\
       p->Release(); \
       p = nullptr; \
    } \
} while (0)


int _tmain(int argc, _TCHAR* argv[])
{
    HRESULT hr = S_OK;
    IDBInitialize* pInitialize = nullptr;
    IDBProperties* pProperties = nullptr;
    DBPROP rgDBProp[1] = {};
    LPCWSTR lpwszProviderString = L"Server=MyServer;"   // server with SQL Server 2008 (or later)
       L"Trusted_Connection=Yes;"
       L"Encrypt=yes;"
       L"ServerSPN=CP_SPN;";   // customer-provided SPN

    DBPROPSET* prgPropertySets = nullptr;
    ULONG cPropertySets = 0;

    CHECKHR(CoInitialize(nullptr));
    CHECKHR(CoCreateInstance(CLSID_MSOLEDBSQL, nullptr, CLSCTX_INPROC_SERVER, __uuidof(IDBProperties), reinterpret_cast<void**>(&pProperties)));

    // set provider string
    rgDBProp[0].dwPropertyID = DBPROP_INIT_PROVIDERSTRING;
    rgDBProp[0].dwOptions = DBPROPOPTIONS_REQUIRED;
    rgDBProp[0].colid = DB_NULLID;
    VariantInit(&(rgDBProp[0].vValue));
    V_VT(&(rgDBProp[0].vValue)) = VT_BSTR;
    V_BSTR(&(rgDBProp[0].vValue)) = SysAllocString(lpwszProviderString);

    { // set the property to the property set
        DBPROPSET PropertySet[1] = {};
        PropertySet[0].rgProperties = &rgDBProp[0];
        PropertySet[0].cProperties = 1;
        PropertySet[0].guidPropertySet = DBPROPSET_DBINIT;

        // set properties and connect to server
        CHECKHR(pProperties->SetProperties(sizeof(PropertySet)/sizeof(DBPROPSET), PropertySet));
    }

    CHECKHR(pProperties->QueryInterface<IDBInitialize>(&pInitialize));
    CHECKHR(pInitialize->Initialize());

    { // get properties
        DBPROPIDSET rgDBPropIDSet[1] = {};

        DBPROPID rgDBPropID[2] = {};
        rgDBPropID[0] = SSPROP_INTEGRATEDAUTHENTICATIONMETHOD;
        rgDBPropID[1] = SSPROP_MUTUALLYAUTHENTICATED;

        rgDBPropIDSet[0].rgPropertyIDs = &rgDBPropID[0];
        rgDBPropIDSet[0].cPropertyIDs = 2;
        rgDBPropIDSet[0].guidPropertySet = DBPROPSET_SQLSERVERDATASOURCEINFO;
        CHECKHR(pProperties->GetProperties(1, rgDBPropIDSet, &cPropertySets, &prgPropertySets));
    }
    wprintf(L"Authentication method: %s\r\n", V_BSTR(&(prgPropertySets[0].rgProperties[0].vValue)));
    wprintf(L"Mutually authenticated: %s\r\n",
        (V_BOOL(&(prgPropertySets[0].rgProperties[1].vValue)) == VARIANT_TRUE) ? L"yes" : L"no");

CleanUp:
    SAFERELEASE(pProperties);
    SAFERELEASE(pInitialize);

    if (prgPropertySets)
    {
        for (ULONG iPropSet = 0; iPropSet < cPropertySets; ++iPropSet)
        {
            for (ULONG iProp = 0; iProp < prgPropertySets[iPropSet].cProperties; ++iProp)
            {
                VariantClear(&prgPropertySets[iPropSet].rgProperties[iProp].vValue);
            }
        }
    }

    VariantClear(&(rgDBProp[0].vValue));
    CoUninitialize();
}
```