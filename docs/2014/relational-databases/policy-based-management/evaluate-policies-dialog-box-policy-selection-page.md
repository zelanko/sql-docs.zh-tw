---
title: 評估原則對話方塊，原則選取頁面 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.runnow.f1
ms.assetid: 20075fbe-0b48-42c8-b747-690f1aa23dcf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6266dd29c3486b6ae4163b15cffbc455eee31c5a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62705131"
---
# <a name="evaluate-policies-dialog-box-policy-selection-page"></a>評估原則對話方塊，原則選取頁面
  使用此對話方塊可評估以原則為基礎的管理原則。 您可以藉由選取 **[評估結果]** 頁面，將原則套用到目標集內不符合原則的項目。  
  
## <a name="options"></a>選項。  
 **來源**  
 指定原則的來源。 若要變更來源，請按一下 [瀏覽]\( **...** ) 按鈕，開啟 **[選取來源]** 對話方塊。  
  
 **檔案**  
 輸入包含以原則為基礎之管理原則的檔案路徑，或是使用 [瀏覽]\( **...** ) 按鈕來選取檔案。  
  
 **Server**  
 選取此選項可連接包含您想要之原則的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體。  
  
 **原則: 原則**  
 按一下此選項可開啟指定之原則的原則對話方塊。  
  
 **原則: 類別目錄**  
 此原則的類別目錄。 這個方塊是唯讀的。  
  
 **原則: Facet**  
 此原則所實作的 Facet。 這個方塊是唯讀的。  
  
 **評估**  
 在評估模式下執行此原則。 這樣會產生目標集的符合報表，但是不會重新設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或是強制未來的符合。  
  
## <a name="possible-errors"></a>可能的錯誤  
  
-   **找不到任何目標**  
  
     目標集可能會基於下列任何一個理由而空白：  
  
    -   此原則指定之型別的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上沒有任何目標。  
  
    -   伺服器限制可能會排除包含目標的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
    -   如果此原則位於資料庫的物件上 (如資料表、檢視表或使用者)，資料庫可能沒有訂閱此原則的類別目錄。  
  
    -   目標集篩選可能會排除這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上的所有目標。  
  
    -   目標伺服器類型與原則評估所在的伺服器類型不同。 例如在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]中，如果您嘗試評估已經針對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]建立的原則，您將會收到空的目標集。  
  
## <a name="see-also"></a>另請參閱  
 [使用以原則為基礎的管理來管理伺服器](administer-servers-by-using-policy-based-management.md)   
 [評估原則對話方塊，評估結果頁面](evaluate-policies-dialog-box-evaluation-results-page.md)  
  
  
