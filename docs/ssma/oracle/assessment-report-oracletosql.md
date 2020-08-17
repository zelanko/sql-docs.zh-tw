---
description: 評定報告 (OracleToSQL)
title: 評量報表 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 168b7465-a6d6-4329-b46e-fc6c5a3f2d9d
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 955c87838f92f15f22e937829f95a34ad8cccdad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88320594"
---
# <a name="assessment-report-oracletosql"></a>評定報告 (OracleToSQL)
[評定報表] 視窗會顯示將資料庫物件轉換成語法的結果 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，也可以協助您估計遷移專案的複雜度和成本。  
  
若要存取評量報告，請選取要在來源中繼資料瀏覽器中轉換的物件，以滑鼠右鍵按一下 [ **架構** ] 或 [ **同義字**]，然後選取 [ **建立報表**]。  
  
## <a name="options"></a>選項。  
  
|詞彙|定義|  
|-|-|  
|**轉換統計資料**|依語句類型顯示轉換統計資料。 在左窗格中選取了群組物件（例如架構）或沒有程式碼的物件時，就會顯示此窗格。|  
|**依類別分類的物件**|依類別顯示物件數目。 只有當群組物件（例如架構）或在左窗格中選取了沒有程式碼的物件時，才會顯示此窗格。|  
|**統計資料**|顯示所選物件的轉換統計資料。 只有在左窗格中選取了具有程式碼的個別物件時，才會顯示此窗格。 您可能必須展開 [ **統計資料**] （位於 [ **來源** ] 窗格正上方）來查看此窗格。|  
|**Source**|顯示所選物件的 Oracle 程式碼，並反白顯示未轉換成的程式碼 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 只有在左窗格中選取了具有程式碼的個別物件時，才會顯示此窗格。<br /><br />按一下行號以設定或清除書簽。 使用窗格頂端的按鈕來流覽程式碼。|  
|**Target**|顯示所選物件的轉換結果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，以及未轉換之程式碼的錯誤訊息。 只有在左窗格中選取了具有程式碼的個別物件時，才會顯示此窗格。<br /><br />按一下行號以設定或清除書簽。 使用窗格頂端的按鈕來流覽程式碼。|  
|**訊息窗格**|顯示建立評量報告時所產生的錯誤、警告和資訊訊息。 訊息會依編號分組。 若要查看造成錯誤的程式碼，請按一下 [ **錯誤**]、[ **警告**] 或 [ **資訊**]，展開訊息的類別，然後按一下訊息。|  
  
