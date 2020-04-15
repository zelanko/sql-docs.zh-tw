---
title: 步驟 4b:獲取行計數 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302959"
---
# <a name="step-4b-fetch-the-row-count"></a>步驟 4b：擷取資料列計數
下一步是獲取行計數,如下圖所示。  
  
 ![顯示提取資料列計數](../../../odbc/reference/develop-app/media/pr15.gif "pr15")  
  
 如果在步驟 3 中執行的語句是**更新**、**刪除**或**INSERT**語句,則應用程式將檢索使用**SQLRowCount**的受影響行的計數。 有關詳細資訊,請參閱[確定受影響的行數](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
 應用程式現在返回到步驟 3 以執行同一事務中的另一個語句,或繼續執行步驟 5 以提交或回滾事務。
