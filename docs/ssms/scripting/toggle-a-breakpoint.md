---
title: 切換中斷點
description: 了解如何切換中斷點來醒目提示相關聯的 Transact-SQL 陳述式，以及在陳述式上執行各種動作 (例如編輯)。
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
ms.assetid: c477ab89-a1cd-4f2c-aa7c-40525041100f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 159834507edfc57466dc0872bf42e2976c4ca8cc
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248063"
---
# <a name="toggle-a-breakpoint"></a>切換中斷點

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式上設定中斷點的動作稱為切換中斷點。  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="breakpoints"></a>中斷點

一旦設定中斷點，就會以陳述式左邊灰色列中的圖示來表示它。 此圖示稱為中斷點圖像。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中斷點會套用至完整的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 當中斷點切換為開時，偵錯工具會反白顯示關聯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
 如果在一行中有多個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，您可以切換每個陳述式的中斷點。 如果按一下視窗左邊灰色列，會切換行中第一個陳述式的中斷點。 藉由反白顯示陳述式的任何部分或將游標移至陳述式，然後按下 F9 或按一下 [偵錯]**** 功能表上的 [切換中斷點]****，可切換後續陳述式的中斷點。 如果在一行中有多個中斷點，左邊灰色列中只有一個中斷點圖像。  
  
 切換中斷點之後，您可以針對中斷點執行各種動作，例如編輯其屬性或暫時予以停用。 如需詳細資訊，請參閱 [Transact-SQL 中斷點](../../relational-databases/scripting/transact-sql-breakpoints.md)。  
  
## <a name="toggle-a-breakpoint"></a>切換中斷點  
 **切換 Transact-SQL 陳述式上的中斷點**  
  
1.  按一下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式左邊的灰色列。  
  
2.  或是反白顯示陳述式的任何部分或將游標移至陳述式，然後執行下列其中一個動作：  
  
    -   按 F9 鍵。  
  
    -   在 [偵錯] 功能表上，按一下 [切換中斷點]。  
  
  
