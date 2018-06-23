---
title: 資料表值物件 (資料行) 屬性 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vdt.designers.properties.QueryViewColumn
ms.assetid: 212d9bcd-aded-4313-a6b9-d7e2270e5954
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c4855f0a6dd583b0dbc92f116cf357203885fd4b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145756"
---
# <a name="table-valued-object-column-properties-visual-database-tools"></a>資料表值物件 (資料行) 屬性 (Visual Database Tools)
  在查詢和檢視表設計工具的 [圖表] 窗格中，選取資料表值物件中的資料行時，就會出現這些屬性。  
  
> [!NOTE]  
>  此主題中的屬性，是依類別目錄的順序排列，而非依字母排列。  
  
> [!NOTE]  
>  您看到的對話方塊與功能表命令，可能會因您所使用的設定或版本，而與說明中所述不同。 若要變更您的設定，請在 [工具] 功能表上選擇 [匯入和匯出設定]。  
  
 **識別類別目錄**  
 展開即可顯示 [名稱] 屬性。  
  
 **名稱**  
 顯示所選取資料行的名稱。  
  
 **查詢設計工具類別**  
 展開即可顯示 [允許 Null]、[定序]、[資料類型]、[長度]、[有效位數]、[小數位數] 和 [大小] 等的屬性。  
  
 **允許 Null**  
 顯示資料行的資料類型是否允許 Null 值。  
  
 **定序**  
 顯示選取之資料行的定序設定。 定序可以在資料表設計師的 [資料行屬性] 索引標籤中設定。  
  
 **資料類型**  
 顯示選取之資料行的資料類型。  
  
 **長度**  
 顯示選取之資料行的資料類型所允許的字元數或位數。 此屬性只適用於以字元為主的資料類型。  
  
> [!NOTE]  
>  針對以位元組為單位的大小，請參閱下列 [大小] 屬性。  
  
 **有效位數**  
 顯示數值資料類型所允許的最大位數數目。 這個屬性會顯示 **0** 來表示非數字的資料類型。  
  
 **小數位數**  
 若為數值資料類型，顯示可在小數點右邊顯示的最大位數數目。 這個值必須小於或等於有效位數。 這個屬性會顯示 **0** 來表示非數字的資料類型。  
  
 **大小**  
 顯示資料行之資料類型所允許的大小 (以位元組為單位)。 例如，nchar 資料類型的長度可能是 10 (字元數)，但是針對 Unicode 字元集，大小就會是 20。  
  
  