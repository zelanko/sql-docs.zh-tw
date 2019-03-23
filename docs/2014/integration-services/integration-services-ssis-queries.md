---
title: Integration Services (SSIS) 查詢 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0b4323715155ddb433012624f9d7a5df9bb0a29c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58382457"
---
# <a name="integration-services-ssis-queries"></a>Integration Services (SSIS) 查詢
  「執行 SQL」工作、OLE DB 來源、OLE DB 目的地和「查閱」轉換可使用 SQL 查詢。 在「執行 SQL」工作中，SQL 陳述式可建立、更新和刪除資料庫物件和資料；執行預存程序；以及執行 SELECT 陳述式。 在 OLE DB 來源和「查閱」轉換中的 SQL 陳述式通常都是 SELECT 陳述式或 EXEC 陳述式。 後者最常執行傳回結果集的預存程序。  
  
 可以剖析查詢，以確定它是否有效。 剖析使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]連接的查詢時，會剖析和執行該查詢，並將執行結果 (成功或失敗) 指派給剖析結果。 如果查詢使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]以外的資料連接，就只會剖析陳述式。  
  
 SQL 陳述式可藉由下列方式定義：直接輸入到設計師中，或指定包含該陳述式的檔案連接或變數。  
  
## <a name="direct-input-sql"></a>直接輸入 SQL  
 「查詢產生器」可在「執行 SQL」工作、OLE DB 來源、OLE DB 目的地和「查閱」轉換的使用者介面上取得。 「查詢產生器」有下列優點：  
  
-   以視覺化方式或利用 SQL 命令工作。  
  
     「查詢產生器」包含以視覺化方式撰寫查詢的圖形窗格，以及顯示查詢之 SQL 文字的文字窗格。 您可使用圖形或文字窗格。 「查詢產生器」會同步處理檢視，讓查詢文字和圖形表示永遠都相符。  
  
-   聯結相關的資料表。  
  
     若您加入一個以上的資料表到查詢，「查詢產生器」會自動決定資料表相關的方式，並建構適當的聯結指令。  
  
-   查詢或更新資料庫。  
  
     您可以使用「查詢產生器」，利用 Transact-SQL SELECT 陳述式傳回資料，或建立更新、加入或刪除資料庫中資料錄的查詢。  
  
-   立即檢視並編輯結果。  
  
     您可以執行您的查詢並使用方格 (可讓您在資料庫中捲動並編輯資料錄) 中的資料錄集。  
  
 儘管「查詢產生器」受到視覺化方式的限制，只能建立 SELECT 查詢，但您可在文字窗格中輸入其他類型的 SQL 陳述式，例如，DELETE 和 UPDATE 陳述式。 圖形窗格會自動進行更新，以反映您所輸入的 SQL 陳述式。  
  
 您還可在工作或資料流程元件對話方塊或 [屬性] 視窗中輸入查詢，以提供直接輸入。  
  
 如需詳細資訊，請參閱 [查詢產生器](../../2014/integration-services/query-builder.md)。  
  
## <a name="sql-in-files"></a>檔案中的 SQL  
 「執行 SQL」工作的 SQL 陳述式也可位於個別檔案中。 例如，在執行封裝時，您可以使用工具 (例如， [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中的「查詢編輯器」) 撰寫查詢、將查詢儲存至檔案，然後從檔案讀取該查詢。 檔案只能包含要執行的 SQL 陳述式和註解。 若要使用在檔案中儲存的 SQL 陳述式，您必須提供指定檔案名稱和位置的檔案連接。 如需相關資訊，請參閱 [檔案連線管理員](connection-manager/file-connection-manager.md)。  
  
## <a name="sql-in-variables"></a>變數中的 SQL  
 如果「執行 SQL」工作中的 SQL 陳述式來源是一個變數，則您要提供包含查詢之變數的名稱。 變數的 Value 屬性包含查詢文字。 您可以將變數的 ValueType 屬性設為字串資料類型，然後將 SQL 陳述式輸入或複製到 Value 屬性中。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)和[在封裝中使用變數](../../2014/integration-services/use-variables-in-packages.md)。  
  
  
