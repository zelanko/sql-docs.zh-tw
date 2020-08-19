---
description: '評量報表 (DB2ToSQL) '
title: 評量報表 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e13eba0-e3cf-4205-974f-c00f982061de
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: bea3b1c684457bc794d1b35d3a7985b79da41bef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418514"
---
# <a name="assessment-report-db2tosql"></a>評量報表 (DB2ToSQL) 
[評定報表] 視窗會顯示將資料庫物件轉換成語法的結果 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，也可以協助您估計遷移專案的複雜度和成本。  
  
若要存取評量報告，請選取要在來源中繼資料瀏覽器中轉換的物件，以滑鼠右鍵按一下 [ **架構** ] 或 [ **同義字**]，然後選取 [ **建立報表**]。  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|-|-|  
|**轉換統計資料**|依語句類型顯示轉換統計資料。 在左窗格中選取了群組物件（例如架構）或沒有程式碼的物件時，就會顯示此窗格。|  
|**依類別分類的物件**|依類別顯示物件數目。 只有當群組物件（例如架構）或在左窗格中選取了沒有程式碼的物件時，才會顯示此窗格。|  
|**統計資料**|顯示所選物件的轉換統計資料。 只有在左窗格中選取了具有程式碼的個別物件時，才會顯示此窗格。 您可能必須展開 [ **統計資料**] （位於 [ **來源** ] 窗格正上方）來查看此窗格。|  
|**Source**|顯示所選物件的 DB2 程式碼，並反白顯示未轉換成的程式碼 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 只有在左窗格中選取了具有程式碼的個別物件時，才會顯示此窗格。<br /><br />按一下行號以設定或清除書簽。 使用窗格頂端的按鈕來流覽程式碼。|  
|**Target**|顯示所選物件的轉換結果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，以及未轉換之程式碼的錯誤訊息。 只有在左窗格中選取了具有程式碼的個別物件時，才會顯示此窗格。<br /><br />按一下行號以設定或清除書簽。 使用窗格頂端的按鈕來流覽程式碼。|  
|**訊息窗格**|顯示建立評量報告時所產生的錯誤、警告和資訊訊息。 訊息會依編號分組。 若要查看造成錯誤的程式碼，請按一下 [ **錯誤**]、[ **警告**] 或 [ **資訊**]，展開訊息的類別，然後按一下訊息。|  
  
