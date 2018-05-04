---
title: 全域設定 （測試人員） (SybaseToSQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 6f0b9cea-5a24-4e42-8bbf-c4516b00da23
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d2808ff0e9fbbc99f8592ab37e676fdbb6474569
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="global-settings-tester-sybasetosql"></a>全域設定 （測試人員） (SybaseToSQL)
使用的測試人員頁面**通用設定**對話方塊來指定設定 SSMA 軟體測試人員。  
  
若要存取的測試設定，在**工具**功能表上，選取**通用設定**，按一下**軟體測試人員**在左窗格的底部。  
  
## <a name="options"></a>選項  
**可測試的物件分析**  
此設定指定是否要執行分析的可測試的物件。 選取**是**如果您想要分析並自動檢查相依物件 SSMA 軟體測試人員。 設定預設選項是**是**。  
  
此設定有下列選項：  
  
1.  是  
  
2.  否  
  
**儲存模式的輔助資料表**  
此設定指定如何儲存測試案例執行期間建立的內部輔助資料表。 此特定的設定可以設定下列選項：  
  
1.  永遠刪除  
  
2.  永遠儲存  
  
3.  如果資料表的比較無法，儲存  
  
4.  要求使用者資料表的比較失敗時  
  
設定預設選項是：**永遠刪除**。  
  
**執行資料復原**  
此設定指定是否要執行每個測試案例後，執行復原作業。 設定預設選項是**否**。  
  
此設定有下列選項：  
  
1.  是  
  
2.  否  
  
**測試之後停止執行第一次失敗**  
此設定指定是否要停止目前正在執行測試案例中，如果執行時，發生錯誤。 設定預設選項是**是**。  
  
此設定有下列選項：  
  
1.  是  
  
2.  否  
  
## <a name="see-also"></a>另請參閱  
[完成測試案例準備&#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)  
  
