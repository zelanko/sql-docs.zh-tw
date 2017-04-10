---
title: "伺服器觸發程序遞迴伺服器組態選項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "遞迴觸發程序 [SQL Server]"
  - "觸發程序 [SQL Server], 遞迴"
  - "Server trigger recursion 選項"
ms.assetid: da4c25f5-d04c-4951-a3db-409e71a1b468
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# 伺服器觸發程序遞迴伺服器組態選項
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 [伺服器觸發程序遞迴] 選項，可指定是否允許伺服器層級的觸發程序以遞迴方式引發。 如果此選項設成 1 (ON)，則允許伺服器層級的觸發程序以遞迴方式引發。 若設成 0 (OFF)，則伺服器層級的觸發程序無法以遞迴方式引發。 當 server trigger recursion 選項設為 0 (OFF)，只能阻止直接遞迴。 (若要停用間接遞迴，請將 [巢狀觸發程序] 選項設定為 0)。這個選項的預設值是 1 (ON)。 伺服器不需重新啟動，設定即可立刻生效。  
  
 如需相關資訊，請參閱[建立巢狀觸發程序](../../relational-databases/triggers/create-nested-triggers.md)。  
  
## 另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  