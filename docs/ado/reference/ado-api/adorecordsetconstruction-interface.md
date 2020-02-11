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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e1d14255acd4cc7f18abea1c494353ef970903c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920798"
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
 假設有一個**** OLE DB 的資料`pRowset`列集物件（），將 ADO**記錄集**物件（`adoRs`）的結構為下列三個基本作業：  
  
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
  
3.  呼叫`IADORecordsetConstruction::put_Rowset`屬性方法，以在 ADO `Rowset` `Recordset`物件上設定 OLE DB 物件：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 結果`adoRs`物件現在代表**從 OLE DB 資料列集物件**所建立的 ADO**記錄集**物件。  
  
 您也可以從 OLE DB**章節**或**RowPosition**物件中，建立 ADO**記錄集**物件。  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 和更新版本  
  
 連結**庫：** msado15.dll  
  
 **UUID：** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>另請參閱  
 [Recordset 物件（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Rowset 屬性 (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
