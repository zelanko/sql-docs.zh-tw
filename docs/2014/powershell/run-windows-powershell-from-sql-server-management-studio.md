---
title: 從 SQL Server Management Studio 執行 Windows PowerShell | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f8ce7eb6e1ba660a676aa08087e689d1d6b1c550
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37215148"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>從 SQL Server Management Studio 執行 Windows PowerShell
  您可以從 **的** [物件總管] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中啟動 Windows PowerShell 工作階段。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 會啟動 Windows PowerShell、 載入`sqlps`模組，並在相關聯的節點設定的路徑內容**物件總管 中**樹狀目錄中。  
  
## <a name="before-you-begin"></a>開始之前  
 當您在物件總管中指定物件的執行中 PowerShell 時，[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 會啟動已載入和註冊 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 嵌入式管理單元的 Windows PowerShell 工作階段。 此工作階段的路徑會預設為您在 [物件總管] 中按一下滑鼠右鍵之物件的位置。 例如，如果您以滑鼠右鍵按一下物件總管中的 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 資料庫物件，並選取 [啟動 PowerShell] 時，Windows PowerShell 路徑會設定為以下內容：  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="run-powershell"></a>執行 PowerShell  
 **從 SQL Server Management Studio 執行 PowerShell**  
  
1.  開啟 **[物件總管]**。  
  
2.  導覽至要進行處理之物件的節點。  
  
3.  以滑鼠右鍵按一下物件，並選取 [啟動 PowerShell]。  
  
## <a name="permissions"></a>Permissions  
 從 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]開啟 PowerShell 時，它不會以系統管理員權限執行，這可能會阻礙某些活動 (例如 WMI 的呼叫)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
