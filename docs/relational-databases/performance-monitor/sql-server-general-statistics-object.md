---
title: SQL Server 的 General Statistics 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:General Statistics
- General Statistics object
ms.assetid: c738e549-d7e7-4211-9ec3-064ac140af7c
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 5d835a317f2968775f0cc94df19866c0d083d69d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093518"
---
# <a name="sql-server-general-statistics-object"></a>SQL Server 的 General Statistics 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **的** SQLServer:General Statistics [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件提供計數器來監視整個伺服器範圍的一般活動，例如目前的連接數目，以及每秒與執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之電腦連接與中斷連接的使用者數目。 當您處理大型線上交易處理 (OLTP) 類型的系統時，這類系統中有許多用戶端會與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體連接與中斷連接，這時就會相當有用。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **General Statistics** 計數器。  
  
|SQL Server 的 General Statistics 計數器|Description|  
|--------------------------------------------|-----------------|  
|**Active Temp Tables**|使用中的暫存資料表數目/資料表變數數目。|  
|**Connection resets/sec**|從連接集區啟動的登入總數。|  
|**Event Notifications Delayed Drop**|等待系統執行緒卸除的事件通知數目。|  
|**HTTP Authenticated Requests**|每秒啟動的經驗證 HTTP 要求數目。|  
|**Logical Connections**|系統的邏輯連接數目。<br /><br /> 邏輯連接的主要用途是服務 Multiple Active Result Sets (MARS) 要求。 針對 MARS 要求，每次當應用程式建立連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，可能會有一個以上的邏輯連接對應至該實體連接。<br /><br /> 若不使用 MARS，則實體連接與邏輯連接的比率為 1:1。 因此，每次有應用程式建立連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，邏輯連接數目就會遞增 1。|  
|**Logins/sec**|每秒啟動登入總數。 這不包括共用連接。|  
|**Logouts/sec**|每秒啟動的登出總數。|  
|**Mars Deadlocks**|偵測到的 MARS 死結數目。|  
|**Non-atomic yield rate**|每秒非不可部分完成的產生數目。|  
|**Processes blocked**|目前已封鎖的處理序數目。|  
|**SOAP Empty Requests**|每秒啟動的空白 SOAP 要求數目。|  
|**SOAP Method Invocations**|每秒啟動的 SOAP 方法引動過程數目。|  
|**SOAP Session Initiate Requests**|每秒啟動的 SOAP 工作階段初始化要求數目。|  
|**SOAP Session Terminate Requests**|每秒啟動的 SOAP 工作階段結束要求數目。|  
|**SOAP SQL Requests**|每秒啟動的 SOAP SQL 要求數目。|  
|**SOAP WSDL Requests**|每秒啟動的 SOAP Web 服務描述語言要求數目。|  
|**SQL Trace IO Provider Lock Waits**|檔案 IO 提供者之每秒鎖定等候的數目。| 
|**Temp Tables Creation Rate**|每秒建立的暫存資料表數目/資料表變數數目。|  
|**Temp Tables For Destruction**|等候清除系統執行緒終結的暫存資料表數目/資料表變數數目。|  
|**Tempdb recovery unit id**|產生的重複 Tempdb 復原單位識別碼的數目。|
|**Tempdb rowset id**|產生的重複 tempdb 列集識別碼的數目。| 
|**Trace Event Notifications Queue**|在內部佇列中等候透過 Service Broker 傳送的追蹤事件通知執行個體數目。|  
|**交易**|交易編列數目 (結合本機、DTC、繫結)。|  
|**User Connections**|計算目前已連線到 SQL Server 的使用者數目。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
