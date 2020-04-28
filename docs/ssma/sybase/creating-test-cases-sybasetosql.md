---
title: 建立測試案例（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: b3f54a38ae995dd2c83fd36647393f81b802fde2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67948456"
---
# <a name="creating-test-cases-sybasetosql"></a>建立測試案例 (SybaseToSQL)
使用 [測試案例] Wizard 建立測試。 此 wizard 可讓您藉由選擇已測試和已驗證的物件，並藉由指定測試參數來建立測試案例。  
  
## <a name="starting-the-test-case-wizard"></a>啟動測試案例嚮導  
若要啟動測試案例，請按一下 [測試**人員**] 功能表中的 [**新增測試案例 ...** ]。  
  
啟動時，嚮導會尋找來源 Sybase 伺服器上的資料庫 ssmatester2005db 或 ssmatester2008db （視專案類型而定）。 這是用來儲存輔助物件的測試人員延伸模組架構。 如果測試案例 Wizard 找不到 ssmatester2005db 或 ssmatester2008db，就會顯示一個對話方塊視窗，建議您建立測試人員擴充資料庫。 （這種情況通常會在第一次執行 SSMA 測試器時發生）。  
  
如果您看到交談視窗，請按一下 [**是**]，在來源伺服器上建立 Sybase 測試者資料庫。 接著會出現一個新的對話方塊視窗，您應該在其中新增一或多個要尋找新測試人員資料庫的裝置。 按一下 [**新增**] 以新增裝置。 在 [**測試人員資料庫的配置空間**] 對話方塊中，選擇裝置，然後指定測試人員資料庫所使用的大小。 此外，您可以為資料庫記錄設定不同的裝置。 請注意，您必須擁有 Sybase 許可權才能建立資料庫。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>使用 Wizard 建立測試案例的總覽  
建立測試案例的套裝程式含五個步驟：  
  
1.  [&#40;SybaseToSQL&#41;初始化測試案例](../../ssma/sybase/initializing-test-cases-sybasetosql.md)。  
  
2.  [選取並設定要測試的物件 &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)。  
  
3.  [選取並設定受影響的物件 &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)。  
  
4.  [自訂呼叫順序 &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)。  
  
5.  [完成測試案例準備 &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[&#40;SybaseToSQL&#41;測試遷移的資料庫物件](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
