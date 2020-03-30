---
title: 匯入原則對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.importpolicy.f1
ms.assetid: 78ab5f6e-2f13-4788-937e-8892ef4e2345
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 807eec350627d64a642abc1043977d67069cc0d4
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68087228"
---
# <a name="import-policies-dialog-box"></a>匯出原則對話方塊
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
 [使用原則式管理來管理伺服器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [匯入原則式管理原則](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md)   
 [匯出原則式管理原則](../../relational-databases/policy-based-management/export-a-policy-based-management-policy.md)  
  
  
