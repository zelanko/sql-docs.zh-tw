---
title: 步驟 4a:獲取結果 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], fetching results
- fetches [ODBC], fetching results
ms.assetid: 77d30142-c774-473c-96fb-b364bb92ac60
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c4f810e5c42b54ec871c233ab498936abae610dc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302969"
---
# <a name="step-4a-fetch-the-results"></a>步驟 4a：擷取結果
下一步是獲取結果,如下圖所示。  
  
 ![顯示 ODBC 應用程式的提取結果](../../../odbc/reference/develop-app/media/pr14.gif "pr14")  
  
 如果在「步驟 3:生成和執行 SQL 語句」中執行的語句是**SELECT**語句或目錄函數,則應用程式首先調用**SQLNumResultCols**以確定結果集中的列數。 如果應用程式已經知道結果集列的數量(例如,在垂直或自定義應用程式中硬編碼 SQL 語句時),則不需要此步驟。  
  
 接下來,應用程式使用**SQLDescribeCol**檢索每個結果集列的名稱、數據類型、精度和比例。 同樣,對於已經知道此資訊的垂直和自定義應用程式,這同樣是必需的。 應用程式將此資訊傳遞給 SQLBindCol ,該**SQLBindCol**將應用程式變數綁定到結果集中的列。  
  
 應用程式現在調用**SQLFetch**來檢索第一行數據,並將該行中的數據放在與**SQLBindCol**綁定的變數中。 如果行中有任何長數據,則調用**SQLGetData**來檢索該數據。 應用程序繼續調用**SQLFetch**和**SQLGetData**來檢索其他數據。 完成數據提取後,它將調用**SQLCloseCursor**關閉游標。  
  
 有關檢索結果的完整說明,請參閱[檢索結果(基本)](../../../odbc/reference/develop-app/retrieving-results-basic.md)和[檢索結果(高級)。](../../../odbc/reference/develop-app/retrieving-results-advanced.md)  
  
 應用程式現在返回到「步驟 3:生成和執行 SQL 語句」,以在同一事務中執行另一個語句;或繼續「步驟 5:提交事務」以提交或回滾事務。
