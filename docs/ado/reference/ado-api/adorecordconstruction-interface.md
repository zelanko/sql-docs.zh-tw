---
title: ADORecordConstruction 介面 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction
helpviewer_keywords:
- ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 079bc873b78a40248d60c36e994750d4c95c076d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="adorecordconstruction-interface"></a>ADORecordConstruction 介面
**ADORecordConstruction**介面用來建構 ADO**記錄**從 OLE DB 物件**列**C/c + + 應用程式中的物件。  
  
 此介面支援下列屬性：  
  
## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|唯寫。<br />設定 OLE DB 的容器**列**上此 ADO 物件**記錄**物件。|  
|[資料列](../../../ado/reference/ado-api/row-property-ado.md)|讀取/寫入。<br />取得/設定 OLE DB**列**物件上此 ADO/從**記錄**物件。|  
  
## <a name="methods"></a>方法  
 無。  
  
## <a name="events"></a>事件  
 無。  
  
## <a name="remarks"></a>備註  
 指定 OLE DB**列**物件 (`pRow`)，ADO 建構**記錄**物件 (`adoR`)，於下列三個基本作業：  
  
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
  
3.  呼叫**IADORecordConstruction::put_Row**屬性方法來設定 OLE DB**列**上之 ADO 物件**記錄**物件：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 產生**adoR**物件現在代表 ADO**記錄**建構從 OLE DB 物件**列**物件。  
  
 ADO**記錄**物件也可以從 OLE DB 容器建構**列**物件。  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 和更新版本  
  
 **程式庫：** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
