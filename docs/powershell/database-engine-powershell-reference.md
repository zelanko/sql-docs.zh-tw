---
title: "資料庫引擎 PowerShell 參考 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: powershell
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3c379a43-c497-47dd-8e7d-2b015c068bb7
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dc3df1d697b05201ac48520c1e344c28648cdfaf
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="database-engine-powershell-reference"></a>資料庫引擎 PowerShell 參考
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 包含一組用以執行 [!INCLUDE[ssDE](../includes/ssde-md.md)]中常用動作的 Windows PowerShell Cmdlet。 此外，查詢運算式與統一資源名稱 (URN) 可轉換為 SQL Server PowerShell 路徑，或用以指定 [!INCLUDE[ssDE](../includes/ssde-md.md)]中的一個或多個物件。  
  
## <a name="database-engine-cmdlets"></a>Database Engine Cmdlet  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 包含相對較少的 [!INCLUDE[ssDE](../includes/ssde-md.md)]Cmdlet。 多數用於 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的 PowerShell 指令碼，皆使用 SQL Server PowerShell 提供者和管理能力物件模型。 如需詳細資訊，請參閱 [SQL Server PowerShell Provider](../relational-databases/scripting/sql-server-powershell-provider.md)。  
  
 如需了解在 Windows PowerShell 環境中取得 SQL Server Cmdlet 相關說明的方法，請參閱＜ [Get Help SQL Server PowerShell](../relational-databases/scripting/get-help-sql-server-powershell.md)＞。  
  
### <a name="in-this-section"></a>本節內容  
 本節包含了有關這些 Cmdlet 的詳細資訊。  
  
|描述|指令程式|  
|-----------------|------------|  
|執行 Runs Transact-SQL 與 XQuery 指令碼，例如可使用 **sqlcmd** 公用程式執行的指令碼。|[Invoke-Sqlcmd 指令程式](../powershell/invoke-sqlcmd-cmdlet.md)|  
|評估 Database Engine 物件是否符合原則式管理之原則。|[Invoke-PolicyEvaluation 指令程式](../powershell/invoke-policyevaluation-cmdlet.md)|  
  
### <a name="information-about-other-cmdlets"></a>其他 Cmdlet 的詳細資訊  
 **Encode-Sqlname** 和 **Decode-Sqlname** Cmdlet 可協助您指定內含 PowerShell 路徑所不支援之字元的 SQL Server 識別碼。 如需詳細資訊，請參閱 [SQL Server Identifiers in PowerShell](../relational-databases/scripting/sql-server-identifiers-in-powershell.md)。  
  
 使用 **Convert-UrnToPath** Cmdlet 將 [!INCLUDE[ssDE](../includes/ssde-md.md)] 物件的唯一資源名稱轉換為 SQL Server PowerShell 提供者的路徑。 如需詳細資訊，請參閱 [Convert URNs to SQL Server Provider Paths](../relational-databases/scripting/convert-urns-to-sql-server-provider-paths.md)。  
  
## <a name="query-expressions-and-unique-resource-names"></a>查詢運算式和唯一的資源名稱  
 查詢運算式是使用類似 XPath 語法的一些字串，可用以指定在物件模型階層中列舉一個或多個物件的準則集合。 唯一的資源名稱 (URN) 是可唯一識別單一物件的特定查詢運算式字串類型。 如需詳細資訊，請參閱 [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)  
  
  

