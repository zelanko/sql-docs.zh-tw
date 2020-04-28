---
title: Microsoft OLE DB 持續性提供者（ADO 服務提供者） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2bd341a3af2d1fdb076312b4c0993184fb4fae39
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926760"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Microsoft OLE DB 持續性提供者總覽
Microsoft OLE DB 持續性提供者可讓您將[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件儲存至檔案中，並于稍後從檔案還原該**記錄集**物件。 會保留架構資訊、資料和暫止的變更。

 您可以將**記錄集**儲存為專屬的先進資料表語法（ADTG）格式或 open 可延伸標記語言 (XML) （XML）格式。

## <a name="provider-keyword"></a>Provider 關鍵字
 若要叫用此提供者，請在連接字串中指定下列關鍵字和值。

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>Errors
 在您的應用程式中，可以偵測到此提供者所發出的下列錯誤。

|持續性|描述|
|--------------|-----------------|
|E_BADSTREAM|開啟的檔案沒有有效的格式（亦即，格式不是 ADTG 或 XML）。|
|E_CANTPERSISTROWSET|儲存的**記錄集**物件具有防止儲存的特性。|

## <a name="remarks"></a>備註
 Microsoft OLE DB 持續性提供者不會公開任何動態屬性。

 目前，只有參數化的階層式**記錄集**物件無法儲存。

 如需有關持續儲存**記錄集**物件的詳細資訊，請參閱[記錄集持續](../../../ado/guide/data/more-about-recordset-persistence.md)性。

 當資料流程用來開啟**記錄集時，** 應該不會指定**Open**方法的*Source*參數以外的任何參數。

## <a name="see-also"></a>另請參閱
[Microsoft OLE DB 持續性提供者（ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
