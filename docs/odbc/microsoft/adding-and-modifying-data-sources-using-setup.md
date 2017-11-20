---
title: "加入和修改資料來源使用安裝程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fd665c63873ba8331290ddeae4ad91137ef1e3c7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="adding-and-modifying-data-sources-using-setup"></a>加入和修改資料來源使用安裝程式
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 資料來源識別資料，可包含網路程式庫、 伺服器、 資料庫和其他屬性的路徑，在此情況下，資料來源是 Oracle 資料庫的路徑。 若要連接到資料來源，驅動程式管理員會檢查 Windows 登錄中的特定連接資訊。  
  
 ODBC 驅動程式管理員和 ODBC 驅動程式會使用建立的 ODBC 資料來源管理員 」 中的登錄項目。 此項目包含每個資料來源和其相關聯的驅動程式的相關資訊。 您可以連接到資料來源之前，其連接資訊必須新增至登錄。  
  
 若要加入及設定資料來源，使用[ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)。 ODBC 管理員更新您的資料來源連接資訊。 當您加入資料來源時，ODBC 管理員更新您的登錄資訊。  
  
### <a name="to-add-a-data-source-for-windows"></a>若要加入資料來源視窗  
  
1.  開啟 ODBC 資料來源管理員。  
  
2.  在 ODBC 資料來源管理員 對話方塊中，按一下 新增。 建立新的資料來源 對話方塊隨即出現。  
  
3.  選取 Oracle 的 Microsoft ODBC，然後按一下 [完成] 5d;。 Microsoft ODBC 的 Oracle 安裝程式 對話方塊隨即出現。  
  
4.  在 [資料來源名稱] 方塊中，輸入您想要存取資料來源的名稱。 它可以是任何您選擇的名稱。  
  
5.  在 [描述] 方塊中，輸入驅動程式的描述。 這個選擇性的欄位描述資料來源連接到資料庫驅動程式。 它可以是任何您選擇的名稱。  
  
6.  在 [使用者名稱] 方塊中，輸入您的資料庫使用者名稱 （您資料庫的使用者識別碼）。  
  
7.  在 [伺服器] 方塊中，輸入資料庫別名或連接的 Oracle 伺服器引擎，您想要存取的字串。  
  
8.  按一下 [確定] 以加入此資料來源。  
  
> [!NOTE]  
>  資料來源 對話方塊隨即出現，並 ODBC 管理員更新登錄資訊。 使用者名稱和連接您所輸入字串成為此資料來源的預設連接值，當您連接到它。  
  
1.  按一下 [製作] 選項更多有關 Oracle 安裝程式的 ODBC 驅動程式規格：  
  
    -   **轉譯**-按一下 [選取] 以選擇載入的資料轉譯器。 預設值是\<否轉譯程式 >。  
  
    -   **效能**— 的包含註解，目錄函數核取方塊中指定驅動程式是否會傳回註解的資料行[SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)結果集。 未設定此值時，oracle ODBC 驅動程式提供存取速度。  
  
         包含內的同義字，SQL 資料行 核取方塊可指定驅動程式是否會傳回資料行資訊。 **緩衝區大小**指定的大小，以位元組為單位，配置給接收提取的資料。 驅動程式會最佳化提取，以便在 Oracle 伺服器從一個提取都會傳回足夠的資料列，以填滿指定的大小的緩衝區。 較大的值通常會擷取大量資料時提升效能。  
  
    -   **自訂**-強制執行 ODBC DayOfWeek 標準的核取方塊可讓您指定結果集將會符合 ODBC 指定的週中日的格式 （星期日 = 1;星期六 = 7）。 如果清除此核取方塊，則會傳回地區設定特定 Oracle 值。  
  
         SQLDescribeCol**一律會傳回值的有效位數**核取方塊可讓您指定的驅動程式是否應該傳回非零的值*cbColDef*引數的**SQLDescribeCol**. 此連接字串屬性僅適用於資料行，其中有任何 Oracle 定義小數位數，例如計算數值資料行和資料行定義為數字，不含有效位數或小數位數。 A **SQLDescribeCol** Oracle 不提供該資訊時，呼叫傳回 130 之有效位數。 如果清除此核取方塊，則驅動程式會改為傳回這些類型的資料行 0。  
  
2.  按一下 [新增] 以新增另一個資料來源，或按一下 [關閉] 結束。  
  
### <a name="to-modify-a-data-source-for-windows"></a>若要修改資料來源視窗  
  
1.  開啟 ODBC 資料來源管理員。 按一下適當的 DSN 索引標籤。  
  
2.  選取您想要修改，然後按一下 設定的 Oracle 資料來源。 Microsoft ODBC 的 Oracle 安裝程式 對話方塊隨即出現。  
  
3.  修改適用的資料來源欄位，然後按一下 [確定]。  
  
 當您完成修改此對話方塊中的資訊時，ODBC 管理員就會更新登錄資訊。

