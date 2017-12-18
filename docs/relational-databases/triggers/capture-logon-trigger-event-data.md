---
title: "擷取登入觸發程序事件資料 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: triggers
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e05b1ab4-c10b-402a-9591-f6ec1e3db8c0
caps.latest.revision: "5"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f416a2ce4e59d9d097348fb601825867df10d7b4
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="capture-logon-trigger-event-data"></a>擷取登入觸發程序事件資料
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)] 若要擷取有關 LOGON 事件的 XML 資料，以用於登入觸發程序內部，請使用 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md) 函式。 LOGON 事件會傳回下列事件資料結構描述：  
  
 `<EVENT_INSTANCE>`  
  
 `<EventType>event_type</EventType>`  
  
 `<PostTime>post_time</PostTime>`  
  
 `<SPID>spid</SPID>`  
  
 `<ServerName>server_name</ServerName>`  
  
 `<LoginName>login_name</LoginName>`  
  
 `<LoginType>login_type</LoginType>`  
  
 `<SID>sid</SID>`  
  
 `<ClientHost>client_host</ClientHost>`  
  
 `<IsPooled>is_pooled</IsPooled>`  
  
 `</EVENT_INSTANCE>`  
  
 `<EventType>`  
 包含 `LOGON`。  
  
 `<PostTime>`  
 包含要求建立工作階段的時間。  
  
 `<SID>`  
 包含所指定登入名稱的安全識別碼 (SID) 之 Base 64 編碼二進位資料流。  
  
 `<ClientHost>`  
 包含建立連接的來源用戶端之主機名稱。 如果用戶端和伺服器名稱相同，這個值會是 '`<local_machine>`'。 否則會是用戶端的 IP 位址。  
  
 `<IsPooled>`  
 如果是利用連接共用來重複使用連接，這會是 `1` 。 否則，這個值便為 `0`。  
  
  
