---
title: RDS 傳回&quot;Stream Not Read&quot;錯誤 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 598326335c32f18b5d7f5a764d387e5b5ea536f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699423"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS 傳回&quot;Stream Not Read&quot;錯誤
"Stream 物件無法讀取，因為它是空的或目前位置是在 Stream 結尾。 對於非空白的資料流，設定 Position 屬性與目前的位置。 若要判斷 Stream 是否為空，檢查 [大小] 屬性。 」  
  
 如果您看到此錯誤訊息，您可能嘗試使用透過 http 的參數化的階層式查詢。 RDS 不允許您使用遠端參數化的階層。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


