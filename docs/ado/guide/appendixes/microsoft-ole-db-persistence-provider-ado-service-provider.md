---
description: 'Microsoft OLE DB 持續性提供者 (ADO 服務提供者) '
title: Microsoft OLE DB 持續性提供者 (ADO 服務提供者) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB persistence provider
- persistence provider [ADO]
- OLE DB persistence provider [ADO]
ms.assetid: e75ef0dc-2016-4fcc-8918-23311c0d4e02
author: rothja
ms.author: jroth
ms.openlocfilehash: fe50ef2d018f01e0811c5d950f73ae6cb3d3c5f3
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/17/2020
ms.locfileid: "97638057"
---
# <a name="microsoft-ole-db-persistence-provider-overview"></a>Microsoft OLE DB 持續性提供者總覽
Microsoft OLE DB 持續性提供者可讓您將 [記錄集](../../reference/ado-api/recordset-object-ado.md) 物件儲存至檔案中，並在稍後從檔案還原該 **記錄集** 物件。 系統會保留架構資訊、資料和暫止的變更。

 您可以將 **記錄集** 儲存在專屬的 Advanced Table 資料表中， (ADTG) 格式或 open 可延伸標記語言 (XML)  (XML) 格式。

## <a name="provider-keyword"></a>Provider 關鍵字
 若要叫用這個提供者，請在連接字串中指定下列關鍵字和值。

```vb
"Provider=MSPersist"
```

## <a name="errors"></a>Errors
 您可以在應用程式中偵測到此提供者所發出的下列錯誤。

|常數|描述|
|--------------|-----------------|
|E_BADSTREAM|開啟的檔案沒有有效的格式 (也就是說，格式不是 ADTG 或 XML) 。|
|E_CANTPERSISTROWSET|儲存的 **記錄集** 物件具有阻礙儲存的特性。|

## <a name="remarks"></a>備註
 Microsoft OLE DB 持續性提供者不會公開任何動態屬性。

 目前，只能儲存參數化階層式 **記錄集** 物件。

 如需持續儲存 **記錄集** 物件的詳細資訊，請參閱 [記錄集持續](../data/more-about-recordset-persistence.md)性。

 當資料流程用來開啟 **記錄集時，** 不應該指定 **Open** 方法的 *Source* 參數以外的任何參數。
