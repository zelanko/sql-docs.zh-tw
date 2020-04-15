---
title: 設定 ODBC 連接池選項 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1d8e66c506518b77320347ce9120254aa1cae287
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307192"
---
# <a name="setting-odbc-connection-pooling-options"></a>設定 ODBC 連線共用選項
連接池使應用程式能夠使用連接池中的連接,而不需要為每個使用重新建立連接池。 您可以使用**ODBC 資料來源管理員**對話方塊的連接**池**選項卡來啟用和禁用效能監視。 按兩下驅動程式名稱以設置連接超時時間。  
  
 在驅動程式級別,連接池由 CPTimeout 註冊表值啟用。 這種選擇性的每個驅動程式啟用允許系統管理員僅為支援它的驅動程序啟用連接池。 通過在驅動程式設置程式期間設置 CPTimeout 的預設值來實現。 按兩下驅動程式名稱以設置連接超時時間。  
  
 有關連接池的詳細資訊,請參閱[ODBC 連接池](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。  
  
## <a name="performance-monitoring"></a>效能監控  
 性能監控通過記錄各種統計資訊來跟蹤連接性能。 開發人員可以自定義這些統計資訊,以包括以下項:  
  
|計數器|定義|  
|-------------|----------------|  
|ODBC 硬連線計數器每秒|每秒對伺服器進行的實際連接數。 第一次你的環境攜帶重負荷時,這個計數器會很快上升。 幾秒鐘后,它將下降到零。 這是連接池工作時的正常情況。 建立與伺服器的連接后,將使用這些連接並將其放置在池中以供重用。|  
|ODBC 每秒硬斷開計數器|每秒頒發給伺服器的硬斷開連接數。 這些是連接池釋放的伺服器的實際連接。 當您停止系統上的所有用戶端並且連接開始超時時,此值將從零增加。|  
|ODBC 每秒軟連線計數器|池每秒滿足的連接數,換句話說,從該池交給用戶的連接。 此計數器指示池是否工作。 根據伺服器上的負載,每秒顯示 40-60 個軟連接的情況並不少見。|  
|ODBC 每秒軟斷開計數器|應用程式每秒發出的斷開連接數。 當應用程式釋放或斷開連接時,連接將放回池中。|  
|ODBC 目前活動連接計數器|池中目前正在使用的連接數。|  
|ODBC 電流自由連線計數器|池中可用的當前可用連接數。 這些是可用的即時連接。|  
|池目前處於活動狀態|當前處於活動狀態的池數。 此計數器在 Windows 8 中添加,用於管理連接池中連接的驅動程式。 有關詳細資訊,請參閱[驅動程式感知連接池](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|已建立池|活動池數,包括活動池和已刪除池。 此計數器在 Windows 8 中添加,用於管理連接池中連接的驅動程式。 有關詳細資訊,請參閱[驅動程式感知連接池](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
  
 您必須指定自己的監視參數。 此版本的 ODBC 中已包含用於效能監控的樣本。
