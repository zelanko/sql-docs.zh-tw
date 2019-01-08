---
title: 資料行轉換詳細資料對話方塊 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bd7abb585c8f6a44fa8a3e107146e7f74dcbb11c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52821957"
---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>資料行轉換詳細資訊對話方塊 (SQL Server 匯入和匯出精靈)
  使用**資料行轉換詳細資訊**對話方塊，即可檢閱有關個別資料行的詳細的轉換資訊。 這項轉換資訊包含來源和目的地的資料行資料類型，以及精靈將要執行的轉換。 此外，這個頁面也會列出精靈用來判斷所需資料類型轉換的資料類型對應檔案。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會在安裝期間安裝這些資料類型對應檔案。  
  
 **若要開啟 [資料行轉換詳細資料] 對話方塊**  
  
1.  在上**檢閱資料類型問題**頁面[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入和匯出精靈，在**資料表**清單中，選取資料表。  
  
2.  在 **資料類型對應**清單中，按兩下包含您要檢視轉換詳細資料的資料行的資料列。  
  
 若要深入了解[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入和匯出精靈，請參閱 < [SQL Server 匯入和匯出精靈](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。 若要深入了解啟動精靈，選項和相關的權限，才能成功執行精靈，請參閱[執行 SQL Server 匯入和匯出精靈](start-the-sql-server-import-and-export-wizard.md)。  
  
 「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈」的用途是將資料從來源複製到目的地。 這個精靈也可以為您建立目的地資料庫和目的地資料表。 不過，如果您必須複製多個資料庫或資料表，或複製其他種類的資料庫物件，則應該改用「複製資料庫精靈」。 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
  
