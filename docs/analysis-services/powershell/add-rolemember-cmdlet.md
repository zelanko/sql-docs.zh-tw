---
title: "Add-RoleMember 指令程式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 827c8bbc-d48f-4e49-9ea5-abb1380f7623
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 14
---
# Add-RoleMember 指令程式
  將成員加入至指定之 Analysis Services 表格式或多維資料庫的角色。  
  
## 語法  
 `Add-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Add-RoleMember [-MemberName] <System.String> [-DatabaseRole] <Microsoft.AnalysisServices.Role> [<CommonParameters>]`  
  
## 說明  
 Add-RoleMember 指令程式會將有效的成員加入至現有的資料庫角色。 只允許使用資料庫角色。 您無法使用這個指令程式，將成員加入至伺服器角色。  
  
 您一次只能加入一個成員，這個成員可以是使用者或群組帳戶。  
  
## 參數  
  
### -MemberName \<字串>  
 指定要加入至角色的 Windows 使用者或群組。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|0|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -Database \<字串>  
 指定角色所屬的資料庫。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|1|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -RoleName \<字串>  
 指定您要加入成員的目標角色。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|2|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### -DatabaseRole \<字串>  
 指定應該加入成員的目標 Microsoft.AnalysisServices.Role 物件。 當您想要經由管線提供資料庫角色時，請使用此參數當做 -Database 和 -RoleName 參數的替代項目。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|true (ByPropertyName)|  
|接受萬用字元？|false|  
  
### \<CommonParameters>  
 這個指令程式支援一般參數：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 如需詳細資訊，請參閱 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## 輸入和輸出  
 輸入類型是可透過管道傳送至指令程式的物件類型。 傳回類型是指令程式所傳回的物件類型。  
  
|||  
|-|-|  
|輸入|無。|  
|輸出|無|  
  
## 範例 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 這個命令會針對在本機預設執行個體上執行的 AdventureWorks 資料庫，將 Windows 網域使用者帳戶加入至 Reader 角色。  
  
## 範例 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 第 1 行會將 AWTEST 資料庫的所有資料庫角色加入至管線。 第 2 行 (您在提示字元中輸入 $roles 的位置) 會顯示角色的陣列。 第 3 行會加入 Windows 使用者 adventure-works\bobh 成為陣列中第一個角色的成員。  
  
## 範例 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Add-rolemember –membername “adventure-works\bobh”  
```  
  
 這個命令會在特定資料庫 (AWTEST) 的內容中，將 Windows 網域使用者帳戶加入至陣列中的第一個角色，而這個陣列是透過列出 Roles 資料夾的子系所建立。  
  
## 請參閱＜  
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [使用 PowerShell 管理表格式模型](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  