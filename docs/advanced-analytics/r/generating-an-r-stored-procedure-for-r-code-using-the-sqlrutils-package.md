---
title: "使用 sqlrutils 套件為 R 程式碼產生 R 預存程序 | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: d8739f16-ac26-4f69-870c-51c77cf286d3
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9301120891d028837ae241be3a0f1b87eebe0024
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package"></a>使用 sqlrutils 套件為 R 程式碼產生 R 預存程序
**sqlrutils** 套件提供一種機制，讓 R 使用者將其 R 指令碼放入 T-SQL 預存程序、註冊具有資料庫的這個預存程序，以及從 R 開發環境執行預存程序。 

轉換 R 程式碼以在單一預存程序內執行，即可更有效地使用 SQL Server R Services，而這需要將 R 指令碼內嵌為 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)的參數。 **sqlrutils** 套件可協助您建置此內嵌 R 指令碼，並適當地設定相關參數。

**sqlrutils** 套件可執行這些工作︰

- 將產生的 T-SQL 指令碼儲存為 R 資料結構內的字串
- 選擇性地產生 T-SQL 指令碼的 .sql 檔案，您可以對其進行編輯或執行以建立預存程序
- 從 R 開發環境中註冊具有 SQL Server 執行個體的新建立預存程序

傳遞格式正確的參數，並處理結果，也可以從 R 環境執行預存程序。 或者，您可以使用來自 SQL Server 的預存程序支援一般資料庫整合案例 (例如 ETL、模型訓練和高容量評分)。

  > [!NOTE]
  > 如果您想要呼叫 *executeStoredProcedure* 函式以從 R 環境執行預存程序，則必須使用 ODBC 3.8 提供者 (例如適用於 SQL Server 的 ODBC Driver 13)。  
  
## <a name="functions-provided-in-sqlrutils"></a>sqlrutils 中提供的函式

下列清單概述您可從 **sqlrutils** 套件呼叫的函式，用以開發在 SQL Server R Services 中使用的預存程序。 如需每個方法或函式的參數的詳細資訊，請參閱套件的 R 說明：

```R
help(package="sqlrutils") 
```

**定義預存程序參數和輸入**

- `InputData`. 定義 SQL Server 中將用於 R 資料框架的資料來源。 您可以指定用來儲存輸入資料的 data.frame 名稱，以及取得資料的查詢，或預設值。 只支援簡單 SELECT 查詢。

- `InputParameter`. 定義將內嵌在 T-SQL 指令碼中的單一輸入參數。 您必須提供參數的名稱和其 R 資料類型。

- `OutputData`. 產生在 R 函式傳回包含 data.frame 的清單時所需的中繼資料物件。 
   *OutputData* 物件用來儲存取自清單的單一 data.frame 名稱。 

- `OutputParameter`. 產生在 R 函式傳回清單時所需的中繼資料物件。 *OutputParameter* 物件會儲存清單單一成員的名稱和資料類型，並假設該成員 **不** 是資料框架。 


**產生並註冊預存程序**


- `StoredProcedure` 是用來建置預存程序的主要建構函式。  這個建構函式會產生「SQL Server 預存程序」  物件，並選擇性地建立文字檔，其中包含可用來產生使用 T-SQL 命令之預存程序的查詢。 選擇性， *StoredProcedure* 函式也可以註冊具有所指定執行個體和資料庫的預存程序。

   + 使用 `func` 引數來指定有效的 R 函式。 函式所使用的所有變數都必須定義在函式內部，或提供為輸入參數。 這些參數最多可以包含一個資料框架。
   + R 函式必須傳回資料框架、具名清單或 NULL。 如果函式傳回清單，則清單最多可以包含一個 data.frame。
   + 使用引數 `spName` 指定您要建立之預存程序的名稱。
   + 您可以使用這些 helper 函式所建立的物件來傳入選擇性輸入和輸出參數： `setInputData`、 `setInputParameter`和 `setOutputParameter`。
   +  選擇性地使用 `filePath` 提供要建立之 .sql 檔案的路徑和名稱。 您可以在 SQL Server 執行個體上執行這個檔案，以使用 T-SQL 產生預存程序。
   + 若要定義將儲存預存程序的伺服器和資料庫，請使用 `dbName` 和  `connectionString`引數。
   + 若要取得用來建立特定 *StoredProcedure* 物件的 *InputData* 和 *InputParameter* 物件清單，請呼叫 `getInputParameters`。 
   + 若要註冊具有所指定資料庫的預存程序，請使用 `registerStoredProcedure`。

   除非指定預設值，否則預存程序物件一般不會有任何相關聯的資料或值。 除非執行預存程序，否則不會擷取資料。 


**指定輸入並執行**

- 使用 `setInputDataQuery` ，將查詢指派給 *InputParameter* 物件。 例如，如果您已使用 R 建立預存程序物件，則可以使用 `setInputDataQuery` 將引數傳遞給 *StoredProcedure* 函式，才能使用所需的輸入來執行預存程序。

- 使用 `setInputValue` ，將特定值指派給儲存為 *InputParameter* 物件的參數。 您接著將參數物件和其值指派傳遞給 *StoredProcedure* 函式，以使用所設定的值來執行預存程序。

- 使用 `executeStoredProcedure` ，執行定義為 *StoredProcedure* 物件的預存程序。 只有透過 R 程式碼執行預存程序時，才會呼叫這個函式。 使用 T-SQL 從 SQL Server 執行預存程序時，請不要使用它。

  > [!NOTE]
  > *executeStoredProcedure* 函式需要 ODBC 3.8 提供者 (例如適用於 SQL Server 的 ODBC Driver 13)。  
  
  



## <a name="see-also"></a>另請參閱
[如何使用 sqlrutils 建立預存程序](../../advanced-analytics/r-services/how-to-create-a-stored-procedure-using-sqlrutils.md)

