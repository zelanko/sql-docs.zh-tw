---
title: "指定 SQL Server PowerShell 提供者中的執行個體 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9373de68-fd43-45f2-b9a6-149c96610aeb
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# 指定 SQL Server PowerShell 提供者中的執行個體
  針對 SQL Server PowerShell 提供者指定的路徑必須識別 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體及其執行所在的電腦。 用來指定電腦和執行個體的語法必須符合 SQL Server 識別碼和 Windows PowerShell 路徑的規則。  
  
1.  **開始之前：**  [限制事項](#LimitationsRestrictions)  
  
2.  **若要指定執行個體：**  [範例](#Examples)  
  
## 開始之前  
 SQL Server 提供者路徑中接在 SQLSERVER:\SQL 後面的第一個節點是執行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體的電腦名稱。例如：  
  
```  
SQLSERVER:\SQL\MyComputer  
```  
  
 如果您在與 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體相同的電腦上執行 Windows PowerShell，就可以使用 localhost 或 (local) 來取代電腦的名稱。 使用 localhost 或 (local) 的指令碼可以在任何電腦上執行，而不需要變更成反映不同的電腦名稱。  
  
 您可以在相同電腦上執行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 可執行程式的多個執行個體。 SQL Server 提供者路徑中接在電腦名稱後面的節點可識別執行個體。例如：  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance  
```  
  
 每一部電腦都只能有一個預設 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體。 當您安裝預設執行個體時，未指定它的名稱。 如果您在連接字串中只有指定電腦名稱，您會連接到該電腦上的預設執行個體。 此電腦上的所有其他執行個體都必須是具名執行個體。 您可在安裝期間指定執行個體名稱，而且連接字串必須指定電腦名稱和執行個體名稱。  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
 您無法使用句號 (.)，在 PowerShell 指令碼中指定本機電腦。 因為句號會被 PowerShell 解譯成命令，所以不支援句號。  
  
 (local) 中的括號字元通常會被 Windows PowerShell 視為命令。 您必須將其編碼或逸出以在路徑中使用，或使用雙引號括住路徑。 如需詳細資訊，請參閱＜編碼及解碼 SQL Server 識別碼＞。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供者會要求您一定要指定執行個體名稱。 如果是預設執行個體，您必須指定執行個體名稱 DEFAULT。  
  
##  <a name="Examples"></a> 範例：電腦和執行個體名稱  
 此範例使用 localhost 和 DEFAULT 指定本機電腦上的預設執行個體：  
  
```  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT   
```  
  
 (local) 中的括號字元通常會被 Windows PowerShell 視為命令。 因此，您必須：  
  
-   使用引號括住路徑字串：  
  
    ```  
    Set-Location "SQLSERVER:\SQL\(local)\DEFAULT"  
    ```  
  
-   使用反勾號字元 (`) 來逸出括號：  
  
    ```  
    Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
    ```  
  
-   使用十六進位表示法來編碼括號：  
  
    ```  
    Set-Location SQLSERVER:\SQL\%28local%29\DEFAULT  
    ```  
  
## 另請參閱  
 [PowerShell 中的 SQL Server 識別碼](../../relational-databases/scripting/sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell 提供者](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  