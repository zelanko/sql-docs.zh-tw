---
title: "Microsoft OLE DB 持續性提供者 （ADO 服務提供者） |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8bcde7e61f7d49107cad0af77175778e66e828bf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Microsoft OLE DB 持續性提供者概觀
Microsoft OLE DB 持續性提供者可讓您儲存[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件到檔案，並稍後還原，**資料錄集**檔案中的物件。 結構描述資訊、 資料，並且保留暫止的變更。

 您可以將儲存**資料錄集**專屬的進階資料表格字母組 (ADTG) 格式，或開啟的可延伸標記語言 (XML) 格式。

## <a name="provider-keyword"></a>提供者關鍵字
 要叫用此提供者，指定連接字串中的下列關鍵字和值。

```
"Provider=MSPersist"
```

## <a name="errors"></a>錯誤
 可以在應用程式中偵測到此提供者所發出的下列錯誤。

|常數|Description|
|--------------|-----------------|
|E_BADSTREAM|開啟這個檔案沒有有效的格式 （也就是格式不 ADTG 或 XML）。|
|E_CANTPERSISTROWSET|**資料錄集**儲存物件具有防止它所儲存的特性。|

## <a name="remarks"></a>備註
 Microsoft OLE DB 持續性提供者會公開任何動態屬性。

 目前，只有參數化的階層式**資料錄集**無法儲存物件。

 如需有關持續儲存**資料錄集**物件，請參閱[資料錄集持續性](../../../ado/guide/data/more-about-recordset-persistence.md)。

 當資料流用來開啟**資料錄集，**不應該指定以外的任何參數*來源*參數**開啟**方法。

## <a name="see-also"></a>請參閱＜
[Microsoft OLE DB 持續性提供者 （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
