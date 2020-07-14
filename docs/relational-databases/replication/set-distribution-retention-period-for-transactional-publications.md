---
title: 設定散發保留週期
description: 在 SQL Server Management Studio (SSMS) 中設定散發資料庫內資料的保留週期。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 0324c8424760ba10a7eae2c997cb5dfe3550e625
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767662"
---
# <a name="set-distribution-retention-period-for-transactional-publications"></a>設定交易式發行集的散發保留週期
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  在 [散發資料庫屬性 - \<DistributionDatabase>] 對話方塊中，指定最短散發保留週期和最長散發保留週期。 這會在 [散發者屬性 - \<Distributor>] 對話方塊的 [一般] 頁面上提供。 如需存取此對話方塊的詳細資訊，請參閱[檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
### <a name="to-specify-the-distribution-retention-period"></a>若要指定散發保留期限  
  
1.  在 [散發者屬性 - \<Distributor>] 對話方塊的 [一般] 頁面上，按一下散發資料庫的屬性按鈕 ( **...** )。  
  
2.  若要指定最短散發保留期限，請在 **[至少]** 方塊中輸入值；若要指定最長散發期限，請在 **[但是不能超過]** 方塊中輸入值。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="see-also"></a>另請參閱  
 [[設定散發]](../../relational-databases/replication/configure-distribution.md)   
 [訂閱逾期與停用](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
