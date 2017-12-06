---
title: "建立測試案例 (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 47b8190259408b057962c47e6847123e7560ce94
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="creating-test-cases-sybasetosql"></a>建立測試案例 (SybaseToSQL)
若要建立測試中使用測試案例精靈。 此精靈可讓您藉由選擇測試及驗證過的物件和測試參數建立測試案例。  
  
## <a name="starting-the-test-case-wizard"></a>啟動測試案例精靈  
若要啟動測試案例精靈按一下**新測試案例...** 從**Tester**功能表。  
  
啟動時，精靈會尋找資料庫 ssmatester2005db 或 Sybase 來源伺服器上的 ssmatester2008db （取決於專案類型）。 它是用來儲存輔助物件 Tester 延伸結構描述。 如果測試案例精靈找不到 ssmatester2005db 或 ssmatester2008db，它會顯示對話方塊視窗中，建議將建立測試人員延伸資料庫。 （這種情況通常發生在 SSMA Tester 第一次執行期間。）  
  
如果出現對話方塊視窗中，按一下**是**在來源伺服器上建立 Sybase tester 資料庫。 然後會出現新的對話方塊視窗，您應該在其中加入一個或多個裝置上，找出新的測試資料庫。 按一下**新增**來新增裝置。 在**配置空間，供測試人員資料庫**對話方塊選擇裝置，並指定軟體測試人員資料庫所使用的大小。 此外，您可以設定資料庫記錄檔的個別裝置。 請注意，您必須建立資料庫的 Sybase 權限。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>建立使用精靈的測試案例的概觀  
建立測試案例的程序包含五個步驟：  
  
1.  [初始化測試案例 &#40;SybaseToSQL &#41;](../../ssma/sybase/initializing-test-cases-sybasetosql.md).  
  
2.  [選取並設定測試 &#40; 物件SybaseToSQL &#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md).  
  
3.  [選取並設定受影響的物件 &#40;SybaseToSQL &#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md).  
  
4.  [自訂呼叫順序 &#40;SybaseToSQL &#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md).  
  
5.  [完成測試案例準備 &#40;SybaseToSQL &#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md).  
  
## <a name="see-also"></a>請參閱  
[測試移轉的資料庫物件 &#40;SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
