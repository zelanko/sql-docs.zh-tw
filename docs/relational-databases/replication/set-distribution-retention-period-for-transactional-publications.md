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
ms.openlocfilehash: d699eb502d99818926e92ff07a8fc16248aeee3d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76287205"
---
# <a name="set-distribution-retention-period-for-transactional-publications"></a>設定交易式發行集的散發保留週期
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  在 [散發資料庫屬性 - **散發資料庫>]\<** 對話方塊中，指定最短和最長散發保留期限。 這可以從 [散發者屬性 - **散發者>]** **對話方塊的 [一般]\<** 頁面取得。 如需存取此對話方塊的詳細資訊，請參閱[檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
### <a name="to-specify-the-distribution-retention-period"></a>若要指定散發保留期限  
  
1.  在 [散發者屬性 - **散發者>]** **對話方塊的 [一般]\<** 頁面上，按一下散發資料庫的屬性按鈕 ( **...** )。  
  
2.  若要指定最短散發保留期限，請在 **[至少]** 方塊中輸入值；若要指定最長散發期限，請在 **[但是不能超過]** 方塊中輸入值。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="see-also"></a>另請參閱  
 [[設定散發]](../../relational-databases/replication/configure-distribution.md)   
 [訂閱逾期與停用](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
