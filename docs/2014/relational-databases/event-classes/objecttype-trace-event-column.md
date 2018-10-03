---
title: ObjectType 追蹤事件資料行 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Object Type column values
- events [SQL Server], Object Type column values
- event classes [SQL Server], Object Type column values
- Object Type column values [SQL Server]
ms.assetid: 42f85c50-34c9-49ca-955f-af9595e2707f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 11726b01926ef5a7dff7157c901c7cbd73607564
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48214754"
---
# <a name="objecttype-trace-event-column"></a>ObjectType 追蹤事件資料行
  Object Type 追蹤事件資料行會用於各種追蹤事件。 此主題描述此資料行和其相關聯定義的可能值。  
  
## <a name="object-type-column-values"></a>Object Type 資料行值  
  
|值|定義|  
|-----------|----------------|  
|8259|檢查條件約束|  
|8260|預設 (條件約束或獨立)|  
|8262|外部索引鍵條件約束|  
|8272|預存程序|  
|8274|規則|  
|8275|系統資料表|  
|8276|伺服器的觸發程序|  
|8277|(使用者定義的) 資料表|  
|8278|檢視|  
|8280|擴充預存程序|  
|16724|CLR 觸發程序|  
|16964|[資料庫]|  
|16975|Object|  
|17222|全文檢索目錄|  
|17232|CLR 預存程序|  
|17235|結構描述|  
|17475|認證|  
|17491|DDL 事件|  
|17741|Management 事件|  
|17747|Security 事件|  
|17749|User 事件|  
|17985|CLR 彙總函式|  
|17993|內嵌資料表值 SQL 函數|  
|18000|資料分割函數|  
|18002|複寫篩選程序|  
|18004|資料表值 SQL 函數|  
|18259|伺服器角色|  
|18263|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 群組|  
|19265|非對稱金鑰|  
|19277|主要金鑰|  
|19280|主索引鍵|  
|19283|ObfusKey|  
|19521|非對稱金鑰登入|  
|19523|憑證登入|  
|19538|角色|  
|19539|SQL 登入|  
|19543|Windows 登入|  
|20034|遠端服務繫結|  
|20036|資料庫的事件通知|  
|20037|事件通知|  
|20038|純量 SQL 函數|  
|20047|物件的事件通知|  
|20051|同義字|  
|20307|序列|  
|20549|端點|  
|20801|可以快取的特定查詢|  
|20816|可以快取的準備查詢|  
|20819|Service Broker 服務佇列|  
|20821|唯一的條件約束|  
|21057|應用程式角色|  
|21059|憑證|  
|21075|[伺服器]|  
|21076|Transact-SQL 觸發程序|  
|21313|組件|  
|21318|CLR 純量函數|  
|21321|內嵌純量 SQL 函數|  
|21328|資料分割配置|  
|21333|使用者|  
|21571|Service Broker 服務合約|  
|21572|資料庫的觸發程序|  
|21574|CLR 資料表值函式|  
|21577|內部資料表 (例如，XML 節點資料表、佇列資料表。)|  
|21581|Service Broker 訊息類型|  
|21586|Service Broker 路由|  
|21587|Statistics|  
|21825<br /><br /> 21827<br /><br /> 21831<br /><br /> 21843<br /><br /> 21847|使用者|  
|22099|Service Broker 服務|  
|22601|索引|  
|22604|憑證登入|  
|22611|XMLSchema|  
|22868|類型|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
