---
description: 使用安裝程式新增和修改資料來源
title: 使用安裝程式新增和修改資料來源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8592c01897e691cdb6702c4efdfca6054655a793
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494738"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>使用安裝程式新增和修改資料來源
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 資料來源會識別可包含網路程式庫、伺服器、資料庫和其他屬性之資料的路徑，在此案例中，資料來源是 Oracle 資料庫的路徑。 若要連接到資料來源，驅動程式管理員會檢查 Windows 登錄中是否有特定的連接資訊。  
  
 Odbc 驅動程式管理員和 ODBC 驅動程式會使用「ODBC 資料來源管理員」所建立的登錄專案。 此專案包含每個資料來源及其相關聯驅動程式的相關資訊。 在您可以連接到資料來源之前，必須先將其連接資訊新增至登錄。  
  
 若要加入和設定資料來源，請使用 [ [ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)]。 ODBC 管理員會更新您的資料來源連接資訊。 當您加入資料來源時，ODBC 系統管理員會為您更新登錄資訊。  
  
### <a name="to-add-a-data-source-for-windows"></a>若要加入 Windows 的資料來源  
  
1.  開啟 [ODBC 資料來源管理員]。  
  
2.  在 [ODBC 資料來源管理員] 對話方塊中，按一下 [加入]。 [新增資料來源] 對話方塊隨即出現。  
  
3.  選取 [Microsoft ODBC for Oracle]，然後按一下 [完成]。 [Microsoft ODBC for Oracle 安裝程式] 對話方塊隨即出現。  
  
4.  在 [資料來源名稱] 方塊中，輸入您想要存取的資料來源名稱。 它可以是您選擇的任何名稱。  
  
5.  在 [描述] 方塊中，輸入驅動程式的描述。 這個選擇性欄位描述資料來源連接的資料庫驅動程式。 它可以是您選擇的任何名稱。  
  
6.  在 [使用者名稱] 方塊中，輸入您的資料庫使用者名稱 (資料庫使用者識別碼) 。  
  
7.  在 [伺服器] 方塊中，輸入您想要存取之 Oracle 伺服器引擎的資料庫別名或連接字串。  
  
8.  按一下 [確定] 以加入此資料來源。  
  
> [!NOTE]  
>  [資料來源] 對話方塊隨即出現，且 ODBC 管理員會更新登錄資訊。 當您連接到此資料來源時，您所輸入的使用者名稱和連接字串會成為這個資料來源的預設連接值。  
  
1.  按一下 [選項] 可對 ODBC Driver for Oracle 設定提供更多規格：  
  
    -   **轉譯** -按一下 [選取] 以選擇載入的資料轉譯器。 預設為 \<No Translator>。  
  
    -   **效能** -[在目錄函數中包含備註] 核取方塊會指定驅動程式是否傳回 [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) 結果集的備註資料行。 當未設定此值時，ODBC Driver for Oracle 可提供更快速的存取。  
  
         [在 SQL 資料行中包含同義字] 核取方塊會指定驅動程式是否會傳回資料行資訊。 **緩衝區大小** 會指定配置用來接收提取資料的大小（以位元組為單位）。 驅動程式會將提取優化，以便從 Oracle 伺服器提取一個資料列，以填滿指定大小的緩衝區。 較大的值通常會在提取大量資料時增加效能。  
  
    -   **自訂** -強制 Odbc DayOfWeek 標準核取方塊會指定結果集是否符合 ODBC 指定的星期幾格式 (星期日 = 1;星期六 = 7) 。 如果清除此核取方塊，則會傳回地區設定特定的 Oracle 值。  
  
         SQLDescribeCol 一律會傳回 [**精確度的值**] 核取方塊，指定驅動程式是否應該針對**SQLDescribeCol**的*cbColDef*引數傳回非零值。 此連接字串屬性只適用于沒有 Oracle 定義之小數位數的資料行，例如計算的數值資料行和資料行，定義為沒有有效位數或小數位數的數位。 當 Oracle 未提供該資訊時， **SQLDescribeCol** 呼叫會傳回130的有效位數。 如果清除此核取方塊，驅動程式會改為針對這些類型的資料行傳回0。  
  
2.  按一下 [加入] 加入另一個資料來源，或按一下 [關閉] 以結束。  
  
### <a name="to-modify-a-data-source-for-windows"></a>若要修改 Windows 的資料來源  
  
1.  開啟 [ODBC 資料來源管理員]。 按一下適當的 [DSN] 索引標籤。  
  
2.  選取您要修改的 Oracle 資料來源，然後按一下 [設定]。 [Microsoft ODBC for Oracle 安裝程式] 對話方塊隨即出現。  
  
3.  修改適用的資料來源欄位，然後按一下 [確定]。  
  
 當您完成修改此對話方塊中的資訊之後，ODBC 管理員就會更新登錄資訊。
