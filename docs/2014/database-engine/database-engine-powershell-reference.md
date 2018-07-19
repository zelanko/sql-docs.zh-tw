---
title: 資料庫引擎 PowerShell 參考 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3c379a43-c497-47dd-8e7d-2b015c068bb7
caps.latest.revision: 7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 17424e5a629a4161760c35d5dcc24b80aaf9c2bd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37205838"
---
# <a name="database-engine-powershell-reference"></a>資料庫引擎 PowerShell 參考
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 包含一組用以執行 [!INCLUDE[ssDE](../includes/ssde-md.md)] 中常用動作的 Windows PowerShell 2.0 Cmdlet。 此外，查詢運算式與統一資源名稱 (URN) 可轉換為 SQL Server PowerShell 路徑，或用以指定 [!INCLUDE[ssDE](../includes/ssde-md.md)]中的一個或多個物件。  
  
## <a name="database-engine-cmdlets"></a>Database Engine Cmdlet  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 包含相對較少的 [!INCLUDE[ssDE](../includes/ssde-md.md)]Cmdlet。 多數用於 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的 PowerShell 指令碼，皆使用 SQL Server PowerShell 提供者和管理能力物件模型。 如需詳細資訊，請參閱 [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md)。  
  
 如需了解在 Windows PowerShell 環境中取得 SQL Server Cmdlet 相關說明的方法，請參閱＜ [Get Help SQL Server PowerShell](../powershell/sql-server-powershell.md)＞。  
  
### <a name="in-this-section"></a>本節內容  
 本節包含了有關這些 Cmdlet 的詳細資訊。  
  
|描述|指令程式|  
|-----------------|------------|  
|執行 TRANSACT-SQL 和 XQuery 指令碼，例如可使用執行的指令碼`sqlcmd`公用程式。|[Invoke-Sqlcmd Cmdlet](../../2014/database-engine/invoke-sqlcmd-cmdlet.md)|  
|評估 Database Engine 物件是否符合原則式管理之原則。|[Invoke-PolicyEvaluation 指令程式](../../2014/database-engine/invoke-policyevaluation-cmdlet.md)|  
  
### <a name="information-about-other-cmdlets"></a>其他 Cmdlet 的詳細資訊  
 `Encode-Sqlname`和`Decode-Sqlname`cmdlet 可協助您指定包含 PowerShell 路徑中不支援的字元的 SQL Server 識別碼。 如需詳細資訊，請參閱 [SQL Server Identifiers in PowerShell](../powershell/sql-server-identifiers-in-powershell.md)。  
  
 使用 `Convert-UrnToPath` Cmdlet 將 [!INCLUDE[ssDE](../includes/ssde-md.md)] 物件的唯一資源名稱轉換為 SQL Server PowerShell 提供者的路徑。 如需詳細資訊，請參閱 [Convert URNs to SQL Server Provider Paths](../../2014/database-engine/convert-urns-to-sql-server-provider-paths.md)。  
  
## <a name="query-expressions-and-unique-resource-names"></a>查詢運算式和唯一的資源名稱  
 查詢運算式是使用類似 XPath 語法的一些字串，可用以指定在物件模型階層中列舉一個或多個物件的準則集合。 唯一的資源名稱 (URN) 是可唯一識別單一物件的特定查詢運算式字串類型。 如需詳細資訊，請參閱 [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
