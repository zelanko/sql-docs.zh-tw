---
title: "章屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 766166a48b1d702d9f3550d22bcb40823728c16b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="chapter-property-ado"></a>章屬性 (ADO)
取得或設定 OLE DB**章**物件上從 / [ADORecordsetConstruction 介面](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)物件。 當您使用**put_Chapter**設定**章**物件、 資料列的子集會轉換成 ADO[資料錄集物件](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 這會設定目前的章節**資料列集**物件。 這是可讀寫的屬性。  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT get_Chapter([out, retval] long* plChapter);  
HRESULT put_Chapter([in] long lChapter);  
```  
  
## <a name="parameters"></a>參數  
 *plChapter*  
 章節的控制代碼指標。  
  
 *LChapter*  
 章節控制代碼。  
  
## <a name="return-values"></a>傳回值  
 這個屬性的方法會傳回標準的 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="applies-to"></a>適用於  
 [ADORecordsetConstruction 介面](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
