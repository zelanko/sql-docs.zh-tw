---
title: "錯誤處理 |Microsoft 文件"
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
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8434e598deba57bf72dfdb8df1c31990113b304c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="error-handling"></a>錯誤處理
ADO 使用數種不同方法來通知發生之錯誤的應用程式。 本章節將討論當您使用 ADO 和您的應用程式接收通知的方式，可以發生之錯誤的類型。 它結束時，會發出有關如何處理這些錯誤的建議。  
  
## <a name="how-does-ado-report-errors"></a>ADO 如何報告錯誤？  
 ADO 錯誤進行通知您數種方式：  
  
-   ADO 錯誤會產生執行階段錯誤。 就像任何其他執行階段錯誤，例如使用的相同方式處理 ADO 錯誤**On Error**在 Visual Basic 中的陳述式。  
  
-   您的程式可以接收來自 OLE DB 的錯誤。 OLE DB 錯誤會產生一個執行階段錯誤。  
  
-   如果此錯誤是特定資料提供者，一或多個**錯誤**物件置於**錯誤**集合**連接**物件，用於存取資料發生錯誤時的存放區。  
  
-   如果引發事件的處理程序也會產生錯誤，錯誤資訊都會置入**錯誤**物件，並做為參數傳遞至事件。 請參閱[處理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)如需事件的詳細資訊。  
  
-   處理時所發生的問題批次更新或其他涉及的大量作業**資料錄集**可以由**狀態**屬性**資料錄集**。 例如，所指定結構描述條件約束違規或權限不足**RecordStatusEnum**值。  
  
-   發生牽涉到特定的問題**欄位**目前記錄中，也會指出由**狀態**每個屬性**欄位**中**欄位**集合**記錄**或**資料錄集**。 例如，無法完成的更新或不相容的資料類型可以指定**FieldStatusEnum**值。  
  
 此章節包含下列主題。  
  
-   [ADO 錯誤](../../../ado/guide/data/ado-errors.md)  
  
-   [提供者錯誤](../../../ado/guide/data/provider-errors.md)  
  
-   [欄位相關的錯誤資訊](../../../ado/guide/data/field-related-error-information.md)  
  
-   [資料錄集相關的錯誤資訊](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [處理其他語言的錯誤](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [預期的錯誤](../../../ado/guide/data/anticipating-errors.md)
