---
title: 作用中的作業對話方塊 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.ssms.isoperations.executions.f1
- sql12.ssis.ssms.isoperations.general.f1
ms.assetid: 5bb0fcd6-0ce9-488a-85b8-25dddaa03cda
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: adf25cd2194e1a02877c38a15d81d8697427ad76
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023821"
---
# <a name="active-operations-dialog-box"></a>作用中的作業對話方塊
  使用 **[作用中的作業]** 對話方塊檢視 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 伺服器上目前執行中之 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 作業 (例如，部署、驗證及封裝執行) 的狀態。 此資料儲存在 SSISDB 目錄中。  
  
 如需相關 [!INCLUDE[tsql](../includes/tsql-md.md)] 檢視的詳細資訊，請參閱 [catalog.operations &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database)、[catalog.validations &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-validations-ssisdb-database) 和 [catalog.executions &#40;SSISDB 資料庫&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database)  
  
 **您想要做什麼事？**  
  
1.  [開啟 [作用中的作業] 對話方塊](#open_dialog)  
  
2.  [設定選項](#options)  
  
##  <a name="open_dialog"></a> 開啟 [作用中的作業] 對話方塊  
  
1.  開啟[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。  
  
2.  連接 Microsoft SQL Server Database Engine  
  
3.  在 [物件總管] 中，展開 **[Integration Services]** 節點，再以滑鼠右鍵按一下 **[SSISDB]**，然後按一下 **[作用中的作業]**。  
  
##  <a name="options"></a> 設定選項  
  
### <a name="options"></a>選項。  
 **型別**  
 指定作業的類型。 以下是可能的值為**類型**欄位與 TRANSACT-SQL 的 operations_type 資料行中的對應值`catalog.operations`檢視。  
  
|||  
|-|-|  
|初始化 Integration Services|@shouldalert|  
|作業清除 (SQL 代理程式作業)|2|  
|專案版本清理 (SQL 代理程式作業)|3|  
|部署專案|101|  
|還原專案|106|  
|建立及啟動封裝執行|200|  
|停止作業 (停止驗證或執行|202|  
|驗證專案|300|  
|驗證封裝|301|  
|設定目錄|1000|  
  
 **停止**  
 按一下即可停止目前執行中的作業。  
  
  
