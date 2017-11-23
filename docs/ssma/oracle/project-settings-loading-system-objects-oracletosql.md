---
title: "專案設定 （載入系統物件） (OracleToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9418cb34-d869-4d24-95b3-6cb9db949bb0
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: ffd350a1f77f6e61585c97286fc7e2f86f7a85c2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="project-settingsloading-system-objects-oracletosql"></a>專案設定 （載入系統物件） (OracleToSQL)
[載入系統物件] 頁面的**專案設定** 對話方塊可讓您指定哪些 Oracle 系統物件 SSMA 會將轉換和載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
[載入系統物件] 窗格位於**專案設定**和**預設專案設定**對話方塊：  
  
-   若要指定所有的 SSMA 專案設定**工具**功能表上，選取**預設專案設定**，選取移轉專案類型，不需要檢視或變更設定**移轉的目標版本**下拉式清單按一下**一般**左的窗格中，然後再按一下底部**載入系統物件**。  
  
-   若要指定目前的專案中，設定**工具**功能表上，選取**專案設定**，按一下 **一般**左的窗格中，然後再按一下底部**載入系統物件**。  
  
## <a name="default-settings"></a>預設值  
系統物件的轉換會耗用系統資源，並花的時間。 若要改善效能，SSMA 只選取最常使用的系統物件，如下列清單所示：  
  
-   SYS。DBMS_OUTPUT  
  
-   SYS。DBMS_PIPE  
  
-   SYS。DBMS_UTILITY  
  
-   SYS。標準  
  
-   SYS。UTL_FILE  
  
-   SYS。DBMS_LOB  
  
-   SYS。DBMS_SQL  
  
-   SYS。DBMS_SESSION  
  
如果 Oracle 物件參考其他系統物件，您應該選取這些物件。 如果您未選取 Oracle 資料庫物件所參考的系統物件，SSMA 會報告轉換錯誤。 如果您收到因遺漏的系統物件的轉換錯誤，請在此對話方塊中選取遺漏的物件。 接著，您可以重複視需要轉換。  
  
