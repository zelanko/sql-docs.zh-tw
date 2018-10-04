---
title: ADOStreamConstruction 介面 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf21be88854837ab2dff1a8bc8bc73f44a6e20c9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828742"
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction 介面
**ADOStreamConstruction**介面用來建構 ADO **Stream**的 OLE DB 物件**IStream** C/c + + 應用程式中的物件。  
  
## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|[Stream 屬性](../../../ado/reference/ado-api/stream-property.md)|讀取/寫入。 取得/設定 OLE DB **Stream**物件。|  
  
## <a name="methods"></a>方法  
 無。  
  
## <a name="events"></a>事件  
 無。  
  
## <a name="remarks"></a>備註  
 指定 OLE DB **IStream**物件 (`pStream`)，建構的 ADO **Stream**物件 (`adoStr`) 相當於下列三種基本作業：  
  
1.  建立 ADO **Stream**物件：  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  查詢**IADOStreamConstruction**介面上**Stream**物件：  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 呼叫`IADOStreamConstruction::get_Stream`屬性的方法，來設定 OLE DB **IStream** ado 物件**Stream**物件：  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 結果`adoStr`物件現在表示 ADO **Stream**建構從 OLE DB 物件**IStream**物件。  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 或更新版本  
  
 **程式庫：** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](../../../ado/reference/ado-api/ado-api-reference.md)
