---
title: 命令視窗
description: 了解如何使用 Transact-SQL 偵錯工具的 [命令] 視窗來執行偵錯命令，以及在將要進行偵錯的程式碼上編輯命令。
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Command Window [Transact-SQL]
ms.assetid: e567ebf9-0793-451b-92c7-26193a02d9da
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3465a430f9b9103088e08db045d1c42338c0224f
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901428"
---
# <a name="transact-sql-debugger---command-window"></a>Transact-SQL 偵錯工具 - 命令視窗

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

使用 [命令] 視窗可針對目前正在偵錯的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] [查詢編輯器] 視窗內程式碼執行命令，例如偵錯和編輯命令。 您必須在偵錯模式中，才能使用 [命令] 視窗。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [命令] 視窗支援許多相同的命令。 如需詳細資訊，請參閱 [Visual Studio 命令視窗](https://go.microsoft.com/fwlink/?LinkId=112007)。  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>工作清單

**存取命令視窗**

- 在 **[偵錯]** 功能表上，按一下 **[開始偵錯]** 。

**列印變數的值**

- 在 [命令] 視窗中鍵入 **Debug.Print \<VariableName>** ，然後按 ENTER。

**列出有關目前執行緒的資訊**

- 在 [命令] 視窗輸入 **Debug.ListThread**，然後按 ENTER 鍵。

**將變數加入至快速監看式視窗**

- 在 [命令] 視窗中鍵入 **Debug.QuickWatch \<VariableName>** ，然後按 ENTER。

## <a name="see-also"></a>另請參閱

[Transact-SQL 偵錯工具](../../relational-databases/scripting/transact-sql-debugger.md)
