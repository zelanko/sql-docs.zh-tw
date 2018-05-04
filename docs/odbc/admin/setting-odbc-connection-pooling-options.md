---
title: 設定 ODBC 連接共用選項 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fe5e63542ab05690656ca772c8cad1aea8d98a7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setting-odbc-connection-pooling-options"></a>設定 ODBC 連接共用選項
連接共用可讓應用程式不需要重新建立每次使用的連接集區使用的連接。 您可以使用**連接共用** 索引標籤**ODBC 資料來源管理員**啟用和停用效能監視 對話方塊。 按兩下要設定連接逾時期限的驅動程式名稱。  
  
 在驅動程式層級，啟用連接共用是 CPTimeout 登錄值。 此選擇性每個驅動程式啟用，可讓系統管理員啟用連接共用，就可以支援它的驅動程式。 它被透過驅動程式的安裝程式期間設定 CPTimeout 的預設值。 按兩下要設定連接逾時期限的驅動程式名稱。  
  
 如需連接共用的詳細資訊，請參閱[ODBC 連接共用](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。  
  
## <a name="performance-monitoring"></a>效能監控  
 效能監視會追蹤連線效能期間透過錄製各種統計資料。 您可以自訂這些統計資料，包括如下所示的項目開發人員：  
  
|計數器|定義|  
|-------------|----------------|  
|每秒的 ODBC 硬碟連線計數器|每秒實際會對伺服器的連線數目。 第一次您的環境執行負載過重時，此計數器會向上非常快速。 幾秒之後，它將會卸除為零。 這是正常情況下，使用連接共用時。 當已建立連線到伺服器時，會使用，會重複使用集區中。|  
|ODBC 永久中斷連線的每秒的計數器|每秒發行至伺服器中斷連接硬式數目。 這些是實際連線到伺服器的連接共用所發行。 當您停止系統上的所有用戶端和逾時的時候開始連接時，這個值會增加從零。|  
|每秒的 ODBC 軟連線計數器|集區每秒所滿足的連接數目，亦即，已傳至使用者的連線從該集區。 此計數器會指出是否使用共用。 根據您的伺服器上的負載，是很常見，才能顯示每秒 40-60 軟性連接。|  
|每秒的 ODBC 軟中斷連線計數器|每秒由應用程式發出中斷連接數目。 當應用程式釋出或中斷時，連線會放回集區中。|  
|ODBC 目前作用中連線計數器|集區中目前正在使用中的連接數目。|  
|ODBC 目前可用的連線計數器|目前可用連線可用集區中的數目。 這些是可供使用的即時連接。|  
|集區的目前作用中|目前作用中的集區數目。 此計數器是在 Windows 8 中，管理連接集區中的連線的驅動程式新增至。 如需詳細資訊，請參閱[感知驅動程式的連接共用](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|建立集區|作用中，包括使用中和已移除集區的集區數目。 此計數器是在 Windows 8 中，管理連接集區中的連線的驅動程式新增至。 如需詳細資訊，請參閱[感知驅動程式的連接共用](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
  
 您必須指定監視的參數。 效能監視的範例已包含在此版本的 ODBC。
