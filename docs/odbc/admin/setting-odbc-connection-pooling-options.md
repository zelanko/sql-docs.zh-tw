---
description: 設定 ODBC 連線共用選項
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
ms.openlocfilehash: 5d6f741654f9765e909a8a2e33bce5e7e596f8b4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386594"
---
# <a name="setting-odbc-connection-pooling-options"></a>設定 ODBC 連線共用選項
連線共用可讓應用程式使用連接集區中不需要重新建立以供每次使用的連接。 您可以使用 [ **ODBC 資料來源管理員**] 對話方塊的 [**連接**共用] 索引標籤，來啟用和停用效能監視。 按兩下驅動程式名稱以設定連接逾時時間。  
  
 在驅動程式層級，連接共用是由 CPTimeout 登錄值啟用。 這種選擇性的每一驅動程式可讓系統管理員只針對可支援的驅動程式啟用連接共用。 它是在驅動程式安裝程式期間設定 CPTimeout 的預設值來完成。 按兩下驅動程式名稱以設定連接逾時時間。  
  
 如需連接共用的詳細資訊，請參閱 [ODBC 連接](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)共用。  
  
## <a name="performance-monitoring"></a>效能監控  
 效能監視會藉由錄製各種統計資料來追蹤連接效能。 這些統計資料可以由開發人員自訂，以包含下列專案：  
  
|計數器|定義|  
|-------------|----------------|  
|每秒 ODBC 硬性連接計數器|每秒對伺服器進行的實際連接數。 當您第一次的環境耗用大量負載時，此計數器將會非常快速地啟動。 幾秒鐘後，它會降到零。 這是連接共用運作時的一般情況。 建立與伺服器的連線之後，將會使用這些連接並放在集區中，以供重複使用。|  
|ODBC 硬性中斷連接計數器/秒|每秒發出至伺服器的硬性中斷連接數。 這些是連接共用所發行之伺服器的實際連接。 當您停止系統上的所有用戶端時，此值會從零增加，且連接會開始時間。|  
|每秒 ODBC 軟連接計數器|每秒集區所滿足的連接數目-換句話說，就是從該集區到使用者的連接。 此計數器表示共用是否正常運作。 根據伺服器上的負載，這種情況並不常見，因為這會顯示每秒40-60 個軟連線。|  
|每秒 ODBC 軟中斷連接計數器|應用程式發出的每秒中斷連接數。 當應用程式放開或中斷連線時，會將連接放回集區中。|  
|ODBC 目前作用中的連接計數器|集區中目前正在使用的連接數目。|  
|ODBC 目前可用的連接計數器|集區中目前可用的免費連接數目。 這些是可供使用的即時連接。|  
|目前作用中的集區|目前作用中的集區數目。 此計數器是針對管理連接集區中連接的驅動程式，在 Windows 8 中新增的。 如需詳細資訊，請參閱 [驅動程式感知連接](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)共用。|  
|建立的集區|作用中的集區數目，包括作用中和已移除的集區。 此計數器是針對管理連接集區中連接的驅動程式，在 Windows 8 中新增的。 如需詳細資訊，請參閱 [驅動程式感知連接](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)共用。|  
  
 您必須指定自己的監視參數。 此版本的 ODBC 已包含效能監視的範例。
