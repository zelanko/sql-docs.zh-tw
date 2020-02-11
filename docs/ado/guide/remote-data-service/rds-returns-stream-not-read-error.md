---
title: RDS 傳回&quot;未讀取&quot;的資料流程錯誤 |Microsoft Docs
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
ms.openlocfilehash: c89756e86a702217d5d9d8495bf62b0d27f52321
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922479"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS 傳回&quot;未讀取&quot;的資料流程錯誤
「無法讀取資料流程物件，因為它是空的，或目前的位置在資料流程的結尾。 若為非空白資料流程，請使用 Position 屬性來設定目前的位置。 若要判斷資料流程是否為空白，請檢查 Size 屬性。」  
  
 如果您看到此錯誤訊息，表示您可能嘗試在 HTTP 上使用參數化的階層式查詢。 RDS 不允許您使用遠端參數化階層。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


