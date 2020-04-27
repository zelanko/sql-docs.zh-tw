---
title: 資料庫引擎 PowerShell 參考 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3c379a43-c497-47dd-8e7d-2b015c068bb7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ed2e407b724f57d6ded518b864e3b1d78b4c489e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66064971"
---
# <a name="database-engine-powershell-reference"></a>資料庫引擎 PowerShell 參考
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 包含一組用以執行 [!INCLUDE[ssDE](../includes/ssde-md.md)] 中常用動作的 Windows PowerShell 2.0 Cmdlet。 此外，查詢運算式與統一資源名稱 (URN) 可轉換為 SQL Server PowerShell 路徑，或用以指定 [!INCLUDE[ssDE](../includes/ssde-md.md)]中的一個或多個物件。  
  
## <a name="database-engine-cmdlets"></a>Database Engine Cmdlet  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 包含相對較少的 [!INCLUDE[ssDE](../includes/ssde-md.md)]Cmdlet。 多數用於 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的 PowerShell 指令碼，皆使用 SQL Server PowerShell 提供者和管理能力物件模型。 如需詳細資訊，請參閱 [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md)。  
  
 如需了解在 Windows PowerShell 環境中取得 SQL Server Cmdlet 相關說明的方法，請參閱＜ [Get Help SQL Server PowerShell](../powershell/sql-server-powershell.md)＞。  
  
### <a name="in-this-section"></a>本節內容  
 本節包含了有關這些 Cmdlet 的詳細資訊。  
  
|描述|Cmdlet|  
|-----------------|------------|  
|執行 Runs Transact-SQL 與 XQuery 指令碼，例如可使用 `sqlcmd` 公用程式執行的指令碼。|[Invoke-Sqlcmd 指令程式](../../2014/database-engine/invoke-sqlcmd-cmdlet.md)|  
|評估 Database Engine 物件是否符合原則式管理之原則。|[Invoke-PolicyEvaluation 指令程式](../../2014/database-engine/invoke-policyevaluation-cmdlet.md)|  
  
### <a name="information-about-other-cmdlets"></a>其他 Cmdlet 的詳細資訊  
 `Encode-Sqlname` 與 `Decode-Sqlname` Cmdlet 可協助您指定內含 PowerShell 路徑所不支援之字元的 SQL Server 識別碼。 如需詳細資訊，請參閱 [SQL Server Identifiers in PowerShell](../powershell/sql-server-identifiers-in-powershell.md)。  
  
 使用 `Convert-UrnToPath` Cmdlet 將 [!INCLUDE[ssDE](../includes/ssde-md.md)] 物件的唯一資源名稱轉換為 SQL Server PowerShell 提供者的路徑。 如需詳細資訊，請參閱 [Convert URNs to SQL Server Provider Paths](../../2014/database-engine/convert-urns-to-sql-server-provider-paths.md)。  
  
## <a name="query-expressions-and-unique-resource-names"></a>查詢運算式和唯一的資源名稱  
 查詢運算式是使用類似 XPath 語法的一些字串，可用以指定在物件模型階層中列舉一個或多個物件的準則集合。 唯一的資源名稱 (URN) 是可唯一識別單一物件的特定查詢運算式字串類型。 如需詳細資訊，請參閱 [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
