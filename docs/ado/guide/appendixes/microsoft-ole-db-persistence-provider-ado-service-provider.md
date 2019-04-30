---
title: Microsoft OLE DB 持續性提供者 （ADO 服務提供者） |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 2550e36f977be13e10865d4bd238c8508c542091
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128512"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Microsoft OLE DB 持續性提供者概觀
Microsoft OLE DB 持續性提供者可讓您儲存[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)物件到檔案，並稍後再還原，**資料錄集**檔案中的物件。 結構描述資訊及資料，而且會保留暫止的變更。

 您可以節省**資料錄集**專屬的進階資料表格字母組 (ADTG) 格式，或開啟的可延伸標記語言 (XML) 格式。

## <a name="provider-keyword"></a>提供者關鍵字
 若要叫用此提供者，請指定下列關鍵字和值的連接字串中。

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>錯誤
 在您的應用程式，可以偵測此提供者所簽發的下列錯誤。

|常數|描述|
|--------------|-----------------|
|E_BADSTREAM|開啟這個檔案沒有有效的格式 （也就是格式不是 ADTG 或 XML）。|
|E_CANTPERSISTROWSET|**資料錄集**儲存的物件具有防止儲存的特性。|

## <a name="remarks"></a>備註
 Microsoft OLE DB 持續性提供者會公開任何動態屬性。

 目前，只有參數化階層**資料錄集**無法儲存物件。

 如需詳細資訊，持續儲存的相關**Recordset**物件，請參閱[資料錄集的持續性](../../../ado/guide/data/more-about-recordset-persistence.md)。

 當資料流用來開啟**資料錄集，** 應該會有未指定以外的其他參數*來源*參數**開啟**方法。

## <a name="see-also"></a>另請參閱
[Microsoft OLE DB 持續性提供者 （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)
