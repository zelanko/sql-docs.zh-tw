---
title: MSSQLSERVER_33028 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 33028 (Database Engine error)
ms.assetid: c5cec0e4-0bcd-4907-826f-e7d835cfcb37
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ccf8eeb5d9c91e1f8ec8cec3c46edf66409bbc5a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023991"
---
# <a name="mssqlserver33028"></a>MSSQLSERVER_33028
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|33028|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SEC_CRYPTOPROV_CANTOPENSESSION|  
|訊息文字|無法為 %S_MSG '%.*ls' 開啟工作階段。 提供者錯誤碼: %d。|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法開啟錯誤訊息中所列的密碼編譯提供者。 此密碼編譯提供者提供了所列的錯誤碼。 如需有關此錯誤的詳細資訊，您可能必須連絡密碼編譯提供者。  
  
|錯誤碼|描述|  
|----------------|-----------------|  
|0|成功。 沒有錯誤。|  
|@shouldalert|失敗。 發生未指定或意外的錯誤。 沒有其他資訊可用。|  
|2|緩衝區不足。 無法針對密碼編譯提供者配置空間。|  
|3|不支援。 這個版本不支援此密碼編譯提供者。 請選取另一個密碼編譯提供者。|  
|4|找不到。 指定的密碼編譯提供者不存在，或者您沒有存取這些檔案的授權。|  
|5|授權失敗。 可能是因為在建立認證時提供了不正確的密碼或使用者名稱。 如果此認證不存在，也可能會造成這種情況。|  
|6|無效的引數。 將無效的引數傳遞給密碼編譯提供者。|  
  
## <a name="user-action"></a>使用者動作  
 解決此錯誤，或者連絡密碼編譯提供者以了解詳細資訊。  
  
  