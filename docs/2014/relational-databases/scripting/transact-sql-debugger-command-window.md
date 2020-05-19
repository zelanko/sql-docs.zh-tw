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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a7f8e72831e333323621279a0403e95e6a134860
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718418"
---
# <a name="command-window"></a>命令視窗
  使用 [命令]  視窗可針對目前所偵錯之 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] [查詢編輯器] 視窗內的程式碼執行命令，例如偵錯和編輯命令。 您必須在偵錯模式中，才能使用 [命令] 視窗  。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [命令]  視窗支援許多相同的命令。 如需詳細資訊，請參閱 [Visual Studio 命令視窗](https://go.microsoft.com/fwlink/?LinkId=112007)。  
  
## <a name="task-list"></a>工作清單  
 **存取命令視窗**  
  
-   在 **[偵錯]** 功能表上，按一下 **[開始偵錯]** 。  
  
 **列印變數的值**  
  
-   在 [命令]  視窗輸入 **Debug.Print \<變數名稱>** ，然後按 ENTER 鍵。  
  
 **列出有關目前執行緒的資訊**  
  
-   在**命令**中，輸入 `Debug.ListThread` ，然後按 enter。  
  
 **將變數加入至快速監看式視窗**  
  
-   在 [命令]  視窗輸入 **Debug.QuickWatch \<變數名稱>** ，然後按 ENTER 鍵。  
  
## <a name="see-also"></a>另請參閱  
 [Transact-SQL 偵錯工具](transact-sql-debugger.md)  
