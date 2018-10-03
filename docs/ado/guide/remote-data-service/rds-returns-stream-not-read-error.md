---
title: RDS 傳回&quot;Stream Not Read&quot;錯誤 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc2944e213e2a6a8ba3f9dc51a9a23b496f4e31a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47613916"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS 傳回&quot;Stream Not Read&quot;錯誤
"Stream 物件無法讀取，因為它是空的或目前位置是在 Stream 結尾。 對於非空白的資料流，設定 Position 屬性與目前的位置。 若要判斷 Stream 是否為空，檢查 [大小] 屬性。 」  
  
 如果您看到此錯誤訊息，您可能嘗試使用透過 http 的參數化的階層式查詢。 RDS 不允許您使用遠端參數化的階層。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


