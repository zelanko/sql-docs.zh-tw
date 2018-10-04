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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46b6f5d7e6af3726558f5cee72f00ff06e13ab89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812054"
---
# <a name="setting-odbc-connection-pooling-options"></a>設定 ODBC 連線共用選項
連接共用，可讓應用程式使用來自不需要重新建立每次使用的連接集區的連接。 您可以使用**連接共用**索引標籤**ODBC 資料來源管理員**啟用和停用效能監視 對話方塊。 按兩下驅動程式名稱，若要設定連接逾時期限。  
  
 在驅動程式層級中，連接共用被啟用 CPTimeout 登錄值。 此選擇性每個驅動程式啟用時，可讓系統管理員來啟用連線共用只是驅動程式可支援它。 它會透過驅動程式的安裝程式期間設定 CPTimeout 的預設值。 按兩下驅動程式名稱，若要設定連接逾時期限。  
  
 如需有關連接共用的詳細資訊，請參閱[ODBC 連接共用](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。  
  
## <a name="performance-monitoring"></a>效能監控  
 效能監視會追蹤連線效能，藉由記錄各種不同的統計資料。 這些統計資料可以來自訂開發人員包含項目，如下所示：  
  
|計數器|定義|  
|-------------|----------------|  
|每秒的 ODBC 硬碟連線計數器|每秒實際會對伺服器的連線數目。 您的環境會帶來負載過重時，第一次此計數器會往非常快速。 幾秒之後，它將會降為零。 正在連接共用時，這是一般的情況。 當建立伺服器的連線之後時，請他們會使用並放在重複使用的集區中。|  
|ODBC 永久中斷連線的每秒的計數器|每秒發行至伺服器，中斷連接的硬碟數目。 這些是實際連線到伺服器的連接共用已發行。 當您停止系統上的所有用戶端，並連接啟動逾時，這個值會增加從零。|  
|每秒的 ODBC 軟性連接計數器|集區每秒所滿足的連線數目 — 換句話說，來自該集區的連線已交付給使用者。 此計數器會指出是否使用共用。 根據您的伺服器上的負載，並不常見顯示 40 – 60 秒的軟性連接。|  
|每秒的 ODBC 軟中斷連線計數器|每秒發出之應用程式所，中斷連線的數目。 當應用程式釋出或中斷連線時，連線會放回集區中。|  
|ODBC 目前作用中連線計數器|集區中目前正在使用中的連線數目。|  
|ODBC 目前可用的連線計數器|免費可用的連線集區中目前數目。 這些是可供使用的即時連線。|  
|集區目前作用中|目前使用中的集區數目。 此計數器已在 Windows 8 中，針對 管理連接集區中的連線的驅動程式。 如需詳細資訊，請參閱 <<c0> [ 感知驅動程式的連接共用](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|建立集區|作用中，包括作用中和已移除集區的集區數目。 此計數器已在 Windows 8 中，針對 管理連接集區中的連線的驅動程式。 如需詳細資訊，請參閱 <<c0> [ 感知驅動程式的連接共用](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
  
 您必須指定您自己的監視參數。 效能監視的範例已包含在此版本的 ODBC。
