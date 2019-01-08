---
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3fd443ff2ad58aa503fac2960016cb55f35b8a7f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52514944"
---
# <a name="creating-test-cases-sybasetosql"></a>建立測試案例 (SybaseToSQL)
使用測試案例精靈以建立測試。 此精靈可讓您建立測試案例，藉由選擇測試並確認物件和測試的參數。  
  
## <a name="starting-the-test-case-wizard"></a>啟動測試實例精靈  
若要啟動測試案例精靈按一下**新測試案例...** 從**Tester**功能表。  
  
啟動時，精靈會尋找資料庫 ssmatester2005db 或 Sybase 來源伺服器上的 ssmatester2008db （取決於專案類型中）。 它是用來儲存輔助物件 Tester 延伸結構描述。 如果 ssmatester2005db 或 ssmatester2008db，找不到 [測試案例] 精靈，它會顯示建立軟體測試人員延伸模組的資料庫所提出的對話方塊視窗。 （這種情況通常發生在 SSMA 軟體測試人員第一次執行期間。）  
  
如果您收到對話方塊視窗中，按一下**是**在來源伺服器上建立 Sybase 軟體測試人員資料庫。 然後會出現新的對話視窗，您應該在其中加入一個或多個裝置上，找出新的軟體測試人員資料庫。 按一下 **新增**來新增裝置。 在  **Tester 資料庫配置空間**對話方塊選擇裝置，並指定測試人員的資料庫所使用的大小。 此外，您可以設定個別的資料庫記錄檔的裝置。 請注意，您必須建立資料庫的 Sybase 權限。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>建立使用精靈的測試案例的概觀  
建立測試案例的程序是由五個步驟所組成：  
  
1.  [將測試案例初始化&#40;SybaseToSQL&#41;](../../ssma/sybase/initializing-test-cases-sybasetosql.md)。  
  
2.  [選取並設定要測試的物件&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)。  
  
3.  [選取並設定受影響的物件&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)。  
  
4.  [自訂呼叫順序&#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)。  
  
5.  [完成測試案例準備&#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)。  
  
## <a name="see-also"></a>另請參閱  
[測試移轉的資料庫物件&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
