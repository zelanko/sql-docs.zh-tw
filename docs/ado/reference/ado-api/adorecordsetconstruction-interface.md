---
title: ADORecordsetConstruction 介面 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 770bf86f62f243ea255693c7773e6fae48527cfd
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747090"
---
# <a name="adorecordsetconstruction-interface"></a>ADORecordsetConstruction 介面
**ADORecordsetConstruction**介面是用來從 C/c + + 應用程式中的 OLE DB 資料列**集**物件，來建立 ADO**記錄集**物件。  
  
 此介面支援下列屬性：  
  
## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|[章節](../../../ado/reference/ado-api/chapter-property-ado.md)|讀取/寫入。<br />取得/設定此 ADO**記錄集**物件上/的 OLE DB**章節**物件。|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|讀取/寫入。<br />取得/設定此 ADO**記錄集**物件上/的 OLE DB **RowPosition**物件。|  
|[資料列集](../../../ado/reference/ado-api/rowset-property-ado.md)|讀取/寫入。<br />取得/設定此 ADO**記錄集**物件上/的 OLE DB 資料列**集**物件。|  
  
## <a name="methods"></a>方法  
 無。  
  
## <a name="events"></a>事件  
 無。  
  
## <a name="remarks"></a>備註  
 假設有一個 OLE DB 的資料列**集**物件（ `pRowset` ），將 ADO**記錄集**物件（）的結構 `adoRs` 為下列三個基本作業：  
  
1.  建立 ADO**記錄集**物件：  
  
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
  
3.  呼叫 `IADORecordsetConstruction::put_Rowset` 屬性方法，以 `Rowset` 在 ADO 物件上設定 OLE DB 物件 `Recordset` ：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 結果 `adoRs` 物件現在代表從 OLE DB 資料**列集**物件所建立的 ADO**記錄集**物件。  
  
 您也可以從 OLE DB**章節**或**RowPosition**物件中，建立 ADO**記錄集**物件。  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 和更新版本  
  
 連結**庫：** msado15.dll  
  
 **UUID：** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>另請參閱  
 [Recordset 物件（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Rowset 屬性 (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
