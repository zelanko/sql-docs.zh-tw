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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 221fdaaeae61b3005fbbe0088ce4270fd4b6c2b5
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782670"
---
# <a name="column-mappings-sql-server-import-and-export-wizard"></a>資料行對應 (SQL Server 匯入和匯出精靈)
  使用**資料行對應**對話方塊，即可編輯轉換參數。  
  
> [!NOTE]  
>  當您選取 [資料表複製] 選項時，並不必複製資料表中的所有資料行。 選取  **\<忽略 >** 中**目的地**的這個對話方塊中，針對您想要跳過的資料行的資料行。  
  
 若要深入了解此精靈，請參閱[SQL Server 匯入和匯出精靈](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要深入了解啟動精靈，以及成功執行精靈所需的權限的選項，請參閱[執行 SQL Server 匯入和匯出精靈](start-the-sql-server-import-and-export-wizard.md)。  
  
 「SQL Server 匯入和匯出精靈」的用途在於將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="options"></a>選項。  
 **Source**  
 識別選取的來源資料表、檢視，或查詢。  
  
 **目的地**  
 識別選取的目的地資料表、檢視，或查詢。  
  
 **建立目的地資料表/檔案**  
 如果目的地資料表不存在，請指定是否要建立目的地資料表。  
  
 **刪除目的地資料表/檔案中的資料列**  
 指定在載入新資料之前，是否要清除現有資料表中的資料。  
  
 **將資料列附加至目的地資料表/檔案**  
 指定是否要將新資料附加到現有資料表中已存在的資料後面。  
  
 **編輯 SQL**  
 使用中的預設陳述式**建立資料表 SQL 陳述式**對話方塊方塊中，或修改您的目的。 如果修改此陳述式，您還必須對資料表對應進行相關的變更。  
  
 **卸除並重新建立目的地資料表**  
 選擇此選項即可覆寫目的地資料表。 只有在您使用精靈來建立目的地資料表時，才能使用這個選項。 目的地資料表只有在您儲存精靈所建立的封裝，然後再次執行封裝時才會卸除並重建。  
  
 **啟用識別插入**  
 選擇此選項即可允許將來源資料中的現有識別值，插入目的地資料表裡的識別欄位中。 依預設，目的地識別欄位並不允許此動作。  
  
 **對應**  
 顯示資料來源中的每個資料行如何對應至目的地中的資料行。  
  
 這份清單具有下列資料行：  
  
 **Source**  
 檢視您可以為其設定轉換參數的每個來源資料行。  
  
 **目的地**  
 指定在進行複製作業的期間，您是否想要忽略某資料行。 您可以透過選取複製的資料行子集**\<忽略 >** 中此資料行，您想要跳過的資料行。 在對應資料行之前，您必須忽略不會加以對應的所有資料行。  
  
 **型別**  
 選取資料行的資料類型。  
  
 **可為 Null**  
 指定資料行是否允許有 Null 值。  
  
 **大小**  
 指定資料行中的字元數目。  
  
 **有效位數**  
 參考數字的位數，來指定所顯示資料的有效位數。  
  
 **小數位數**  
 參考小數的位數，來指定所顯示資料的小數位數。  
  
  
