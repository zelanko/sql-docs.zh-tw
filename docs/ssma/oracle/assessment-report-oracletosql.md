---
title: 評估報表 (OracleToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 168b7465-a6d6-4329-b46e-fc6c5a3f2d9d
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 3a192d86e53b02f1abb46ed5bab590fd974e4a9c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="assessment-report-oracletosql"></a>評估報表 (OracleToSQL)
評估報表視窗中顯示的資料庫物件的轉換結果[!INCLUDE[tsql](../../includes/tsql_md.md)]語法，並且也可幫助您評估複雜度及成本的移轉專案。  
  
若要存取評估的報表，在來源中繼資料總管，轉換選取的物件上按一下滑鼠右鍵**結構描述**或**同義字**，然後選取**建立報表**。  
  
## <a name="options"></a>選項  
  
|||  
|-|-|  
|詞彙|定義|  
|**轉換統計資料**|顯示依陳述式類型的轉換統計資料。 這個窗格會顯示當群組物件，例如結構描述，或沒有程式碼的物件已選取左窗格中。|  
|**依類別分組的物件**|依類別顯示物件的數目。 這個窗格會顯示時，才是群組物件，例如結構描述，或沒有程式碼的物件已選取左窗格中。|  
|**統計資料**|顯示所選物件的轉換統計資料。 只有在左窗格中選取個別物件以程式碼時，此窗格是可見。 您可能必須展開 [**統計資料**，正上方**來源**] 窗格中，若要檢視此窗格。|  
|**Source**|顯示所選物件的 Oracle 程式碼，並反白顯示程式碼，未轉換成[!INCLUDE[tsql](../../includes/tsql_md.md)]。 只有在左窗格中選取個別物件以程式碼時，此窗格是可見。<br /><br />按一下以設定或清除書籤的行號。 使用窗格頂端的按鈕來瀏覽程式碼。|  
|**Target**|顯示產生的轉換[!INCLUDE[tsql](../../includes/tsql_md.md)]選取的物件，並不會被轉換的程式碼的錯誤訊息的程式碼。 只有在左窗格中選取個別物件以程式碼時，此窗格是可見。<br /><br />按一下以設定或清除書籤的行號。 使用窗格頂端的按鈕來瀏覽程式碼。|  
|**訊息窗格**|顯示錯誤、 警告和參考用訊息建立評估報表時所產生的。 訊息會依數字分組。 若要檢視造成此錯誤的程式碼，請按一下**錯誤**，**警告**，或**資訊**，展開圖形的訊息、 分類，然後按一下 訊息。|  
  
