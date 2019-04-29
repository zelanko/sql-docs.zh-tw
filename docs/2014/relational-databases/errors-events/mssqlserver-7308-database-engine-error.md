---
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3b64f55f2ce7f71a358cc202a428191d5f1998f3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62913577"
---
# <a name="mssqlserver7308"></a>MSSQLSERVER_7308
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|7308|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|RMT_STA_DISABLED|  
|訊息文字|OLE DB 提供者 '%ls' 不能用來散佈查詢，因為提供者是設定成以單一執行緒 Apartment 模式執行。|  
  
## <a name="explanation"></a>說明  
 您已經使用設定成以單一執行緒 Apartment (STA) 模式執行的 OLE DB 提供者。 以單一執行緒 Apartment (STA) 模式執行的 OLE DB 提供者無法用於分散式查詢。  
  
## <a name="user-action"></a>使用者動作  
 若要解決這個錯誤，請將提供者設定成以多執行緒 Apartment (MTA) 模式執行。 如果此提供者不支援 MTA，而且此提供者無法升級為支援 MTA 的版本，請考慮將此提供者設定為跨處理序執行。 提供者供應商應該能夠告訴您此提供者是否支援 MTA 或跨處理序執行。  
  
  
