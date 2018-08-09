---
title: 功能切換 (Analytics Platform System)
description: Analytics Platform System AU7 中，會顯示有關導入的兩個功能參數的資訊。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: d9657b1433b0647d7165cb427da6333c0a325583
ms.sourcegitcommit: 0cda14b1151d9bce1253d96dea038c038484f07a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/08/2018
ms.locfileid: "39400921"
---
#<a name="appliance-feature-switch"></a>應用裝置功能參數
**功能切換**頁面會顯示有關導入的兩個功能參數的資訊在 Analytics Platform System 2016-AU7。 使用此頁面來更新或啟用/停用功能和 Analytics Platform System 中的設定。 功能參數值的變更需要重新啟動服務。

![DWConig 設備功能切換](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConig 設備功能參數") 

##<a name="autostatsenabled-switch"></a>AutoStatsEnabled 交換器
控制自動統計資料功能。 此功能開關設定為升級到 AU7 之後的預設值為 true。 升級之後所建立的任何資料庫會繼承自動建立與非同步更新統計資料。 對於現有的資料庫，資料庫系統管理員可以啟用自動統計資料[ALTER DATABASE （平行資料倉儲）](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)。 如需有關統計資料的詳細資訊，請參閱 <<c0> [ 統計資料](../relational-databases/statistics/statistics.md)。

##<a name="dmsprocessstopmessagetimeoutinseconds-switch"></a>DmsProcessStopMessageTimeoutInSeconds 交換器
控制資料移動服務 (DMS) 涉及移動資料的查詢已取消時，在忙碌的系統同步處理所等待的時間。 更新至 AU7 預設會設定此值為 900 秒 （15 分鐘）。 有效範圍為 0 – 3600 秒。
