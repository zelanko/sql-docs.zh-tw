---
title: "唯讀狀態 （Excel 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 641c6b6324ccb0f12cb5b28bd25b06dc0fcc5029
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="read-only-status-excel-driver"></a>唯讀狀態 （Excel 驅動程式）
使用 Microsoft Excel 驅動程式時，會以唯讀狀態開啟依預設，資料來源資料表，並只有一位使用者可以開啟一次。 即使資料表有唯讀狀態，不過，應用程式可以執行插入和更新的 Microsoft Excel 資料表。  
  
 當應用程式透過 Microsoft Excel 驅動程式的 Microsoft Excel 資料上執行 [另存新檔] 命令時，應用程式建立新的資料表中，插入的資料儲存到新的資料表。 插入會導致附加至資料表。 可以在資料表上不執行其他任何作業，直到它已關閉並重新開啟。 一旦關閉資料表，沒有後續插入可以執行，因為資料表然後是唯讀的資料表。  
  
 可更新的值時使用 Microsoft Excel 驅動程式，但無法從根據 Microsoft Excel 試算表，讓更新不會被視為正式支援 Microsoft Excel 驅動程式在資料表中刪除資料列。
