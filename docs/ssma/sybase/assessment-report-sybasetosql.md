---
title: 評定報告 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c6d83e81253430f243fcaed55b66f6d0de6299ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083497"
---
# <a name="assessment-report-sybasetosql"></a>評定報告 (SybaseToSQL)
評定報表視窗中顯示的資料庫物件的轉換結果[!INCLUDE[tsql](../../includes/tsql-md.md)]語法，也可以幫助您評估複雜度和成本的移轉專案。  
  
若要存取評估報表中，選取來源的中繼資料檔案總管 中要轉換的物件上按一下滑鼠右鍵**資料庫**，然後選取**建立報表**。  
  
## <a name="options"></a>選項。  
**轉換統計資料**  
顯示依陳述式類型的轉換統計資料。 這個窗格為可見時，才群組物件，例如結構描述，或在左窗格中選取某物件不需要程式碼。  
  
**物件類別**  
顯示依物件類型的轉換統計資料。 這個窗格為可見時，才群組物件，例如結構描述，或在左窗格中選取某物件不需要程式碼。  
  
**統計資料**  
顯示所選物件的轉換統計資料。 在左窗格中選取具有程式碼的個別物件時才，此窗格是可見的。 您可能必須展開**統計資料**檢視這個窗格。  
  
**來源瀏覽**  
顯示選取的物件，ASE 程式碼，並反白顯示未轉換成的程式碼[!INCLUDE[tsql](../../includes/tsql-md.md)]。 在左窗格中選取具有程式碼的個別物件時才，此窗格是可見的。  
  
按一下以設定或清除 書籤的行號。 使用窗格頂端的按鈕來瀏覽程式碼。  
  
**目標導覽**  
顯示產生轉換的[!INCLUDE[tsql](../../includes/tsql-md.md)]選取的物件，並不會被轉換的程式碼的錯誤訊息的程式碼。 在左窗格中選取具有程式碼的個別物件時才，此窗格是可見的。  
  
按一下以設定或清除 書籤的行號。 使用窗格頂端的按鈕來瀏覽程式碼。  
  
**訊息窗格**  
顯示錯誤、 警告和資訊訊息時建立評定報表所產生。 訊息會依數字。 若要檢視造成錯誤的程式碼，請按一下**錯誤**，**警告**，或**資訊**展開訊息的類別目錄，然後按一下 訊息。  
  
