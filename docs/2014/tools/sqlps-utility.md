---
title: sqlps 公用程式 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqlps utility
- PowerShell [SQL Server], sqlps utility
ms.assetid: 4b2515a6-12c3-44fb-b263-1c567681cd2b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b25921a7b48ecd818527dd95ebc2d8714cb6871d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187038"
---
# <a name="sqlps-utility"></a>sqlps 公用程式
  `sqlps` 公用程式會啟動 Windows PowerShell 2.0 工作階段並且載入和註冊 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 提供者與指令程式。 您可以輸入 PowerShell 命令或指令碼，以便使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 元件來處理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體及其物件。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)]請改用 `sqlps` PowerShell 模組。 如需詳細資訊`sqlps`模組，請參閱 <<c2> [ 匯入 SQLPS 模組](../database-engine/import-the-sqlps-module.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
      sqlps   
[ [ [ -NoLogo ][ -NoExit ][ -NoProfile ]  
    [ -OutPutFormat { Text | XML } ] [ -InPutFormat { Text | XML } ]  
  ]  
  [ -Command { -  
             | script_block [ -argsargument_array ]  
             | string [ command_parameters ]  
             }  
  ]  
]  
[ -? | -Help ]  
```  
  
## <a name="arguments"></a>引數  
 **-NoLogo**  
 指定 `sqlps` 公用程式在啟動時隱藏著作權橫幅。  
  
 **-NoExit**  
 指定 `sqlps` 公用程式在啟動命令完成之後繼續執行。  
  
 **-NoProfile**  
 指定 `sqlps` 公用程式不要載入使用者設定檔。 使用者設定檔會記錄在 PowerShell 工作階段之間常用的別名、函數與變數。  
  
 **-OutPutFormat** { **Text** | **XML** }  
 指定`sqlps`公用程式輸出要格式化成為文字字串 (**文字**) 或序列化 CLIXML 格式 (**XML**)。  
  
 **-InPutFormat** { **Text** | **XML** }  
 指定的輸入要`sqlps`公用程式會格式化成為文字字串 (**文字**) 或序列化 CLIXML 格式 (**XML**)。  
  
 **-Command**  
 指定 `sqlps` 公用程式要執行的命令。 `sqlps`公用程式會執行命令，然後結束，除非 **-NoExit**同時指定。 請勿在 **-Command**之後指定任何其他參數，因為這些參數將會讀取成命令參數。  
  
 **-**  
 **-Command-** 指定`sqlps`公用程式從標準輸入讀取輸入。  
  
 *script_block* [ **-args**_argument_array_ ]  
 指定要執行的 PowerShell 命令區塊，此區塊必須以大括號括住：{}。 *Script_block*只有當指定`sqlps`公用程式會呼叫**PowerShell**或其他`sqlps`公用程式工作階段。 *argument_array* 是 PowerShell 變數的陣列，其中包含 *script_block*中 PowerShell 命令的引數。  
  
 *string* [ *command_parameters* ]  
 指定包含要執行之 PowerShell 命令的字串。 使用格式 **"& {*`command`*}"**。 引號表示字串，並叫用運算子 (&) 會導致`sqlps`公用程式來執行命令。  
  
 [ **-?** | **-Help** ]  
 顯示 `sqlps` 公用程式選項的語法摘要。  
  
## <a name="remarks"></a>備註  
 `sqlps`公用程式會啟動 PowerShell 環境 (PowerShell.exe) 並且載入[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]PowerShell 模組。 此模組，也稱為`sqlps`、 載入及註冊以下[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]PowerShell 嵌入式管理單元：  
  
-   Microsoft.SqlServer.Management.PSProvider.dll  
  
     實作 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 提供者和相關聯的 Cmdlet，例如 **Encode-SqlName** 和 **Decode-SqlName**。  
  
-   Microsoft.SqlServer.Management.PSSnapin.dll  
  
     實作 **Invoke-Sqlcmd** 和 **Invoke-PolicyEvaluation** Cmdlet。  
  
 您可以使用 `sqlps` 公用程式進行下列作業：  
  
-   以互動方式執行 PowerShell 命令。  
  
-   執行 PowerShell 指令碼檔案。  
  
-   執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 指令程式。  
  
-   使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者路徑來逐一導覽 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件的階層。  
  
 根據預設，`sqlps`公用程式執行時會將指令碼的執行原則，設定為**Restricted**。 如此即不會執行任何 PowerShell 指令碼。 您可以使用 **Set-ExecutionPolicy** Cmdlet 來允許執行已簽署的指令碼或任何指令碼。 建議您只執行來自信任來源的指令碼，並且利用適當的 NTFS 權限來保護所有輸入和輸出檔案。 如需有關啟用 PowerShell 指令碼的詳細資訊，請參閱 [執行 Windows PowerShell 指令碼](https://www.tech-recipes.com/rx/2513/powershell_enable_script_support/)。  
  
 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中的 `sqlps` 公用程式版本實作為 Windows PowerShell 1.0 迷你 shell。 迷你 Shell 有一些限制，例如不允許使用者載入迷你 Shell 所載入之嵌入式管理單元以外的嵌入式管理單元。 這些限制不適用於 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 及更高版本的公用程式，這些版本已經變更為使用 `sqlps` 模組。  
  
## <a name="examples"></a>範例  
 **A.在不顯示著作權橫幅的預設互動模式中執行 sqlps 公用程式**  
  
```  
sqlps -NoLogo  
```  
  
 **B.從命令提示字元處執行 SQL Server PowerShell 指令碼**  
  
```  
sqlps -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
 **C.從命令提示字元處執行 SQL Server PowerShell 指令碼，並在指令碼完成之後維持執行狀態**  
  
```  
sqlps -NoExit -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
## <a name="see-also"></a>另請參閱  
 [啟用或停用伺服器網路通訊協定](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
