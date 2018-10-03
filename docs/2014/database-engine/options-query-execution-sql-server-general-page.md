---
title: 選項 （查詢執行-SQL Server-一般頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionGeneral
ms.assetid: 3f8d59bc-3f97-4e5d-8b86-5ac670d20780
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 947412d7a4d0fe27af7975919bddb3107007e801
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48152984"
---
# <a name="options-query-execution-sql-server-general-page"></a>選項 （查詢執行-SQL Server-一般頁面）
  使用此頁面可指定執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢的選項。 這些選項的變更僅適用於新的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢。 若要變更目前查詢的選項，請按一下 [查詢] 功能表上的 [查詢選項]，或在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢視窗中按一下滑鼠右鍵，並選取 [查詢選項]。  
  
## <a name="options"></a>選項。  
 **SET ROWCOUNT**  
 預設值 0 指出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 將等候結果，直到所有結果都收到為止。 如果您要 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在取得指定的資料列數後停止查詢，請提供大於 0 的值。 若要關閉此選項 (以便傳回所有資料列)，請指定 SET ROWCOUNT 0。  
  
 **SET TEXTSIZE**  
 2,147,483,647 個位元組的預設值，指出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 將提供完整的資料欄位，直到 `text` 和 `ntext` 資料欄位的上限。 提供較小的數值，即可在有大量數值時，限制傳回的結果數量。 資料行若大於提供的數值，就會被截斷。  
  
 **執行逾時**  
 在 **[新增連接]** 對話方塊中設定預設值。 使用此微調方塊，指出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 取消查詢之前要等候的秒數。 值為 0 表示無盡的等候，或沒有逾時。在新安裝上此值為 0。  
  
 **批次分隔符號**  
 輸入用來將 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式分隔成批次的文字。 預設為 GO。  
  
 **預設會以 SQLCMD 模式開啟新查詢**  
 選取此核取方塊，即可以 SQLCMD 模式開啟新查詢。 如需 SQLCMD 模式的詳細資訊，請參閱[使用查詢編輯器編輯 SQLCMD 指令碼](../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)。  
  
 當您選取此選項時，請注意以下限制：  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)] 查詢編輯器中的 IntelliSense 會關閉。  
  
-   由於查詢編輯器不會從命令列執行，所以您無法傳入命令列參數 (如變數)。  
  
-   由於查詢編輯器無法回應作業系統提示，所以您必須非常小心，不要執行互動式陳述式。  
  
 **重設為預設值**  
 按一下即可將此頁面上的所有值重設為原始預設值。  
  
## <a name="see-also"></a>另請參閱  
 [sqlcmd 工用程式](../tools/sqlcmd-utility.md)  
  
  
