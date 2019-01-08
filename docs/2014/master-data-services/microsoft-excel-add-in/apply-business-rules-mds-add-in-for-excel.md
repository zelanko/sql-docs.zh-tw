---
title: 套用商務規則 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cd106345-f561-4966-88d3-a69139b2bd78
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 2722e678de98bbfbf5a1181a69101fbe2a9427d8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52797920"
---
# <a name="apply-business-rules-mds-add-in-for-excel"></a>套用商務規則 (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 中，當您想要驗證資料並確認資料是否有效時，請套用商務規則。 您可以更正驗證並且重新發行資料。  
  
> [!NOTE]  
>  資料驗證會在您發行資料時自動進行。 如需詳細資訊，請參閱 [驗證預存程序 &#40;Master Data Services&#41;](../validation-stored-procedure-master-data-services.md)。  
  
## <a name="prerequisites"></a>先決條件  
 若要執行此程序：  
  
-   您必須擁有總管 功能區域的存取權。  
  
-   您必須擁有包含 MDS 管理之資料的使用中工作表。  
  
### <a name="to-apply-business-rules"></a>若要套用商務規則  
  
1.  按一下 [發行和驗證] 群組中的 [套用規則]。  
  
    > [!NOTE]  
    >  單次驗證的成員 (資料列) 數目主要取決於 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]中的設定。 如需詳細資訊，請參閱 [商務規則設定](../system-settings-master-data-services.md#BusinessRules)。  
  
2.  系統會根據商務規則驗證資料，並且顯示兩個狀態資料行。 如果未自動顯示這些資料行，請按一下 [發行和驗證] 群組中的 [顯示狀態] 檢視它們。  
  
## <a name="see-also"></a>另請參閱  
 [發行資料&#40;MDS 增益集的 Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
