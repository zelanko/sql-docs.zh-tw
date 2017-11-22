---
title: "專案 Settings(Synchronization) (OracleToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e223fb7d-05ec-4fa5-8973-d845c33a23dd
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 81a3c4860c3916753435e2b5c608628650bae255
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="project-settingssynchronization-oracletosql"></a>專案 Settings(Synchronization) (OracleToSQL)
同步處理頁面**專案設定**對話方塊包含自訂如何 SSMA 載入並重新整理資料庫物件，例如資料表和預存程序，到設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
預設的動作選項指定預設設定，重新整理物件從 Oracle 資料庫和 SQL Server 資料庫與同步處理物件。 如需詳細資訊，請參閱[從 Oracle 資料庫重新整理](../../ssma/oracle/refresh-from-database-oracletosql.md)。  
  
您可以存取兩個不同的同步處理頁面包含相同的設定：  
  
-   設定為所有未來的 SSMA 專案，指定上**工具**功能表上，按一下**預設專案設定**，然後按一下 **同步處理**在左窗格底部。  
  
-   若要指定目前的專案中，設定**工具**功能表上，按一下**專案設定**，然後按一下 **同步處理**在左窗格底部。  
  
## <a name="miscellaneous-options"></a>其他選項  
**嘗試**  
指定將物件載入時，應該進行 SSMA 的嘗試次數[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 未載入的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中目前的嘗試將會重試直到 SSMA 到達目前的同步處理程序中的嘗試次數上限。 設定預設值是**2**  
  
## <a name="synchronization-for-oracle-options"></a>如需 Oracle 選項的同步處理  
**本機和遠端物件變更時採取的動作**  
物件定義變更 SSMA 和資料庫伺服器時，同步處理 對話方塊中指定的預設設定。 設定預設值是**從資料庫重新整理**。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
**本機物件變更時採取的動作**  
SSMA 物件發生變更時，同步處理 對話方塊中指定的預設設定。 設定預設值是**略過**。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
**遠端物件變更時採取的動作**  
當資料庫伺服器上變更物件時，同步處理 對話方塊中指定的預設設定。 設定預設值是**從資料庫重新整理**。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
**遺漏本機物件的中繼資料時的動作**  
遺漏本機中繼資料時，同步處理 對話方塊中指定的預設設定。 設定預設值是**從資料庫重新整理**。  
  
-   如果您選取**從資料庫重新整理**，SSMA SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
## <a name="synchronization-for-sql-server-options"></a>SQL Server 選項的同步處理  
**本機和遠端物件變更時採取的動作**  
物件定義變更 SSMA 和資料庫伺服器時，同步處理 對話方塊中指定的預設設定。 設定預設值是**寫入資料庫**。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 滿足條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
**本機物件變更時採取的動作**  
SSMA 物件發生變更時，同步處理 對話方塊中指定的預設設定。 設定預設值是**寫入資料庫**。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 滿足條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
**遠端物件變更時採取的動作**  
當資料庫伺服器上變更物件時，同步處理 對話方塊中指定的預設設定。  設定預設值是**從資料庫重新整理**。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 滿足條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
**遺漏本機物件的中繼資料時的動作**  
遺漏本機中繼資料時，同步處理 對話方塊中指定的預設設定。 設定預設值是**從資料庫重新整理**。  
  
-   如果您選取**從資料庫重新整理**，SSMA 選取**從資料庫重新整理**選項時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 將物件從資料庫中刪除時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
