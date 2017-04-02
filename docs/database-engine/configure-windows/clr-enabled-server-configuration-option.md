---
title: "CLR 已啟用伺服器組態選項 | Microsoft Docs"
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
  - "組件 [CLR 整合]，驗證可否執行"
  - "clr enabled 選項"
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
caps.latest.revision: 36
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 36
---
# CLR 已啟用伺服器組態選項
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 clr enabled 選項來指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否能執行使用者組件。 [CLR 已啟用] 選項提供下列值： 
  
|值|描述|  
|-----------|-----------------|  
|0|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上不允許組件執行。|  
|1|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上允許組件執行。|  
  
僅限 WOW64。 請重新啟動 WOW64 伺服器使設定變更生效。 對於其他伺服器類型，則不需要重新啟動。  

當您執行 RECONFIGURE 且 [CLR 已啟用] 選項的執行值從 1 變更為 0 時，會立即卸載包含使用者組件的所有應用程式定義域。  
  
>  **在輕量型共用下，不支援 Common Language Runtime (CLR) 執行：**請停用下列兩個選項的其中之一：[CLR 已啟用] 或 [輕量型共用]。 依賴 CLR 而且在 Fiber 模式下無法正常運作的功能包括了**階層**資料類型、複寫和原則式管理。  
  
## 範例  
 以下範例會先顯示使用 clr 已啟用選項的目前設定，然後將選項值設定為 1 來啟用選項。 若要停用此選項，請將值設定為 0。  
  
```tsql  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;    
```  
  
## 另請參閱  
 [輕量型共用伺服器組態選項](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [輕量型共用伺服器組態選項](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
  