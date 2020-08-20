---
description: 建立測試案例 (SybaseToSQL)
title: 建立測試案例 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: fb3fe4816faeb050a1c4321def0e7dd4e6937bdb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463150"
---
# <a name="creating-test-cases-sybasetosql"></a>建立測試案例 (SybaseToSQL)
使用測試案例嚮導來建立測試。 此嚮導可讓您選擇測試和驗證的物件，以及指定測試參數，以建立測試案例。  
  
## <a name="starting-the-test-case-wizard"></a>啟動測試案例嚮導  
若要啟動測試案例，請從 **[測試器] 功能表按一下**[**新增測試案例**]。  
  
當啟動時，嚮導會根據來源 Sybase 伺服器上) 的專案類型，尋找資料庫 ssmatester2005db 或 ssmatester2008db (。 它是用來儲存輔助物件的測試人員擴充架構。 如果測試案例嚮導找不到 ssmatester2005db 或 ssmatester2008db，則會顯示一個對話方塊視窗，建議您建立測試人員擴充功能資料庫。  (這種情況通常是在第一次執行 SSMA 測試人員期間發生。 )   
  
如果您看到對話方塊視窗，請按一下 [ **是** ]，在來源伺服器上建立 Sybase 測試人員資料庫。 接著會出現一個新的對話方塊視窗，您應該在其中新增一或多個裝置，以找出新的測試人員資料庫。 按一下 [ **新增** ] 以新增裝置。 在 [ **測試人員資料庫的配置空間** ] 對話方塊中，選擇裝置並指定測試人員資料庫所使用的大小。 此外，您可以為資料庫記錄檔設定個別的裝置。 請注意，您必須擁有 Sybase 許可權才能建立資料庫。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>使用 Wizard 建立測試案例的總覽  
建立測試案例的套裝程式含五個步驟：  
  
1.  [&#40;SybaseToSQL&#41;初始化測試案例 ](../../ssma/sybase/initializing-test-cases-sybasetosql.md)。  
  
2.  [選取並設定要測試 &#40;SybaseToSQL&#41;的物件 ](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)。  
  
3.  [選取和設定受影響的物件 &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)。  
  
4.  [自訂呼叫順序 &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)。  
  
5.  [完成測試案例準備 &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[測試遷移的資料庫物件 &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
