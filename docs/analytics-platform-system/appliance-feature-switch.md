---
title: 功能切換 (Analytics Platform System)
description: 顯示有關 Analytics Platform System AU7 中引進的兩個功能參數資訊。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e384a252584fed0e7543a7a4000fc9a70f6533e7
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/25/2018
---
#<a name="appliance-feature-switch"></a>應用裝置功能切換
**功能切換**頁面顯示 Analytics Platform System AU7 導入的兩個功能參數資訊。 若要更新或啟用/停用功能與 Analytics Platform System 設定使用此頁面。 功能參數值的變更需要重新啟動服務。

![DWConig 應用裝置功能切換](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig 應用裝置功能切換") 

##<a name="autostatsenabled-switch"></a>AutoStatsEnabled 交換器
控制自動統計資料功能。 此功能的開關設定為依預設，在升級至 AU7 之後，則為 true。 在升級之後所建立的任何資料庫會繼承，自動建立和非同步更新統計資料。 現有的資料庫，資料庫管理員可以啟用自動統計資料，使用 [變更資料庫] （/ sql/t-sql/statements/alter-database-parallel-data-warehouse）。 如需有關統計資料的詳細資訊，請參閱[統計資料](../relational-databases/statistics/statistics.md)。

##<a name="dmsprocessstopmessagetimeoutinseconds-switch"></a>DmsProcessStopMessageTimeoutInSeconds 交換器
控制當涉及移動資料的查詢被取消時，在忙碌的系統同步處理資料移動服務 (DMS) 要等候的時間。 更新至 AU7 設定此值為 900 秒 （15 分鐘） 預設。 有效範圍為 0 – 3600 秒。
