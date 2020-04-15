---
title: 使用資料來源 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df9b09e4c5519e0fff44902bd83b8e3d92a67ca8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286538"
---
# <a name="using-data-sources"></a>使用資料來源
資料來源通常由最終使用者或技術人員建立,其程式稱為*ODBC 管理員*。 ODBC 管理員提示使用者使用驅動程式,然後調用該驅動程式。 驅動程式顯示一個對話框,該對話方塊請求連接到數據源所需的資訊。 使用者輸入資訊后,驅動程式將其存儲在系統上。  
  
 稍後,應用程式調用驅動程式管理員,並傳遞計算機數據源的名稱或包含檔數據源的檔的路徑。 傳遞計算機數據源名稱時,驅動程式管理器將搜索系統以查找數據來源使用的驅動程式。 然後載入驅動程式並將數據源名稱傳遞給它。 驅動程式使用資料源名稱尋找連接到資料來源所需的資訊。 最後,它連接到數據源,通常提示使用者輸入使用者 ID 和密碼,這些 ID 和密碼通常不儲存。  
  
 傳遞檔案資料來源時,驅動程式管理員將打開該檔並載入指定的驅動程式。 如果檔還包含連接字串,它將將其傳遞給驅動程式。 使用連接字串中的資訊,驅動程式連接到資料來源。 如果未傳遞連接字串,驅動程式通常會提示用戶獲得必要的資訊。
