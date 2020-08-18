---
description: Server Memory Change 事件類別
title: Server Memory Change 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Server Memory Change event class
ms.assetid: c9836484-39c5-4a89-b080-3567783b6fff
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 86f8e8a10a7207b75419a14b5b575a57297d9d81
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88329935"
---
# <a name="server-memory-change-event-class"></a>Server Memory Change 事件類別
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  當 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體使用量增加或減少 1 MB 或最大伺服器記憶體的 5% (以較大者為主)，就會發生 **Server Memory Change** 事件類別。  
  
## <a name="server-memory-change-event-class-data-columns"></a>Server Memory Change 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|是|  
|----------------------|---------------|-----------------|---------------|---------|  
|**EventClass**|**int**|事件類型 = 81。|27|否|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**EventSubClass**|**int**|事件子類別的類型。<br /><br /> 1=增加記憶體<br /><br /> 2=減少記憶體|21|是|  
|**IntegerData**|**int**|新的記憶體大小 (以 MB 表示)。|25|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**RequestID**|**int**|包含陳述式之要求的識別碼。|49|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**nvarchar**|引發工作階段的使用者登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
|**XactSequence**|**bigint**|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
