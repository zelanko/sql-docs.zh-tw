---
title: 步驟4b：提取資料列計數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- fetches [ODBC], fetching row count
- row count [ODBC]
- application process [ODBC], fetching row count
ms.assetid: 3af481b1-d694-446e-948d-e3a5edcad050
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31ccbd15ae435165ea007fa9f3c0505c1dcc5aa0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302959"
---
# <a name="step-4b-fetch-the-row-count"></a>步驟 4b：擷取資料列計數
下一步是提取資料列計數，如下圖所示。  
  
 ![顯示提取資料列計數](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 如果在步驟3中執行的語句是**UPDATE**、 **DELETE**或**INSERT**語句，應用程式會使用**SQLRowCount**來抓取受影響的資料列計數。 如需詳細資訊，請參閱[判斷受影響的資料列數目](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
 應用程式現在會回到步驟3，以在相同的交易中執行另一個語句，或繼續進行步驟5來認可或回復交易。
