---
description: ADOStreamConstruction 介面
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 144965d31dbb11da6cbc9a3ee6b23cd79cda800e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776627"
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction 介面
**ADOStreamConstruction**介面是用來從 C/c + + 應用程式中 OLE DB **IStream**物件來建立 ADO**資料流程**物件。  
  
## <a name="properties"></a>屬性  
  
|屬性|描述|  
|-|-|  
|[資料流](./stream-property.md)|讀取/寫入。 取得/設定 OLE DB **資料流程** 物件。|  
  
## <a name="methods"></a>方法  
 無。  
  
## <a name="events"></a>事件  
 無。  
  
## <a name="remarks"></a>備註  
 假設有 OLE DB **IStream** 物件 (`pStream`) ，則 ADO **資料流程** 物件的結構 (`adoStr`) 為下列三個基本作業：  
  
1.  建立 ADO **資料流程** 物件：  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  查詢**資料流程**物件上的**IADOStreamConstruction**介面：  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 呼叫 `IADOStreamConstruction::get_Stream` 屬性方法，在 ADO**資料流程**物件上設定 OLE DB **IStream**物件：  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 結果 `adoStr` 物件現在代表從 OLE DB **IStream**物件所建立的 ADO**資料流程**物件。  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 或更新版本  
  
 連結**庫：** msado15.dll  
  
 **UUID：** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>另請參閱  
 [ADO API 參考](./ado-api-reference.md)