---
title: ADORecordConstruction 介面 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction
helpviewer_keywords:
- ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 925eefdbe8f5ff9196689026edb685c8f76d7d0a
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718173"
---
# <a name="adorecordconstruction-interface"></a>ADORecordConstruction 介面
**ADORecordConstruction**介面用來建構 ADO**記錄**的 OLE DB 物件**列**C 中的物件 /C++應用程式。  
  
 此介面支援下列屬性：  
  
## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|唯寫。<br />設定 OLE DB 的容器**資料列**物件，此 ado**記錄**物件。|  
|[Row](../../../ado/reference/ado-api/row-property-ado.md)|讀取/寫入。<br />取得/設定 OLE DB**資料列**物件，此 ado 往返**記錄**物件。|  
  
## <a name="methods"></a>方法  
 無。  
  
## <a name="events"></a>事件  
 無。  
  
## <a name="remarks"></a>備註  
 指定 OLE DB**資料列**物件 (`pRow`)，建構的 ADO**記錄**物件 (`adoR`)，相當於下列三種基本作業：  
  
1.  建立 ADO**記錄**物件：  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  查詢**IADORecordConstruction**介面上**記錄**物件：  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  呼叫**IADORecordConstruction::put_Row**屬性的方法，來設定 OLE DB**資料列**ado 物件**記錄**物件：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 結果**adoR**物件現在表示 ADO**記錄**建構從 OLE DB 物件**列**物件。  
  
 ADO**記錄**物件也可以從 OLE DB 的容器建構**資料列**物件。  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 和更新版本  
  
 **程式庫：** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
