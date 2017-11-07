---
title: "Remove-rolemember 指令程式 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e38f56ab-facd-4bef-9502-f52f8486a6a6
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c093787d86398acaaeaca8f282e1f588c3e726d7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="remove-rolemember-cmdlet"></a>Remove-RoleMember 指令程式

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  從 Analysis Services 資料庫的指定角色中移除成員。  

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
## <a name="syntax"></a>語法  
 `Remove-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Remove-RoleMember [-DatabaseRole] <Microsoft.AnalysisServices.Role> [-MemberName] <System.String>  [<CommonParameters>]`  
  
## <a name="description"></a>說明  
 Remove-RoleMember 指令程式會從 Analysis Services 資料庫的角色中移除現有的成員。  
  
## <a name="parameters"></a>參數  
  
### <a name="-membername-string"></a>-MemberName\<字串 >  
 指定要從角色中移除的 Windows 使用者或群組。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|0|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-database-string"></a>-資料庫\<字串 >  
 指定角色所屬的資料庫。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|1|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-rolename-string"></a>-RoleName\<字串 >  
 指定您要從中移除成員的角色。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|2|  
|預設值||  
|接受管線輸入？|false|  
|接受萬用字元？|false|  
  
### <a name="-databaserole-string"></a>-DatabaseRole\<字串 >  
 指定要從中移除成員的 Microsoft.AnalysisServices.Role 物件。 當您想要經由管線提供資料庫角色時，請使用此參數當做 -Database 和 -RoleName 參數的替代項目。  
  
|||  
|-|-|  
|必要項？|true|  
|位置？|具名|  
|預設值||  
|接受管線輸入？|true (ByPropertyName)|  
|接受萬用字元？|false|  
  
### <a name="commonparameters"></a>\<一般參數 >  
 這個指令程式支援一般參數：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 如需詳細資訊，請參閱 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>輸入和輸出  
 無。  
  
## <a name="example-1"></a>範例 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 這個命令會針對在本機預設執行個體上執行的 AdventureWorks 資料庫，從 Reader 角色中移除 Windows 網域使用者帳戶。  
  
## <a name="example-2"></a>範例 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 第 1 行會將 AWTEST 資料庫的所有資料庫角色加入至管線。 第 2 行 (您在提示字元中輸入 $roles 的位置) 會顯示角色的陣列。 第 3 行會從陣列的第一個角色中移除 Windows 使用者 “adventure-works\bobh”。  
  
## <a name="example-3"></a>範例 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Remove-rolemember –membername “adventure-works\bobh”  
```  
  
 這個命令會在特定資料庫 (AWTEST) 的內容中，從陣列的第一個角色中移除 Windows 網域使用者帳戶，而這個陣列是透過列出 Roles 資料夾的子系所建立。  
  

  
  

