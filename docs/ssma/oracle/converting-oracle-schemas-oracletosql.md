---
title: 轉換 Oracle 結構描述 (OracleToSQL) |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 9f1bbbb583a29cfb5e3a4b416515a293aa211d98
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="converting-oracle-schemas-oracletosql"></a>轉換 Oracle 結構描述 (OracleToSQL)
您已經連接到 Oracle 之後，連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，設定專案和對應的資料選項，您可以將轉換至 Oracle 資料庫物件和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫物件。  
  
## <a name="the-conversion-process"></a>轉換程序  
轉換的資料庫物件從 Oracle 取得的物件定義、 將它們轉換成類似[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件，然後再將這項資訊載入至 SSMA 中繼資料。 不會載入到的執行個體資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您接著可以使用檢視物件和其屬性[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管。  
  
在轉換期間，SSMA 會列印至輸出窗格的輸出訊息和錯誤訊息 [錯誤清單] 窗格。 若要判斷您是否需要修改 Oracle 資料庫或您要取得所需的轉換結果的轉換程序使用的輸出和錯誤的資訊。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
在轉換前的物件，請檢閱中的專案轉換選項**專案設定** 對話方塊。 藉由使用此對話方塊中，您可以設定 SSMA 如何將轉換函式和全域變數。 如需詳細資訊，請參閱[專案設定&#40;轉換&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)。  
  
## <a name="conversion-results"></a>轉換結果  
下表顯示 Oracle 物件轉換，以及產生[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件：  
  
|||  
|-|-|  
|Oracle 物件|產生 SQL Server 物件|  
|函數|如果函式直接轉換成[!INCLUDE[tsql](../../includes/tsql_md.md)]，SSMA 建立函式。<br /><br />在某些情況下，函式必須轉換成預存程序。 在此情況下，SSMA 所建立的預存程序和函式呼叫預存程序。|  
|程序|如果程序可以直接轉換成[!INCLUDE[tsql](../../includes/tsql_md.md)]，SSMA 建立預存程序。<br /><br />在某些情況下，必須在自發交易中呼叫預存程序。 在此情況下，SSMA 會建立兩個預存程序： 實作程序，和另一個則用於呼叫實作的其中一個預存程序。|  
|Packages|SSMA 會建立一組預存程序和函式，會完全依類似的物件名稱。|  
|序列|SSMA 建立順序物件 （SQL Server 2012 或 SQL Server 2014），或模擬 Oracle 序列。|  
|具有相依的物件，例如索引和觸發程序的資料表|SSMA 會建立資料表，與相依物件。|  
|檢視與相依的物件，例如觸發程序|SSMA 會建立具有相依物件的檢視。|  
|具體化的檢視|**SSMA 會建立 SQL server 上的索引檢視表，但有些例外狀況。如果具體化的檢視包含一或多個下列建構函式，轉換將會失敗：**<br /><br />使用者定義函數<br /><br />不具決定性的欄位 / 函式 / 運算式在 SELECT、 位置或 GROUP BY 子句<br /><br />選取 * 中的浮點數資料行的使用位置或 GROUP BY 子句 （上一個問題的特殊情況）<br /><br />自訂資料類型 （內含巢狀資料表）<br /><br />計數 (相異&lt;欄位&gt;)<br /><br />FETCH<br /><br />OUTER 聯結 (LEFT、RIGHT 或 FULL)<br /><br />子查詢，其他的檢視<br /><br />[過度]、 RANK、 會導致、 記錄<br /><br />MIN、MAX<br /><br />UNION、 減號，交集<br /><br />HAVING|  
|觸發程序|**SSMA 會建立觸發程序根據下列規則：**<br /><br />之前觸發程序會轉換成，而不是觸發程序。<br /><br />AFTER 觸發程序會轉換成 AFTER 觸發程序。<br /><br />INSTEAD OF 觸發程序會轉換成，而不是觸發程序。 多個 INSTEAD OF 觸發程序定義在相同的作業會結合到一個觸發程序。<br /><br />資料列層級觸發程序都被模擬的使用資料指標。<br /><br />階層式的觸發程序會轉換成多個個別的觸發程序。|  
|同義字|**同義字會建立下列物件類型：**<br /><br />資料表和物件的資料表<br /><br />檢視和物件的檢視<br /><br />預存程序<br /><br />函數<br /><br />**解決和直接物件的參考取代為下列物件的同義字：**<br /><br />序列<br /><br />Packages<br /><br />Java 類別的結構描述物件<br /><br />使用者定義的物件類型<br /><br />為另一個同義字的同義字無法移轉，並將標示為錯誤。<br /><br />同義字不會建立 Materialized 檢視。|  
|使用者定義型別|**SSMA 使用者定義類型的轉換不提供支援。使用者定義型別，其使用情形納入 PL/SQL 程式會使用下列規則來引導式的特殊轉換錯誤標記：**<br /><br />資料表資料行的使用者定義型別會轉換成 VARCHAR(8000)。<br /><br />引數的使用者定義型別預存程序或函式會轉換成 VARCHAR(8000)。<br /><br />PL/SQL 區塊中的使用者定義類型的變數會轉換成 VARCHAR(8000)。<br /><br />物件表會轉換成標準的資料表。<br /><br />物件檢視會轉換成標準的檢視。|  
  
## <a name="converting-oracle-database-objects"></a>轉換的 Oracle 資料庫物件  
若要將 Oracle 資料庫物件，您先選取您要轉換的物件，然後執行轉換的 SSMA。 若要進行轉換時，檢視輸出訊息上**檢視**功能表上，選取**輸出**。  
  
**若要將 Oracle 物件轉換成 SQL Server 語法**  
  
1.  在 Oracle 中繼資料總管，請在 Oracle 伺服器上，依序展開，然後再展開**結構描述**。  
  
2.  選取要轉換的物件：  
  
    -   若要轉換的所有結構描述，選取核取方塊旁的 **結構描述**。  
  
    -   若要轉換或省略資料庫，選取結構描述名稱旁邊的核取方塊。  
  
    -   轉換或省略物件的類別，結構描述中，依序展開，然後選取或清除類別旁的核取方塊。  
  
    -   轉換或省略個別物件，展開類別目錄資料夾，然後選取或清除物件旁的核取方塊。  
  
3.  若要將所有選取的物件，以滑鼠右鍵按一下**結構描述**選取**轉換結構描述**。  
  
    您也可以轉換個別物件或類別目錄的物件，該物件或其父資料夾上按一下滑鼠右鍵，然後選取**轉換結構描述**。  
  
## <a name="viewing-conversion-problems"></a>檢視轉換問題  
某些 Oracle 物件可能不會轉換。 您可以檢視摘要轉換報表來判斷轉換成功率。  
  
**若要檢視摘要報表**  
  
1.  在 Oracle 中繼資料總管，選取**結構描述**。  
  
2.  在右窗格中，選取**報表** 索引標籤。  
  
    此報告會顯示摘要評估報表中的所有資料庫物件評估或轉換。 您也可以檢視個別物件的摘要報告：  
  
    -   若要檢視報表中的個別結構描述，請在 Oracle 中繼資料總管 選取的結構描述。  
  
    -   若要檢視報表中的個別物件，請在 Oracle 中繼資料總管 選取的物件。 已轉換問題的物件具有紅色錯誤圖示。  
  
無法轉換的物件，您可以檢視導致轉換失敗的語法。  
  
**若要檢視個別轉換問題**  
  
1.  在 Oracle 中繼資料總管，依序展開**結構描述**。  
  
2.  展開結構描述會顯示紅色錯誤圖示。  
  
3.  在結構描述中，展開一個資料夾具有紅色錯誤圖示。  
  
4.  選取具有紅色錯誤圖示的物件。  
  
5.  在右窗格中，按一下 [**報表**] 索引標籤。  
  
6.  在頂端**報表** 索引標籤是下拉式清單。 如果此清單會顯示**統計資料**，變更選取範圍到**來源**。  
  
    SSMA 會顯示與原始程式碼和數個程式碼正上方的按鈕。  
  
7.  按一下**下一個問題** 按鈕。 這是指向右側的箭號紅色錯誤圖示。  
  
    SSMA 會反白顯示在目前的物件中找到的第一個有問題的原始碼。  
  
針對無法轉換每個項目，您必須決定您想要使用該物件：  
  
-   您可以修改程序的程式碼上**SQL**  索引標籤。  
  
-   您可以修改以移除或修改有問題的程式碼的 Oracle 資料庫中的物件。 若要更新的程式碼載入 SSMA，您必須更新的中繼資料。 如需詳細資訊，請參閱[連接到 Oracle 資料庫&#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)。  
  
-   您可以從移轉排除的物件。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管和 Oracle 中繼資料總管，清除項目旁邊的核取方塊，然後再載入物件到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和從 Oracle 移轉資料。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[已轉換的物件載入 SQL Server](http://msdn.microsoft.com/en-us/a8ae33b2-1883-4785-922b-ea0e31c0b37a)。  
  
## <a name="see-also"></a>另請參閱  
[SQL server 資料庫移轉 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
