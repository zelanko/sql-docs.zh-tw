---
title: 設定 ODBC 連接共用選項 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307192"
---
# <a name="setting-odbc-connection-pooling-options"></a>設定 ODBC 連線共用選項
連線共用可讓應用程式使用連線集區的連線，而不需要重新建立每個使用的連接。 您可以使用 [ **ODBC 資料來源管理員**] 對話方塊的 [**連接**共用] 索引標籤，啟用和停用效能監視。 按兩下驅動程式名稱以設定連接逾時時間。  
  
 在驅動程式層級，連接共用是由 CPTimeout 登錄值所啟用。 這個選擇性的每一驅動程式可讓系統管理員僅針對可支援的驅動程式啟用連接共用。 在驅動程式的安裝程式期間設定 CPTimeout 的預設值，即可完成此作業。 按兩下驅動程式名稱以設定連接逾時時間。  
  
 如需連接共用的詳細資訊，請參閱[ODBC 連接](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)共用。  
  
## <a name="performance-monitoring"></a>效能監控  
 效能監視會藉由記錄各種統計資料來追蹤連接效能。 這些統計資料可以由開發人員自訂，以包含如下所示的專案：  
  
|計數器|定義|  
|-------------|----------------|  
|每秒的 ODBC 硬性連接計數器|每秒對伺服器進行的實際連接數目。 當您的環境第一次進入負載過重時，此計數器會非常快速地啟動。 幾秒鐘後，它就會降至零。 當連接共用正常運作時，這是正常情況。 建立伺服器的連線之後，將會使用這些連接並放在集區中以供重複使用。|  
|每秒的 ODBC 硬中斷連線計數器|每秒發出至伺服器的硬中斷連線數。 這些是連接共用所發行之伺服器的實際連接。 當您停止系統上的所有用戶端，且連線開始超時時，此值會從零增加。|  
|每秒的 ODBC 軟連接計數器|集區每秒滿足的連線數目-換言之，從該集區傳送給使用者的連接數。 此計數器指出共用是否正常運作。 視伺服器上的負載而定，這通常會顯示每秒40-60 個軟連線的情況。|  
|每秒的 ODBC 軟中斷連接計數器|應用程式每秒發出的中斷連接數目。 當應用程式釋放或中斷連線時，連接就會放回集區中。|  
|ODBC 目前作用中的連接計數器|集區中目前使用中的連接數目。|  
|ODBC 目前的免費連接計數器|集區中目前可用的可用連線數目。 這些是可供使用的即時連線。|  
|目前使用中的集區|目前使用中的集區數目。 這個計數器是在 Windows 8 中新增，適用于管理連接集區中連接的驅動程式。 如需詳細資訊，請參閱可[感知驅動程式的連接](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)共用。|  
|建立的集區|使用中的集區數目，包括作用中和已移除的集區。 這個計數器是在 Windows 8 中新增，適用于管理連接集區中連接的驅動程式。 如需詳細資訊，請參閱可[感知驅動程式的連接](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)共用。|  
  
 您必須指定自己的監視參數。 此版本的 ODBC 已包含效能監視的範例。
