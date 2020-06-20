---
title: 設定交易式發行集的散發保留週期（SQL Server Management Studio） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a68f092c63e75196ab82a81d2a8ca36d13142813
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055669"
---
# <a name="set-the-distribution-retention-period-for-transactional-publications-sql-server-management-studio"></a>設定交易式發行集的散發保留週期 (SQL Server Management Studio)
  在 [**散發資料庫屬性- \<DistributionDatabase> ** ] 對話方塊中，指定最小散發保留期限和最大散發保留期限。 這可從 [散發者**屬性- \<Distributor> ** ] 對話方塊的 [**一般**] 頁面取得。 如需存取此對話方塊的詳細資訊，請參閱[檢視及修改散發者和發行者屬性](view-and-modify-distributor-and-publisher-properties.md)。  
  
### <a name="to-specify-the-distribution-retention-period"></a>若要指定散發保留期限  
  
1.  在 [散發者**屬性- \<Distributor> ** ] 對話方塊的 [**一般**] 頁面上，按一下散發資料庫的屬性按鈕（**...**）。  
  
2.  若要指定最短散發保留期限，請在 **[至少]** 方塊中輸入值；若要指定最長散發期限，請在 **[但是不能超過]** 方塊中輸入值。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [設定散發](configure-distribution.md)   
 [訂閱逾期與停用](subscription-expiration-and-deactivation.md)  
  
  
