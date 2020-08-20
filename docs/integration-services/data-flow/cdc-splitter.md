---
description: CDC 分隔器
title: CDC 分隔器 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.cdcsplitter.f1
ms.assetid: 167bc5c6-fa36-439d-987c-b20acd1a77e2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38ecdd11aa4527fee14b558deb05dcfe578f4d84
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457396"
---
# <a name="cdc-splitter"></a>CDC 分隔器

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  CDC 分隔器會將 CDC 來源資料流程中變更資料列的單一流程分割為插入、更新和刪除作業的不同資料流程。 資料流程是根據 `__$operation` 變更資料表中的必要資料行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 及其標準值分割的。  
  
|作業值|輸出|描述|  
|------------------------|------------|-----------------|  
|1|刪除|已刪除的資料列|  
|2|插入|插入的資料列 (在使用 [Net with Merge (淨 (含合併))]**** CDC 模式時無法使用)|  
|3|更新|更新前資料列 (僅在使用 [All with Old Values (全部 (含舊值))]**** CDC 模式時才可使用)|  
|4|更新|更新後資料列 (在更新前之後)|  
|5|更新|合併資料列 (僅在使用 [Net with Merge (淨 (含合併))]**** CDC 模式時才可使用)|  
|其他|錯誤||  
  
 您可以使用分隔器連接到預先定義的 INSERT、DELETE 和 UPDATE 輸出，以供進一步處理。  
  
 CDC 分隔器轉換有一個一般輸入和一個錯誤輸出。  
  
## <a name="error-handling"></a>錯誤處理  
 CDC 分隔器轉換有錯誤輸出。 含 $operation 資料行無效值的輸入資料列是視為錯誤的，會依據輸入的 **ErrorRowDisposition** 屬性來處理。  
  
 此元件的錯誤輸出包含下列輸出資料行：  
  
-   **錯誤碼**：設為 1。  
  
-   **錯誤資料行**：造成錯誤 (用於轉換錯誤) 的來源資料行。  
  
-   **錯誤資料列資料行**：造成錯誤之資料列的輸入資料行。  
  
## <a name="configuring-the-cdc-splitter"></a>設定 CDC 分隔器  
 CDC 分隔器沒有可設定的屬性。  
  
 如需有關使用 CDC 分隔器的詳細資訊，請參閱＜Microsoft SQL Server Integration Services 的 CDC 元件＞。  
  
 **[進階編輯器]** 對話方塊包含可以程式設計方式設定的屬性。  
  
 若要開啟 **[進階編輯器]** 對話方塊：  
  
-   在 **專案的** [資料流程] [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 畫面中，以滑鼠右鍵按一下 CDC 分隔器，然後選取 **[顯示進階編輯器]**。  
  
## <a name="see-also"></a>另請參閱  
 [依據變更類型來導向 CDC 資料流](../../integration-services/data-flow/direct-the-cdc-stream-according-to-the-type-of-change.md)  
  
  
