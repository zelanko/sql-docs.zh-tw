---
title: 評定報告 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5525d989-024c-402d-9e84-faa4721cc5b9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 72b6171864c0ab801e89d3eba5a19ff61031a81e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253285"
---
# <a name="assessment-report-mysqltosql"></a>評定報告 (MySQLToSQL)
評定報表視窗中顯示的資料庫物件的轉換結果[!INCLUDE[tsql](../../includes/tsql-md.md)]語法，也可以幫助您評估複雜度和成本的移轉專案。  
  
若要存取評估報表中，選取來源的中繼資料檔案總管 中要轉換的物件上按一下滑鼠右鍵**結構描述**，然後選取**建立報表**。  
  
## <a name="options"></a>選項  
  
|||  
|-|-|  
|**詞彙**|**[定義]**|  
|**轉換統計資料**|顯示依陳述式類型的轉換統計資料。 這個窗格會顯示當群組物件，例如結構描述，或在左窗格中選取某物件不需要程式碼。|  
|**依類別分組的物件**|依類別顯示物件的數目。 這個窗格為可見時，才群組物件，例如結構描述，或在左窗格中選取某物件不需要程式碼。|  
|**統計資料**|顯示所選物件的轉換統計資料。 在左窗格中選取具有程式碼的個別物件時才，此窗格是可見的。 您可能必須展開**統計資料**，其正上方**來源** 窗格中，若要檢視此窗格。|  
|**Source**|顯示 MySQL 程式碼，針對選取的物件，並反白顯示 未轉換成的程式碼[!INCLUDE[tsql](../../includes/tsql-md.md)]。 在左窗格中選取具有程式碼的個別物件時才，此窗格是可見的。<br /><br />按一下以設定或清除 書籤的行號。 使用窗格頂端的按鈕來瀏覽程式碼。|  
|**Target**|顯示產生轉換的[!INCLUDE[tsql](../../includes/tsql-md.md)]選取的物件，並不會被轉換的程式碼的錯誤訊息的程式碼。 在左窗格中選取具有程式碼的個別物件時才，此窗格是可見的。<br /><br />按一下以設定或清除 書籤的行號。 使用窗格頂端的按鈕來瀏覽程式碼。|  
|**訊息窗格**|顯示錯誤、 警告和參考用訊息建立評定報表時所產生。 訊息會依數字。 若要檢視造成錯誤的程式碼，請按一下**錯誤**，**警告**，或**資訊**展開訊息的類別目錄，然後按一下 訊息。|  
  
