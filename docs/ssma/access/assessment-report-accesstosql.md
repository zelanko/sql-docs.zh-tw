---
title: 評定報告 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1278552f1bfe1ccfb7ab250f843e86c62e63440b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62651078"
---
# <a name="assessment-report-accesstosql"></a>評定報告 (AccessToSQL)
評定報表視窗中顯示的資料庫物件的轉換結果[!INCLUDE[tsql](../../includes/tsql-md.md)]語法，也可以幫助您評估複雜度和成本的移轉專案。  
  
若要建立的評估報告，將來源中繼資料總管 中，選取物件上按一下滑鼠右鍵**資料庫**，然後選取**建立報表**。 您也會自動顯示這份報告之後您將結構描述的轉換。 不過，報表名稱將會轉換報告。 如需詳細資訊，請參閱 <<c0> [ 專案設定 (GUI) （SSMA 常見）](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
## <a name="options"></a>選項。  
**檔案總管 窗格**  
包含評估報表中的物件階層。 展開以檢視個別物件和子元件的資料夾。 當您按一下類別或物件時，該類別或物件的轉換統計資料會出現在 [詳細資料] 窗格中。  
  
**詳細資料窗格**  
顯示轉換所選物件的統計資料或錯誤和警告訊息。 比方說，如果選取 [資料表] 資料夾時，[詳細資料] 窗格會顯示外部索引鍵、 索引、 主索引鍵和資料表的已轉換的數字。  
  
**訊息窗格**  
顯示錯誤、 警告和資訊訊息時建立評定報表所產生。 訊息會依數字。  
  
若要檢視訊息詳細資料，請按一下**錯誤**，**警告**，或**訊息**，然後展開 訊息。 SSMA 會顯示具有這項錯誤的物件清單。 按一下以顯示物件的所有轉換詳細資訊的物件。  
  
## <a name="see-also"></a>另請參閱  
[使用者介面 Reference(Access)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
