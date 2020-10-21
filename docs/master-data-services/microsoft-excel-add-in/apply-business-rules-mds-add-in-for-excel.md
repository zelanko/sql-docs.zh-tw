---
description: 套用商務規則 (適用於 Excel 的 MDS 增益集)
title: 套用商務規則
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cd106345-f561-4966-88d3-a69139b2bd78
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 582c3245d69d1a2bc92b3a4ab3442797116571d9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "92257595"
---
# <a name="apply-business-rules-mds-add-in-for-excel"></a>套用商務規則 (適用於 Excel 的 MDS 增益集)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 中，當您想要驗證資料並確認資料是否有效時，請套用商務規則。 您可以更正驗證並且重新發行資料。  
  
> [!NOTE]  
>  資料驗證會在您發行資料時自動進行。 如需詳細資訊，請參閱[驗證 &#40;Master Data Services&#41;](../../master-data-services/validation-master-data-services.md)。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有總管**** 功能區域的存取權。  
  
-   您必須擁有包含 MDS 管理之資料的使用中工作表。  
  
### <a name="to-apply-business-rules"></a>若要套用商務規則  
  
1.  按一下 [發行和驗證]**** 群組中的 [套用規則]****。  
  
    > [!NOTE]  
    >  單次驗證的成員 (資料列) 數目主要取決於 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]中的設定。 如需詳細資訊，請參閱 [商務規則設定](../../master-data-services/system-settings-master-data-services.md#BusinessRules)。  
  
2.  系統會根據商務規則驗證資料，並且顯示兩個狀態資料行。 如果未自動顯示這些資料行，請按一下 [發行和驗證]**** 群組中的 [顯示狀態]**** 檢視它們。  
  
## <a name="see-also"></a>另請參閱  
 [概觀：從 Excel 匯入資料 &#40;適用於 Excel 的 MDS 增益集&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
