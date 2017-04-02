---
title: "具名管道屬性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "管道 [SQL Server]"
  - "接聽 [SQL Server], 管道"
  - "管道 [SQL Server], 在管道上接聽"
  - "具名管道 [SQL Server], 在管道上接聽"
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 32
---
# 具名管道屬性
  使用具名管道通訊協定時，可使用 [具名管道內容] 對話方塊上的 [通訊協定] 頁面，來檢視或變更 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接聽的具名管道。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須重新啟動，才能啟用或停用通訊協定或變更具名管道。  
  
## 選項。  
 **Enabled**  
 可能的值為 [是] 和 [否]。  
  
 **管道名稱**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接聽的具名管道。 根據預設，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對於預設執行個體會接聽：`\\.\pipe\sql\query`，而對於具名執行個體會接聽：`\\.\pipe\MSSQL$<instancename>\sql\query`。 此欄位最長不可超過 2047 個字元。  
  
## 建立替代具名管道  
 若要變更具名管道，請在 [具名管道] 方塊中輸入新的管道名稱，然後停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，之後再重新啟動。 因為已知 **sql\query** 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的具名管道，所以變更管道有助於降低遭惡意程式攻擊的風險。  
  
### 範例  
 輸入 **\\\\.\pipe\unit\app** 以接聽 **unit\app** 管道。  
  
 輸入 **\\\\.\pipe\acct** 以接聽 **acct** 管道。  
  
## 請參閱＜  
 [啟用或停用伺服器網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [選擇網路通訊協定](../Topic/Choosing%20a%20Network%20Protocol.md)   
 [使用具名管道建立有效的連接字串](../Topic/Creating%20a%20Valid%20Connection%20String%20Using%20Named%20Pipes.md)  
  
  