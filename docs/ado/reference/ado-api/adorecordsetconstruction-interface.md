---
title: "ADORecordsetConstruction 介面 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ADORecordsetConstruction
helpviewer_keywords: ADORecordsetConstruction interface [ADO]
ms.assetid: 08386eba-f1f7-4879-8ffd-8733930ecb2f
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad2a33da2d2e54f45e765bf21b2bca018128d139
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="adorecordsetconstruction-interface"></a>ADORecordsetConstruction 介面
**ADORecordsetConstruction**介面用來建構 ADO**資料錄集**從 OLE DB 物件**資料列集**C/c + + 應用程式中的物件。  
  
 此介面支援下列屬性：  
  
## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|[本文章節](../../../ado/reference/ado-api/chapter-property-ado.md)|讀取/寫入。<br />取得/設定 OLE DB**章**物件上此 ADO/從**資料錄集**物件。|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|讀取/寫入。<br />取得/設定 OLE DB **RowPosition**物件上此 ADO/從**資料錄集**物件。|  
|[資料列集](../../../ado/reference/ado-api/rowset-property-ado.md)|讀取/寫入。<br />取得/設定 OLE DB**資料列集**物件上此 ADO/從**資料錄集**物件。|  
  
## <a name="methods"></a>方法  
 無。  
  
## <a name="events"></a>事件  
 無。  
  
## <a name="remarks"></a>備註  
 指定 OLE DB**資料列集**物件 (`pRowset`)，ADO 建構**資料錄集**物件 (`adoRs`) 於下列三個基本作業：  
  
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
  
3.  呼叫`IADORecordsetConstruction::put_Rowset`屬性方法來設定 OLE DB`Rowset`上之 ADO 物件`Recordset`物件：  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 產生`adoRs`物件現在代表 ADO**資料錄集**建構從 OLE DB 物件**資料列集**物件。  
  
 您也可以建構 ADO**資料錄集**從 OLE DB 物件**章**或**RowPosition**物件。  
  
## <a name="requirements"></a>需求  
 **版本：** ADO 2.0 和更新版本  
  
 **程式庫：** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>請參閱  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Rowset 屬性 (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
