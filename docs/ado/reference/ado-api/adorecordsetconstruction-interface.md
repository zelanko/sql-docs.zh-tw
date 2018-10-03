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
manager: craigg
ms.openlocfilehash: 078b48c36d0ee2a1b3f368b8e6baf7346ed343fa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47634386"
---
# <a name="adorecordsetconstruction-interface"></a>ADORecordsetConstruction 介面
**ADORecordsetConstruction**介面用來建構 ADO **Recordset**的 OLE DB 物件**資料列集**C/c + + 應用程式中的物件。  
  
 此介面支援下列屬性：  
  
## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|[章節](../../../ado/reference/ado-api/chapter-property-ado.md)|讀取/寫入。<br />取得/設定 OLE DB**一章**物件，此 ado 往返**資料錄集**物件。|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|讀取/寫入。<br />取得/設定 OLE DB **RowPosition**物件，此 ado 往返**資料錄集**物件。|  
|[Rowset](../../../ado/reference/ado-api/rowset-property-ado.md)|讀取/寫入。<br />取得/設定 OLE DB**資料列集**物件，此 ado 往返**資料錄集**物件。|  
  
## <a name="methods"></a>方法  
 無。  
  
## <a name="events"></a>事件  
 無。  
  
## <a name="remarks"></a>備註  
 指定 OLE DB**資料列集**物件 (`pRowset`)，建構的 ADO**資料錄集**物件 (`adoRs`) 相當於下列三種基本作業：  
  
1.  建立 ADO**資料錄集**物件：  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  查詢**IADORecordsetConstruction**介面上**資料錄集**物件：  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  呼叫`IADORecordsetConstruction::put_Rowset`屬性的方法，來設定 OLE DB `Rowset` ado 物件`Recordset`物件：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 結果`adoRs`物件現在表示 ADO **Recordset**建構從 OLE DB 物件**資料列集**物件。  
  
 您也可以建構 ADO **Recordset** OLE DB 物件**章**或**RowPosition**物件。  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 和更新版本  
  
 **程式庫：** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>另請參閱  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Rowset 屬性 (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
