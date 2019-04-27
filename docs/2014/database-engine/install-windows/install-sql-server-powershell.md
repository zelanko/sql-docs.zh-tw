---
title: 安裝 SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a90a30a0ae7fe09d49b1d42b577b13370c48c0de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775438"
---
# <a name="install-sql-server-powershell"></a>安裝 SQL Server PowerShell
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式若偵測到您選取了內含 PowerShell 元件的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能，但卻未安裝 Windows PowerShell 2.0，其將會停止。 您必須使用 Windows Management Framework 安裝 Windows PowerShell 2.0，然後重新執行安裝程式。  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-powershell-support"></a>安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 支援  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式安裝提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows PowerShell 支援的軟體。 當您選取需要 PowerShell 支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能時，安裝程式會檢查有無安裝 Windows PowerShell 2.0。 PowerShell 2.0 若已存在，安裝程式將會安裝下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 元件：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 嵌入式管理單元。這些嵌入式管理單元是可實作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之兩種 Windows PowerShell 支援的 dll 檔案：  
  
    -   一組 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指令程式。 指令程式是實作特定動作的命令。 例如 **Invoke-Sqlcmd** 會執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 XQuery 指令碼 (此指令碼也可使用 **sqlcmd** 公用程式加以執行)，而 **Invoke-PolicyEvaluation** 則會報告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件是否符合原則型管理原則。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供者。 此提供者可讓您使用類似於檔案系統路徑的路徑來導覽 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件階層。 每一個物件都與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件模型中的類別有關聯。 您可以使用此類別的方法和屬性來針對物件執行工作。 例如，如果您執行 cd 切換到路徑中的資料庫物件，您可以使用 Microsoft.SqlServer.Managment.SMO.Database 類別的方法和屬性來管理資料庫。  
  
-   **Sqlps**匯入 Windows PowerShell 2.0 工作階段以載入的模組[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]嵌入式管理單元。  
  
-   已被取代**sqlps**公用程式會啟動 Windows PowerShell 2.0 工作階段並匯入**sqlps**模組。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 支援從物件總管樹狀結構啟動 Windows PowerShell 工作階段。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式支援 Windows PowerShell 作業步驟。  
  
 如果尚未安裝，Windows PowerShell 2.0，或已解除安裝，您必須安裝它遵循上的指示[Windows Management Framework](https://go.microsoft.com/fwlink/?LinkId=186214)頁面。  
  
 如果在安裝程式完成之後解除安裝了 Windows PowerShell，將會造成 Windows PowerShell 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能無法運作。 Windows PowerShell 可以由 Windows 使用者解除安裝，而且某些 Windows 作業系統升級可能也會要求解除安裝 Windows PowerShell。 如果要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 功能，您必須使用 Windows Management Framework 安裝 PowerShell 2.0。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)  
  
  
