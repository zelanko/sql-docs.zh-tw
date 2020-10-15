---
title: 從 SQL Server Management Studio 執行 Windows PowerShell | Microsoft 文件
description: 了解如何從 SQL Server Management Studio 中的 [物件總管] 啟動 Windows PowerShell 工作階段，並將路徑預設為所選物件的位置。
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 03/14/2017
ms.openlocfilehash: c074b0f0ed5f5b041a8a4c4ed341837fec2b1926
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006171"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>從 SQL Server Management Studio 執行 Windows PowerShell

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

您可以從 **的** [物件總管] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中啟動 Windows PowerShell 工作階段。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 會啟動 Windows PowerShell、載入 **SqlServer** 模組，以及設定物件總管樹狀目錄中相關聯節點的路徑內容。  

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

當您在物件總管中指定物件的執行中 PowerShell 時，[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 會啟動已載入和註冊 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 嵌入式管理單元的 Windows PowerShell 工作階段。 此工作階段的路徑會預設為您在物件總管中按一下滑鼠右鍵之物件的位置。 例如，如果您以滑鼠右鍵按一下物件總管中的 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫物件，並選取 [啟動 PowerShell]**** 時，Windows PowerShell 路徑會設定為以下內容：  

```powershell
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```

## <a name="run-powershell"></a>執行 PowerShell

### <a name="to-run-powershell-from-sql-server-management-studio"></a>從 SQL Server Management Studio 執行 PowerShell

1. 開啟 **[物件總管]** 。

2. 導覽至要進行處理之物件的節點。

3. 以滑鼠右鍵按一下物件，並選取 [啟動 PowerShell]。

## <a name="permissions"></a>權限

從 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 開啟 PowerShell 時，它不會以系統管理員權限執行，這可能會阻礙某些活動 (例如 WMI 的呼叫)。  
  
## <a name="see-also"></a>另請參閱

- [SQL Server PowerShell](sql-server-powershell.md)