---
title: "唯讀狀態 （Excel 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f2aadcc2a1ce449b59f4ac360cad941203275e15
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="read-only-status-excel-driver"></a>唯讀狀態 （Excel 驅動程式）
使用 Microsoft Excel 驅動程式時，會以唯讀狀態開啟依預設，資料來源資料表，並只有一位使用者可以開啟一次。 即使資料表有唯讀狀態，不過，應用程式可以執行插入和更新的 Microsoft Excel 資料表。  
  
 當應用程式透過 Microsoft Excel 驅動程式的 Microsoft Excel 資料上執行 [另存新檔] 命令時，應用程式建立新的資料表中，插入的資料儲存到新的資料表。 插入會導致附加至資料表。 可以在資料表上不執行其他任何作業，直到它已關閉並重新開啟。 一旦關閉資料表，沒有後續插入可以執行，因為資料表然後是唯讀的資料表。  
  
 可更新的值時使用 Microsoft Excel 驅動程式，但無法從根據 Microsoft Excel 試算表，讓更新不會被視為正式支援 Microsoft Excel 驅動程式在資料表中刪除資料列。
