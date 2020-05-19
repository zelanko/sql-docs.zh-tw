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
author: rothja
ms.author: jroth
ms.openlocfilehash: 12a9b2cae1c516ed3bf8caef8127034e6ff2a847
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747181"
---
# <a name="adorecordconstruction-interface"></a>ADORecordConstruction 介面
**ADORecordConstruction**介面是用來從 C/c + + 應用程式中的 OLE DB **Row**物件，來建立 ADO**記錄**物件。  
  
 此介面支援下列屬性：  
  
## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|唯寫。<br />設定此 ADO **Record**物件上 OLE DB **Row**物件的容器。|  
|[連續](../../../ado/reference/ado-api/row-property-ado.md)|讀取/寫入。<br />取得/設定此 ADO **Record**物件上/的 OLE DB 資料**列**物件。|  
  
## <a name="methods"></a>方法  
 無。  
  
## <a name="events"></a>事件  
 無。  
  
## <a name="remarks"></a>備註  
 假設有一個 OLE DB 的資料**列**物件（ `pRow` ），即 ADO **Record**物件（ `adoR` ）的結構，其數量為下列三個基本作業：  
  
1.  建立 ADO**記錄**物件：  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  查詢**記錄**物件上的**IADORecordConstruction**介面：  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  呼叫**IADORecordConstruction：:p ut_Row** property 方法，設定 ADO **Record**物件上的 OLE DB **Row**物件：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 結果**adoR**物件現在代表從 OLE DB **Row**物件所建立的 ADO**記錄**物件。  
  
 您也可以從 OLE DB **Row**物件的容器中，建立 ADO**記錄**物件。  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 和更新版本  
  
 連結**庫：** msado15.dll  
  
 **UUID：** 00000567-0000-0010-8000-00AA006D2EA4
