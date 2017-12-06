---
title: "評估報表 (AccessToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
caps.latest.revision: "14"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3dcc3a4b1af7a6bbd815a95086e819f5c3c6fc6
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="assessment-report-accesstosql"></a>評估報表 (AccessToSQL)
評估報表視窗中顯示的資料庫物件的轉換結果[!INCLUDE[tsql](../../includes/tsql_md.md)]語法，並且也可幫助您評估複雜度及成本的移轉專案。  
  
若要建立評估報表中，選取來源中繼資料總管，在轉換的物件上按一下滑鼠右鍵**資料庫**，然後選取**建立報表**。 您也會自動顯示這份報表之後您將結構描述的轉換。 不過，報表名稱將會轉換報告。 如需詳細資訊，請參閱[專案設定 (GUI) （SSMA 常見）](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
## <a name="options"></a>選項。  
**總管窗格**  
包含評估報表中的物件階層。 展開資料夾，以檢視個別物件和子元件。 當您按一下類別或物件時，該類別或物件的轉換統計資料會出現在 [詳細資料] 窗格中。  
  
**詳細資料窗格**  
顯示所選物件的統計資料或錯誤和警告訊息的轉換。 例如，如果選取 「 資料表 」 資料夾時，詳細資料窗格會顯示外部索引鍵、 索引、 主索引鍵和資料表的已轉換的數字。  
  
**訊息窗格**  
顯示錯誤、 警告和評估報表建立時所產生的資訊訊息。 訊息會依數字分組。  
  
若要檢視訊息詳細資料，請按一下**錯誤**，**警告**，或**訊息**，然後展開 訊息。 SSMA 會顯示具有這項錯誤的物件清單。 按一下以顯示物件所有轉換的詳細資料物件。  
  
## <a name="see-also"></a>請參閱  
[使用者介面 Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
