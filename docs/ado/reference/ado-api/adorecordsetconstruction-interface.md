---
description: ADORecordsetConstruction 介面
title: ADORecordsetConstruction 介面 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction
helpviewer_keywords:
- ADORecordsetConstruction interface [ADO]
ms.assetid: 08386eba-f1f7-4879-8ffd-8733930ecb2f
author: rothja
ms.author: jroth
ms.openlocfilehash: ecf8f8e12f8d12a3382e7b67b13e8bb12fb69ac9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976219"
---
# <a name="adorecordsetconstruction-interface"></a>ADORecordsetConstruction 介面
**ADORecordsetConstruction**介面是用來從 C/c + + 應用程式中**的 OLE DB 資料列集物件**來建立 ADO**記錄集**物件。  
  
 此介面支援下列屬性：  
  
## <a name="properties"></a>屬性  
  
|屬性|描述|  
|-|-|  
|[章節](./chapter-property-ado.md)|讀取/寫入。<br />取得/設定這個 ADO**記錄集**物件的 OLE DB**章節**物件。|  
|[RowPosition](./rowposition-property-ado.md)|讀取/寫入。<br />取得/設定這個 ADO**記錄集**物件上的 OLE DB **RowPosition**物件。|  
|[資料列集](./rowset-property-ado.md)|讀取/寫入。<br />取得/設定此 ADO**記錄集**物件上**的 OLE DB 資料列集物件**。|  
  
## <a name="methods"></a>方法  
 無。  
  
## <a name="events"></a>事件  
 無。  
  
## <a name="remarks"></a>備註  
 假設有 OLE DB 的資料 **列集物件** (`pRowset`) ，則 ADO **記錄集** 物件的結構 (`adoRs`) 為下列三個基本作業：  
  
1.  建立 ADO **記錄集** 物件：  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  查詢**記錄集**物件上的**IADORecordsetConstruction**介面：  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  呼叫 `IADORecordsetConstruction::put_Rowset` property 方法以設定 `Rowset` ADO 物件上的 OLE DB 物件 `Recordset` ：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 結果 `adoRs` 物件現在代表從 OLE DB 資料**列集**物件所建立的 ADO**記錄集**物件。  
  
 您也可以從 OLE DB**章節**或**RowPosition**物件來建立 ADO**記錄集**物件。  
  
## <a name="requirements"></a>規格需求  
 **版本：** ADO 2.0 和更新版本  
  
 連結**庫：** msado15.dll  
  
 **UUID：** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的記錄集物件 ](./recordset-object-ado.md)   
 [Rowset 屬性 (ADO)](./rowset-property-ado.md)