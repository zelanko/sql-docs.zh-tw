---
description: ADORecordConstruction 介面
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
ms.openlocfilehash: f93370ae23cd50e1fb494d484756505f69514df1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776598"
---
# <a name="adorecordconstruction-interface"></a>ADORecordConstruction 介面
**ADORecordConstruction**介面是用來從 C/c + + 應用程式中 OLE DB 的資料**列**物件來建立 ADO**記錄**物件。  
  
 此介面支援下列屬性：  
  
## <a name="properties"></a>屬性  
  
|屬性|描述|  
|-|-|  
|[ParentRow](./parentrow-property-ado.md)|唯寫。<br />設定此 ADO**記錄**物件上 OLE DB 資料**列**物件的容器。|  
|[行](./row-property-ado.md)|讀取/寫入。<br />取得/設定這個 ADO**記錄**物件的 OLE DB 資料**列**物件。|  
  
## <a name="methods"></a>方法  
 無。  
  
## <a name="events"></a>事件  
 無。  
  
## <a name="remarks"></a>備註  
 假設 OLE DB 的資料 **列** 物件 (`pRow`) ， () 的 ADO **記錄** 物件的結構 `adoR` ，就會產生下列三個基本作業的數量：  
  
1.  建立 ADO **記錄** 物件：  
  
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
  
3.  呼叫**IADORecordConstruction：:p ut_Row**屬性方法，設定 ADO **Record**物件上 OLE DB 的資料**列**物件：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 結果**adoR**物件現在代表從 OLE DB **Row**物件所建立的 ADO**記錄**物件。  
  
 您也可以從 OLE DB 資料**列**物件的容器來建立 ADO**記錄**物件。  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 和更新版本  
  
 連結**庫：** msado15.dll  
  
 **UUID：** 00000567-0000-0010-8000-00AA006D2EA4