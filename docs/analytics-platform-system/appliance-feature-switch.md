---
title: 功能切換
description: 顯示分析平臺系統 AU7 中引進的兩個功能參數的相關資訊。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 8642f27a329da8819acf0ab99a648c4979ed40d0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401457"
---
# <a name="appliance-feature-switches"></a>裝置功能切換

[**功能切換**] 頁面會顯示在分析平臺系統 AU7 和更新版本中引進之功能參數的相關資訊。 使用此設定頁面來更新或啟用/停用分析平臺系統中的功能和設定。

> [!NOTE]
> 功能切換值的變更需要重新開機服務。

![DWConfig 裝置功能切換](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "DWConfig 裝置功能切換")

## <a name="autostatsenabled"></a>AutoStatsEnabled

控制自動統計資料功能。 在升級至 AU7 之後，此功能參數預設會設定為 true。 升級之後建立的任何資料庫都會繼承自動建立和非同步更新統計資料。 針對現有的資料庫，資料庫管理員可以使用[ALTER database （平行處理資料倉儲）](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)啟用自動統計資料。 如需統計資料的詳細資訊，請參閱[統計資料](../relational-databases/statistics/statistics.md)。

## <a name="maxdopforinsertqueries"></a>MaxDOPForInsertQueries

可讓您針對插入/選取作業挑選大於1的 maxdop 設定。 此設定的選項為0、1、2和4，預設值為1。

## <a name="optimizecommonsubexpressions"></a>OptimizeCommonSubExpressions

藉由排除 SQL 查詢最佳化工具中通用子運算式的資料移動，來改善查詢效能。 您可以在[這裡](common-sub-expression-elimination.md)找到這項功能的詳細說明。

## <a name="usecatalogqueries"></a>UseCatalogQueries

針對某些中繼資料呼叫使用目錄物件，而不使用 SMO，已顯示效能改進。 根據預設，在 CU 7.1 中設定為 true，此參數會控制該行為。

## <a name="dmsprocessstopmessagetimeoutinseconds"></a>DmsProcessStopMessageTimeoutInSeconds

控制與資料移動相關的查詢取消時，資料移動服務（DMS）等候在忙碌系統上進行同步處理的時間。 [更新至 AU7] 預設會將此值設為900秒（15分鐘）。 有效範圍為 0-3600 秒。
