---
title: "用戶端通訊協定 - 具名管道內容 (通訊協定索引標籤) | Microsoft Docs"
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
  - "管道 [SQL Server], 連接至"
  - "具名的管道 [SQL Server], 預設管道"
  - "用戶端通訊協定 [SQL Server]"
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 用戶端通訊協定 - 具名管道內容 (通訊協定索引標籤)
  在「 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」中，使用 **[Named Pipes 內容]** 對話方塊的 **[通訊協定]** 索引標籤來檢視或修改預設管道的描述。 若要連接到其他管道，請在 **[預設管道]** 方塊內輸入管道名稱。 如需有關連接字串的詳細資訊，請參閱＜ [Creating a Valid Connection String Using Named Pipes](../Topic/Creating%20a%20Valid%20Connection%20String%20Using%20Named%20Pipes.md)＞。  
  
## 選項。  
 **預設管道**  
 指定「具名管道網路」程式庫嘗試連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目標執行個體時要使用的預設管道。 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會接聽： `\\.\pipe\sql\query`  
  
 若要連接到預設管道，請輸入 `sql\query`  
  
 **已啟用**  
 可能的值為 [是] 和 [否]。  
  
## 請參閱＜  
 [選擇網路通訊協定](../Topic/Choosing%20a%20Network%20Protocol.md)  
  
  