---
description: RDS 傳回 &quot; 資料流程未讀取 &quot; 錯誤
title: RDS 傳回 &quot; 資料流程未讀取 &quot; 錯誤 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
author: rothja
ms.author: jroth
ms.openlocfilehash: 6acb603594acdd23f8ad8764c9b9a692acabdb9b
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724899"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS 傳回 &quot; 資料流程未讀取 &quot; 錯誤
「無法讀取資料流程物件，因為它是空的，或是目前的位置在資料流程的結尾。 若是非空白的資料流程，請使用 Position 屬性來設定目前的位置。 若要判斷資料流程是否為空的，請檢查 Size 屬性。」  
  
 如果您看到此錯誤訊息，您可能已嘗試使用參數化的階層式查詢（透過 HTTP）。 RDS 不允許您使用遠端參數化階層。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](/dotnet/framework/wcf/)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](./rds-fundamentals.md)