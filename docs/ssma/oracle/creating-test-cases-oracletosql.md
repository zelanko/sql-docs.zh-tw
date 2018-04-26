---
title: 建立測試案例 (OracleToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 7401e9b5de144160abb84388cb9dc1f8e144f357
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="creating-test-cases-oracletosql"></a>建立測試案例 (OracleToSQL)
若要建立測試中使用測試案例精靈。 此精靈可讓您藉由選擇測試及驗證過的物件和測試參數建立測試案例。  
  
## <a name="starting-the-test-case-wizard"></a>啟動測試案例精靈  
若要啟動測試案例精靈按一下**新測試案例...** 從**Tester**功能表。  
  
啟動時，精靈就會尋找結構描述 SSMATESTER_ORACLE 來源 Oracle 伺服器上。 它是用來儲存輔助物件 Tester 延伸結構描述。 如果測試案例精靈找不到 SSMATESTER_ORACLE，它會顯示建立結構描述所提出的對話方塊視窗。 （這種情況通常發生在 SSMA Tester 第一次執行期間。）  
  
如果出現對話方塊視窗中，按一下**是**來源伺服器上建立 SSMATESTER_ORACLE 結構描述。 請注意，您必須建立新的使用者和此使用者的結構描述中建立物件的 Oracle 權限。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>建立使用精靈的測試案例的概觀  
建立測試案例的程序包含五個步驟：  
  
1.  [初始化測試案例&#40;OracleToSQL&#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [選取和設定測試的物件&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [選取並設定受影響的物件&#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [自訂呼叫順序&#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [完成測試案例準備&#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[測試移轉的資料庫物件&#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
