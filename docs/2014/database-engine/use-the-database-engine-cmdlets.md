---
title: 使用 Database Engine Cmdlet | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Cmdlets [SQL Server], Encode-Sqlname
- Encode-Sqlname cmdlet
- PowerShell [SQL Server], Encode-Sqlname
- Convert-UrnToPath cmdlet
- PowerShell [SQL Server], cmdlets
- Cmdlets [SQL Server]
- PowerShell [SQL Server], Convert-UrnToPath
- Cmdlets [SQL Server], Convert-UrnToPath
- Decode-Sqlname cmdlet
- PowerShell [SQL Server], Decode-Sqlname
- Cmdlets [SQL Server], Decode-Sqlname
ms.assetid: 720aa982-09ae-41a3-b603-a91004cfbe3e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cd5575c94c9a74623efaa80c9470c54982a41d0d
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783105"
---
# <a name="use-the-database-engine-cmdlets"></a>使用 Database Engine Cmdlet
  Windows PowerShell Cmdlet 是單一功能的命令，通常具有動詞-名詞命名慣例，例如 **Get-Help** 或 **Set-MachineName**。 適用於 Windows PowerShell 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者會提供 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]特有的指令程式。  
  
## <a name="database-engine-cmdlets"></a>Database Engine 指令程式  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會實作少數的 [!INCLUDE[ssDE](../includes/ssde-md.md)]Cmdlet。 這些指令程式主要是用來從新的 PowerShell 指令碼執行現有的 Transact-SQL 指令碼、評估原則式管理原則，以及協助在 SQL Server 提供者路徑中指定 SQL Server 識別碼。  
  
 大部分的 Windows PowerShell 指令碼都會使用 SQL Server PowerShell 提供者和 SQL Server 管理能力物件模型，來處理 [!INCLUDE[ssDE](../includes/ssde-md.md)] 。 如需詳細資訊，請參閱 [SQL Server PowerShell](../powershell/sql-server-powershell.md)。  
  
### <a name="get-cmdlet-help"></a>取得指令程式說明  
 在 Windows PowerShell 環境中， **Get-Help** Cmdlet 會提供每個 Cmdlet 的說明資訊。 **Get-Help** 會傳回語法、參數定義、輸入和輸出類型以及 Cmdlet 所執行之動作描述等資訊。 如需詳細資訊，請參閱＜ [Get Help SQL Server PowerShell](../../2014/database-engine/get-help-sql-server-powershell.md)＞。  
  
### <a name="partial-parameter-names"></a>部分參數名稱  
 您不需要指定指令程式參數的完整名稱。 您只要指定足夠的名稱，就可以唯一地分隔它與指令程式所支援的其他參數。 例如，下列範例將示範三種指定 **Invoke-Sqlcmd -QueryTimeout** 參數的方式：  
  
```powershell
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTimeout 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTime 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryT 3  
```  
  
## <a name="database-engine-cmdlet-tasks"></a>Database Engine 指令程式工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何使用 **Invoke-Sqlcmd** 來執行包含 **或 XQuery 陳述式的** sqlcmd [!INCLUDE[tsql](../includes/tsql-md.md)] 指令碼或命令。 它可接受 **sqlcmd** 輸入作為字元字串輸入參數，或作為要開啟的指令碼檔案名稱。|[Invoke-Sqlcmd 指令程式](../../2014/database-engine/invoke-sqlcmd-cmdlet.md)|  
|描述如何使用 **Invoke-PolicyEvaluation** 報告 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件的目標集是否符合在原則式管理原則中定義的條件。 您可以選擇性地使用此指令程式，在目標物件中重新設定任何不符合原則條件的可設定選項。|[Invoke-PolicyEvaluation Cmdlet](../../2014/database-engine/invoke-policyevaluation-cmdlet.md)|  
|描述如何使用 `Encode-Sqlname` 和 `Decode-Sqlname` 處理含有 Windows PowerShell 路徑不支援之字元的 SQL Server 識別碼。|[編碼及解碼 SQL Server 識別碼](../powershell/encode-and-decode-sql-server-identifiers.md)|  
|描述如何使用 `Convert-UrnToPath`，將 SQL Server 管理能力物件統一資源名稱 (URN) 轉換為對等的 SQL Server 提供者路徑。|[將 URN 轉換成 SQL Server 提供者路徑](../../2014/database-engine/convert-urns-to-sql-server-provider-paths.md)|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell 提供者](../powershell/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)   
 [AlwaysOn 可用性群組&#40;SQL Server 的 PowerShell Cmdlet 總覽&#41;](availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  
