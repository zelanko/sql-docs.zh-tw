---
title: 資料行對應 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.columnmapandtransform.f1
ms.assetid: eadc54a6-f936-4ffc-91d7-fbfd2bdcab93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c1d381ec773499fdcf018375c7a51740880d3d9b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436785"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>資料行對應 (SQL Server 匯入和匯出精靈)
  使用 [資料**行**對應] 對話方塊，即可編輯轉換參數。  
  
> [!NOTE]  
>  當您選取 [資料表複製] 選項時，並不必複製資料表中的所有資料行。 **\<ignore>** 針對您要略過的資料行，在此對話方塊的 [**目的地**] 資料行中選取。  
  
 若要深入瞭解此嚮導，請參閱[SQL Server 匯入和匯出嚮導](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要瞭解用來啟動精靈的選項，以及成功執行嚮導所需的許可權，請參閱[執行 SQL Server 匯入和匯出嚮導](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項  
 **Source**  
 識別選取的來源資料表、檢視，或查詢。  
  
 **Destination**  
 識別選取的目的地資料表、檢視，或查詢。  
  
 **建立目的地資料表/檔案**  
 如果目的地資料表不存在，請指定是否要建立目的地資料表。  
  
 **刪除目的地資料表/檔案中的資料列**  
 指定在載入新資料之前，是否要清除現有資料表中的資料。  
  
 **將資料列附加至目的地資料表/檔案**  
 指定是否要將新資料附加到現有資料表中已存在的資料後面。  
  
 **編輯 SQL**  
 使用 [**建立資料表的 SQL 語句**] 對話方塊中的 [預設] 語句，或針對您的用途加以修改。 如果修改此陳述式，您還必須對資料表對應進行相關的變更。  
  
 **卸除並重新建立目的地資料表**  
 選擇此選項即可覆寫目的地資料表。 只有在您使用精靈來建立目的地資料表時，才能使用這個選項。 目的地資料表只有在您儲存精靈所建立的封裝，然後再次執行封裝時才會卸除並重建。  
  
 **啟用識別插入**  
 選擇此選項即可允許將來源資料中的現有識別值，插入目的地資料表裡的識別欄位中。 依預設，目的地識別欄位並不允許此動作。  
  
 **對應**  
 顯示資料來源中的每個資料行如何對應至目的地中的資料行。  
  
 這份清單具有下列資料行：  
  
 **Source**  
 檢視您可以為其設定轉換參數的每個來源資料行。  
  
 **Destination**  
 指定在進行複製作業的期間，您是否想要忽略某資料行。 您可以 **\<ignore>** 針對想要略過的資料行，在此資料行中選取，只複製資料行的子集。 在對應資料行之前，您必須忽略不會加以對應的所有資料行。  
  
 **型別**  
 選取資料行的資料類型。  
  
 **可為 Null**  
 指定資料行是否允許有 Null 值。  
  
 **大小**  
 指定資料行中的字元數目。  
  
 **有效位數**  
 參考數字的位數，來指定所顯示資料的有效位數。  
  
 **縮放比例**  
 參考小數的位數，來指定所顯示資料的小數位數。  
  
  
