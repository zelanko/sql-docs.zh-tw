---
title: 進階物件選取項目 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c978fba4-c953-4ed0-a21d-1b38e7225552
author: Shamikg
ms.author: Shamikg
manager: v-pelars
ms.openlocfilehash: 8bc452dff465ca872f094fa7aaaba98612beb135
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287195"
---
# <a name="advanced-object-selection--oracletosql"></a>進階物件選取 (OracleToSQL)
**進階物件部分**對話方塊可讓您使用在 物件名稱的字串與子字串篩選資料庫物件，然後選取或取消選取這些物件。 SSMA 會執行轉換和移轉作業選取的物件。  
  
若要存取此對話方塊中，在 [中繼資料總管] 中，以滑鼠右鍵按一下，然後按**進階物件選取項目**。  
  
當您第一次開啟的對話方塊中時，按一下**顯示子類別目錄項目**顯示已載入專案的中繼資料的所有物件。 然後，您可以輸入字串以篩選的項目。 例如，輸入字串 「 公司 」 顯示名稱中包含該字串的所有項目。  
  
使用此對話方塊之前，您可能想要強制載入所有的中繼資料轉換結構描述，或儲存專案的 SSMA。  
  
## <a name="options"></a>選項。  
**請檢查所有項目**  
將所有的項目旁的核取記號。 在 [中繼資料總管] 中，會立即選取這些項目。  
  
**取消選取所有項目**  
移除所有項目旁的核取記號。 在 [中繼資料總管] 中，會立即清除這些項目。  
  
**清單檢視模式**  
顯示篩選在清單中的項目。  
  
**資料表檢視模式**  
顯示篩選的資料表中的項目。  
  
**顯示只載入的項目**  
切換分類或項目的顯示。 選取此按鈕時，SSMA 就會顯示符合篩選準則以及先前已載入的所有項目。 當未選取此按鈕時，SSMA 會顯示類別目錄資料夾。  
  
**篩選**  
輸入您想要用來篩選項目的字串。 例如，若要尋找所有可用的項目包含字串"ID"的項目名稱，輸入字串 「 識別碼 」 中**篩選** 方塊中。  
  
如果項目符合篩選準則，類別或項目將會出現您輸入的字串。 若要查看符合的項目，我們建議您按一下**顯示只載入的項目** 按鈕。  
  
**清除篩選**  
清除**篩選** 方塊中。  
  
