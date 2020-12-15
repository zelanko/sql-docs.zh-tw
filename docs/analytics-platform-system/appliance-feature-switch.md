---
title: 功能切換
description: 顯示在 Analytics Platform System AU7 中引進的兩個功能切換的相關資訊。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7'
ms.openlocfilehash: cd9e93b1b734737eda94501df7a30a07c8f8042a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97420261"
---
# <a name="appliance-feature-switches"></a>裝置功能參數

[ **功能切換** ] 頁面會顯示在 Analytics PLATFORM System AU7 和更新版本中所引進之功能參數的相關資訊。 使用此設定頁面來更新或啟用/停用 Analytics Platform System 中的功能和設定。

> [!NOTE]
> 功能切換值的變更需要重新開機服務。

![Dwconfig 應用裝置功能切換](media/feature-switch/SQL_Server_PDW_DWConfig_feature_switch.png "Dwconfig 應用裝置功能切換")

## <a name="autostatsenabled"></a>>autostatsenabled

控制自動統計資料功能。 升級至 AU7 之後，此功能參數預設會設定為 true。 升級之後建立的任何資料庫都會繼承自動建立和非同步更新統計資料。 針對現有的資料庫，資料庫管理員可以使用 [ALTER database (平行資料倉儲) ](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)來啟用自動統計資料。 如需統計資料的詳細資訊，請參閱 [統計資料](../relational-databases/statistics/statistics.md)。

## <a name="maxdopforinsertqueries"></a>MaxDOPForInsertQueries

允許您針對插入/選取作業挑選大於1的 maxdop 設定。 此設定的選項為0、1、2和4，預設值為1。

## <a name="optimizecommonsubexpressions"></a>OptimizeCommonSubExpressions

藉由消除 SQL 查詢最佳化工具中一般子運算式的資料移動，來改善查詢效能。 您可以在 [這裡](common-sub-expression-elimination.md)找到這項功能的詳細說明。

## <a name="usecatalogqueries"></a>UseCatalogQueries

針對某些中繼資料呼叫使用目錄物件，而不使用 SMO，會顯示效能改進。 在 CU 7.1 中預設設定為 true，此參數會控制該行為。

## <a name="dmsprocessstopmessagetimeoutinseconds"></a>DmsProcessStopMessageTimeoutInSeconds

控制在取消涉及資料移動的查詢時， (DMS) 等候在忙碌系統上同步處理的時間資料移動服務。 更新至 AU7 預設會將此值設定為900秒 (15 分鐘) 。 有效範圍是 0-3600 秒。
