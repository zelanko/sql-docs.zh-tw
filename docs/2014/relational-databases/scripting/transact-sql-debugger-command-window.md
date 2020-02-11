---
title: 命令視窗
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26306f8ad2adf01ebdcbf1b52169f1c2ec964920
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "75243075"
---
# <a name="command-window"></a>命令視窗
  針對目前**** 正在進行調試的 [ [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]查詢編輯器] 視窗中的程式碼，使用命令來執行命令，例如 [debug] 和 [edit] 命令。 您必須在偵錯模式中，才能使用 [命令] 視窗****。 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具會支援  [命令][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **** 視窗內也支援的許多命令。 如需詳細資訊，請參閱 [Visual Studio 命令視窗](https://go.microsoft.com/fwlink/?LinkId=112007)。  
  
## <a name="task-list"></a>工作清單  
 **存取命令視窗**  
  
-   在 **[偵錯]** 功能表上，按一下 **[開始偵錯]** 。  
  
 **列印變數的值**  
  
-   在 [命令]**** 視窗輸入 **Debug.Print \<變數名稱>**，然後按 ENTER 鍵。  
  
 **列出目前線程的相關資訊**  
  
-   在**命令**中，輸入`Debug.ListThread`，然後按 enter。  
  
 **將變數加入至快速監看式視窗**  
  
-   在 [命令]**** 視窗輸入 **Debug.QuickWatch \<變數名稱>**，然後按 ENTER 鍵。  
  
## <a name="see-also"></a>另請參閱  
 [Transact-SQL 偵錯工具](transact-sql-debugger.md)  
