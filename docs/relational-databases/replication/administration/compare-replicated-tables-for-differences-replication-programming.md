---
title: "比較複寫資料表的差異 (複寫程式設計) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "tablediff 公用程式"
  - "比較複寫資料表"
ms.assetid: cd253a17-0c85-42b4-912c-690169ebe799
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 比較複寫資料表的差異 (複寫程式設計)
  發行項驗證可用來判斷「發行者」和「訂閱者」端資料表發行項的發行資料是否互異，若有則可能代表無法聚合。 如需詳細資訊，請參閱 [驗證複寫資料](../../../relational-databases/replication/validate-replicated-data.md)。 不過，驗證只會傳回通過或失敗資訊，而不會針對來源及目的地資料表之間的差異提供任何相關資訊。  **Tablediff** 命令提示字元公用程式會傳回詳細資訊，兩個資料表之間的差異和甚至可能產生 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼，在 「 發行者 」 將訂閱的資料聚合。  
  
> [!NOTE]  
>   **Tablediff** 公用程式才支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 伺服器。  
  
### 若要使用 tablediff 比較複寫資料表的差異  
  
1.  從命令提示中複寫拓撲中的任何伺服器上，執行 [tablediff 公用程式](../../../tools/tablediff-utility.md)。 指定下列參數：  
  
    -   **-sourceserver** -所在資料已知為正確的通常是 「 發行者 」 的伺服器名稱。  
  
    -   **-sourcedatabase** -包含正確的資料之資料庫的名稱。  
  
    -   **-sourcetable** -所比較發行項的來源資料表的名稱。  
  
    -   （選擇性） **-sourceschema** -來源資料表中，如果不是預設的結構描述的結構描述擁有者。  
  
    -   （選擇性） **-sourceuser** 和 **-sourcepassword** 使用 SQL Server 驗證連接到 「 發行者 」 時。  
  
        > [!IMPORTANT]  
        >  盡可能使用 Windows 驗證。 如果必須使用「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證」，請提示使用者在執行階段輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
    -   **-destinationserver** -所比較的資料，通常是 「 訂閱者 」 的伺服器名稱。  
  
    -   **-destinationdatabase** -名稱進行比較的資料庫。  
  
    -   **-destinationtable** -所比較之資料表的名稱。  
  
    -   （選擇性） **-destinationschema** -目的地資料表中，如果不是預設的結構描述的結構描述擁有者。  
  
    -   （選擇性） **-使用 「** 和 **-destinationuser** 時使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證來連接到訂閱者。  
  
        > [!IMPORTANT]  
        >  盡可能使用 Windows 驗證。 如果必須使用「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證」，請提示使用者在執行階段輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
    -   （選擇性）使用 **-c** 來執行資料行層級比較。  
  
    -   （選擇性）使用 **-q** 若要執行快速，資料列計數-和-僅限結構描述比較。  
  
    -   （選擇性）指定檔案名稱和路徑 **-o** 來輸出結果到檔案。  
  
    -   （選擇性）指定在訂閱資料庫，其中插入結果 **-et**。 如果資料表已存在，指定 **-dt** 先卸除資料表。  
  
    -   （選擇性）使用 **-f** 產生 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 檔案，以修正 「 訂閱者 」 的資料，使其符合發行者端的資料。 使用 **-df** 以指定的數目 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 每個檔案中的陳述式。  
  
    -   （選擇性）使用 **-rc** 和 **-ri** 指定的作業，但重試間隔重試的次數。  
  
    -   （選擇性）使用 **-strict** 來強制執行嚴格的結構描述比較來源和目的地資料表。  
  
## 另請參閱  
 [驗證訂閱者端的資料](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  