---
title: 全域設定 （測試器） (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4acc0f2a-85ba-4c99-856a-89030f5c418e
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: f7e421774d3a09622835b181d5c053c994e905ee
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264406"
---
# <a name="global-settings-tester-oracletosql"></a>全域設定 (測試器) (OracleToSQL)
使用軟體測試人員頁面**全域設定**對話方塊來指定設定 SSMA 軟體測試人員。  
  
若要存取 [測試設定] 中，在**工具**功能表上，選取**全域設定**，然後按一下**軟體測試人員**在左窗格底部。  
  
## <a name="options"></a>選項。  
**可測試的物件分析**  
此設定指定是否要執行之測試的物件的分析。 選取 **是**如果您想要分析，並自動檢查相依物件的 SSMA 測試人員。 設定預設選項是**是**。  
  
此設定有下列選項：  
  
1.  是  
  
2.  否  
  
**儲存模式的輔助資料表**  
此設定會指定如何儲存測試案例執行期間建立的內部輔助資料表。 針對此特定的設定可以設定下列選項：  
  
1.  永遠刪除  
  
2.  永遠儲存  
  
3.  如果資料表的比較無法，儲存  
  
4.  要求使用者資料表的比較失敗時  
  
設定預設選項是：**永遠刪除**。  
  
**執行資料復原**  
此設定指定是否要在執行每個測試案例後執行復原作業。 設定預設選項是**No**。  
  
此設定有下列選項：  
  
1.  是  
  
2.  否  
  
**停止後第一次失敗的測試執行**  
此設定會指定是否要停止目前執行的測試案例，如果執行時，發生錯誤。 設定預設選項是**是**。  
  
此設定有下列選項：  
  
1.  是  
  
2.  否  
  
## <a name="see-also"></a>另請參閱  
[完成測試案例準備&#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
