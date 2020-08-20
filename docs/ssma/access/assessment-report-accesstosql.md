---
description: '評量報表 (AccessToSQL) '
title: 評量報表 (AccessToSQL) |Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 5f1058947591fdd454ce181b2d098f88b183cbe1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497824"
---
# <a name="assessment-report-accesstosql"></a>評量報表 (AccessToSQL) 
[評定報表] 視窗會顯示將資料庫物件轉換成語法的結果 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，也可以協助您估計遷移專案的複雜度和成本。  
  
若要建立評量報告，請在 [來源中繼資料瀏覽器] 中選取要轉換的物件，以滑鼠右鍵按一下 [ **資料庫**]，然後選取 [ **建立報告**]。 您也可以在轉換架構之後自動顯示這份報表。 不過，報表名稱將會是轉換報表。 如需詳細資訊，請參閱 [ (GUI 的專案設定)  (SSMA 一般) ](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
## <a name="options"></a>選項。  
**[總管] 窗格**  
包含評量報告中的物件階層。 展開資料夾以查看個別物件和子元件。 當您按一下類別或物件時，[詳細資料] 窗格中會顯示該類別或物件的轉換統計資料。  
  
**詳細資料窗格**  
顯示所選物件的轉換統計資料或錯誤和警告訊息。 例如，如果選取 [資料表] 資料夾，[詳細資料] 窗格會顯示已轉換的外鍵、索引、主鍵和資料表的數目。  
  
**訊息窗格**  
顯示建立評量報告時所產生的錯誤、警告和資訊訊息。 訊息會依編號分組。  
  
若要查看訊息詳細資料，請按一下 [ **錯誤**]、[ **警告**] 或 [ **訊息**]，然後展開訊息。 SSMA 會顯示有此錯誤的物件清單。 按一下物件以顯示物件的所有轉換詳細資料。  
  
## <a name="see-also"></a>另請參閱  
[消費者介面參考 (存取) ](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
