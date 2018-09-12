---
title: 匯入原則對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.importpolicy.f1
ms.assetid: 78ab5f6e-2f13-4788-937e-8892ef4e2345
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: de3e57c1d1e0072ef4ceb489a79191525b3260d0
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43817672"
---
# <a name="import-policies-dialog-box"></a>匯出原則對話方塊
  使用此對話方塊，可將儲存為 XML 檔案的一個或多個原則 (和其參考條件) 匯入到目前的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體中。  
  
## <a name="options"></a>選項。  
 **要匯入的檔案**  
 若要從 XML 檔案匯入原則，請輸入檔案的路徑和名稱，或是使用 [瀏覽]\( **...** ) 按鈕。  
  
 **以匯入的項目取代重複的項目**  
 選取此選項可覆寫任何同名的現有原則或條件 (如果這個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體上已經有該原則或條件存在)。 具有相依原則的條件無法被覆寫，除非該相依原則也一起被覆寫。 如果未選取這個選項，使用相同條件運算式的現有條件將不會產生錯誤。  
  
 **原則狀態**  
 選取匯入的原則所要的狀態：  
  
-   **匯入時保留原則狀態**  
  
-   **匯入時啟用所有原則**  
  
-   **匯入時停用所有原則**  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來管理伺服器](administer-servers-by-using-policy-based-management.md)   
 [匯入原則式管理原則](import-a-policy-based-management-policy.md)   
 [匯出原則式管理原則](export-a-policy-based-management-policy.md)  
  
  
