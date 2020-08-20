---
description: ADO 中的錯誤處理
title: 錯誤處理 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
author: rothja
ms.author: jroth
ms.openlocfilehash: d26cbadd4f9c6a33c6dc43a6dcc88e0a92f23d65
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453440"
---
# <a name="error-handling-in-ado"></a>ADO 中的錯誤處理
ADO 使用數種不同的方法來通知應用程式發生錯誤。 本節將討論當您使用 ADO 時可能發生的錯誤類型，以及您的應用程式如何獲得通知。 它最後會提出有關如何處理這些錯誤的建議。  
  
## <a name="how-does-ado-report-errors"></a>ADO 如何報告錯誤？  
 ADO 會以數種方式通知您錯誤：  
  
-   ADO 錯誤會產生執行階段錯誤。 以您處理任何其他執行階段錯誤的相同方式來處理 ADO 錯誤，例如在 Visual Basic 中使用 **On error** 語句。  
  
-   您的程式可能會收到 OLE DB 的錯誤。 OLE DB 錯誤也會產生執行階段錯誤。  
  
-   如果錯誤是您的資料提供者所特有，則會在發生錯誤時，將一個或多個**錯誤**物件放在用來存取資料存放區之**連接**物件的**Errors**集合中。  
  
-   如果引發事件的進程也產生錯誤，則會將錯誤資訊放在 **error** 物件中，並以參數的形式傳遞給事件。 如需事件的詳細資訊，請參閱 [處理 ADO 事件](../../../ado/guide/data/handling-ado-events.md) 。  
  
-   處理批次更新或涉及**記錄集**的其他大量作業時所發生的問題，可由**記錄集**的**Status**屬性工作表示。 例如， **RecordStatusEnum** 值可以指定架構條件約束違規或許可權不足。  
  
-   與目前記錄中特定**欄位**相關的問題，也會以**記錄**或**記錄集**之**Fields**集合中每個**欄位**的**Status**屬性來表示。 例如， **FieldStatusEnum** 值可以指定無法完成的更新或不相容的資料類型。  
  
 此章節包含下列主題。  
  
-   [ADO 錯誤](../../../ado/guide/data/ado-errors.md)  
  
-   [提供者錯誤](../../../ado/guide/data/provider-errors.md)  
  
-   [欄位相關的錯誤資訊](../../../ado/guide/data/field-related-error-information.md)  
  
-   [資料錄集相關的錯誤資訊](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [處理其他語言的錯誤](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [預期的錯誤](../../../ado/guide/data/anticipating-errors.md)
