---
title: "從 SQL Server Management Studio 執行 Windows PowerShell | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2f3f405a8a0a64d1202918154a163bf9b397ab93
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>從 SQL Server Management Studio 執行 Windows PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 您可以從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的**物件總管**中啟動 Windows PowerShell 工作階段。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 會啟動 Windows PowerShell、載入 **sqlps** 模組，以及設定物件總管樹狀目錄中相關聯節點的路徑內容。  
  
## <a name="before-you-begin"></a>開始之前  
 當您在物件總管中指定物件的執行中 PowerShell 時，[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會啟動已載入和註冊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 嵌入式管理單元的 Windows PowerShell 工作階段。 此工作階段的路徑會預設為您在 [物件總管] 中按一下滑鼠右鍵之物件的位置。 例如，如果您以滑鼠右鍵按一下物件總管中的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫物件，並選取 [啟動 PowerShell] 時，Windows PowerShell 路徑會設定為以下內容：  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="run-powershell"></a>執行 PowerShell  
 **從 SQL Server Management Studio 執行 PowerShell**  
  
1.  開啟 **[物件總管]**。  
  
2.  導覽至要進行處理之物件的節點。  
  
3.  以滑鼠右鍵按一下物件，並選取 [啟動 PowerShell]。  
  
## <a name="permissions"></a>Permissions  
 從 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]開啟 PowerShell 時，它不會以系統管理員權限執行，這可能會阻礙某些活動 (例如 WMI 的呼叫)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
