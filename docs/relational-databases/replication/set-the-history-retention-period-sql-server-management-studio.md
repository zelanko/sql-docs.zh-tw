---
title: 設定記錄保留週期 (SSMS)
description: 了解如何在 SQL Server Management Studio (SSMS) 中設定散發資料庫記錄保留週期。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- history retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: c288daab-5181-4d4b-ba2a-8a147098e758
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 6f9ada00c3166637ca1c5721b17ed950df58a4e2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "76287195"
---
# <a name="set-the-history-retention-period-sql-server-management-studio"></a>設定記錄保留週期 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  在 [散發資料庫屬性 - \<散發資料庫>] 對話方塊的 [一般] 頁面中指定記錄保留期限。 此設定會控制複寫代理程式記錄的儲存時間。 此頁面可以從 [散發者屬性 - \<散發者>] 對話方塊的 [一般] 頁面取得。 如需存取此對話方塊的詳細資訊，請參閱[檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
### <a name="to-specify-the-history-retention-period"></a>若要指定記錄的保留期限  
  
1.  在 [散發者屬性 - \<散發者>] 對話方塊的 [一般]  頁面上，按一下散發資料庫的屬性按鈕 (**…**)。  
  
2.  在 **[存放複寫效能記錄至少]** 方塊中輸入值。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [設定散發](../../relational-databases/replication/configure-distribution.md)  
  
  
