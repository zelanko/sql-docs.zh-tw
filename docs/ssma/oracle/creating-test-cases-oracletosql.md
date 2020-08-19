---
description: 建立測試案例 (OracleToSQL)
title: 建立測試案例 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 4f7183089fd67f413515034a557e4b73388f950f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418384"
---
# <a name="creating-test-cases-oracletosql"></a>建立測試案例 (OracleToSQL)
使用測試案例嚮導來建立測試。 此嚮導可讓您選擇測試和驗證的物件，以及指定測試參數，以建立測試案例。  
  
## <a name="starting-the-test-case-wizard"></a>啟動測試案例嚮導  
若要啟動測試案例，請從 **[測試器] 功能表按一下**[**新增測試案例**]。  
  
啟動時，嚮導會尋找來源 Oracle 伺服器上的架構 SSMATESTER_ORACLE。 它是用來儲存輔助物件的測試人員擴充架構。 如果 [測試案例嚮導] 找不到 SSMATESTER_ORACLE，則會顯示一個對話方塊視窗，建議您建立架構。  (這種情況通常是在第一次執行 SSMA 測試人員期間發生。 )   
  
如果您看到對話方塊視窗，請按一下 [ **是** ]，在來源伺服器上建立 SSMATESTER_ORACLE 的架構。 請注意，您必須擁有 Oracle 許可權，才能建立新的使用者，並在這個使用者的架構中建立物件。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>使用 Wizard 建立測試案例的總覽  
建立測試案例的套裝程式含五個步驟：  
  
1.  [&#40;OracleToSQL&#41;初始化測試案例 ](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [選取並設定要測試的物件 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [選取及設定受影響的物件 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [自訂呼叫順序 &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [完成測試案例準備 &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>另請參閱  
[測試遷移的資料庫物件 &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
