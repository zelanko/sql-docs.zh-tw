---
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49f67200d7489bf90102325cf3463b5ea58424f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver7308"></a>MSSQLSERVER_7308
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
