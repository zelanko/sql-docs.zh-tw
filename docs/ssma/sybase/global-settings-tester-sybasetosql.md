---
title: " (測試人員的全域設定)  (SybaseToSQL) |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 6f0b9cea-5a24-4e42-8bbf-c4516b00da23
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f1ebf6d1122db6b28b13c33320dabef520a40f5a
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87931285"
---
# <a name="global-settings-tester-sybasetosql"></a>全域設定 (測試器) (SybaseToSQL)
使用 [**通用設定**] 對話方塊的 [測試人員] 頁面，即可指定 SSMA 測試人員的設定。  
  
若要存取測試人員設定，請在 [**工具**] 功能表上選取 [**通用設定**]，然後按一下左窗格底部的 [**測試人員**]。  
  
## <a name="options"></a>選項。  
**可測試的物件分析**  
此設定指定是否要執行可測試物件的分析。 如果您想要讓 SSMA 測試人員分析並自動檢查相依物件，請選取 **[是]** 。 預設選項群組為 **[是]**。  
  
此設定可使用下列選項：  
  
1.  是  
  
2.  否  
  
**輔助資料表儲存模式**  
此設定會指定如何儲存在測試案例執行期間建立的內部輔助資料表。 您可以針對此特定設定來設定下列選項：  
  
1.  一律刪除  
  
2.  一律儲存  
  
3.  資料表比較失敗時儲存  
  
4.  如果資料表比較失敗，詢問使用者  
  
預設選項群組為： [**永遠刪除**]。  
  
**執行資料復原**  
此設定會指定是否要在每個測試案例執行之後執行復原操作。 預設選項群組為 [**否**]。  
  
此設定可使用下列選項：  
  
1.  是  
  
2.  否  
  
**第一次失敗後停止測試執行**  
此設定會指定是否要在執行時發生錯誤時，停止目前正在執行的測試案例。 預設選項群組為 **[是]**。  
  
此設定可使用下列選項：  
  
1.  是  
  
2.  否  
  
## <a name="see-also"></a>另請參閱  
[完成測試案例準備 &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)  
  
