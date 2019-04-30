---
title: 設計查詢 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptwizard.designquery.f1
ms.assetid: 2dad800f-10a1-453c-8761-2935b9826d84
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 46e3db8807e8e730ce0476f27d2dad0e3a64eaf4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63165161"
---
# <a name="design-the-query"></a>設計查詢
  使用報表精靈的這個頁面，即可透過手動輸入查詢、使用查詢產生器以互動方式建立查詢或從其他報表匯入查詢，藉以建立查詢。  
  
 您在 [選取資料來源] 頁面 (報表精靈中之前的頁面) 上所選擇的資料來源類型會決定您可以在這個頁面上輸入的查詢。 例如，如果資料來源類型為 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，您就可以輸入 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式或預存程序名稱。 如果資料來源類型為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，則 [查詢] 窗格會停用，而且您無法直接輸入查詢。 您可以使用「查詢產生器」來指定查詢。  
  
## <a name="options"></a>選項。  
 **查詢字串**  
 輸入查詢，以擷取要在報表中使用的資料。  
  
 **查詢產生器**  
 按一下 [查詢產生器] 即可為資料來源開啟查詢設計工具，或從其他報表匯入查詢。  
  
 如需有關查詢設計工具的詳細資訊，請參閱＜ [Reporting Services Query Designers](../../2014/reporting-services/reporting-services-query-designers.md)＞。  
  
## <a name="example"></a>範例  
 資料來源類型**Microsoft SQL Server**，下列查詢會擷取最後一個名稱，從一份[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]資料庫`Person`資料表。  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 資料來源類型**Microsoft SQL Server**，下列查詢會執行[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]預存程序`uspGetEmployeeManagers`之員工識別碼的數字 1:  
  
```  
EXEC uspgetEmployeeManagers '1';  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表精靈說明](../../2014/reporting-services/report-wizard-help.md)   
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
