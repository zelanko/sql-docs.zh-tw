---
description: 專案設定 (轉換) (SybaseToSQL)
title: 專案設定 (轉換)  (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/19/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1f4d616b964a1e9e9eed391e3386b16e9df54e44
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195530"
---
# <a name="project-settings-conversion-sybasetosql"></a>專案設定 (轉換) (SybaseToSQL)

[**專案設定**] 對話方塊的 [**轉換**] 頁面包含的設定，可自訂 SSMA 如何將 SAP 自我調整 Server Enterprise (ASE) 語法轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL 語法。

您可以在 [**專案設定**] 和 [**預設專案設定**] 對話方塊中使用 [**轉換**] 窗格：

- 如果您想要指定所有 SSMA 專案的設定，請在 [ **工具** ] 功能表上選取 [ **預設專案設定**]，按一下左窗格底部的 **[一般** ]，然後按一下 [ **轉換**]。

- 若要指定目前專案的設定，請在 [ **工具** ] 功能表上選取 [ **專案設定**]，按一下左窗格底部的 **[一般** ]，然後按一下 [ **轉換**]。

## <a name="miscellaneous-section"></a>其他區段

### <a name="error"></a>@@ERROR

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL 和 ASE 使用不同的錯誤碼。

使用此設定可指定當 SSMA 在輸出或 [錯誤清單] 窗格中遇到 ASE 程式碼的參考時，所顯示的訊息類型 (警告或錯誤) `@@ERROR` 。

- 如果您選取 [ **轉換] 和 [標記為警告**]，SSMA 會轉換語句，並以警告註解標記這些語句。
- 如果您選取 [ **標記錯誤**]，SSMA 會略過轉換，並將語句標記為錯誤批註。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|轉換並標示警告|
|開放式|轉換並標示警告|
|完整|標記錯誤|

### <a name="conversion-of-like-operator"></a>LIKE 運算子的轉換

指定是否要將 `LIKE` 運算元轉換成符合 SAP ASE 行為。 重點是 ASE 會修剪類似模式中的尾端空白。 因應措施是以最大有效位數將 right 運算式轉換成固定長度的資料類型。
  
- 選取 [ **簡單轉換** ] 以轉換運算式，而不進行任何更正。
- 若要使用 ASE 行為，請選取 [ **轉換成固定長度]。**
  
當您在 [模式] 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|簡單轉換|
|開放式|簡單轉換|
|完整|轉換成固定長度|

### <a name="convert-or-cast-empty-strings-to-numeric-types"></a>將空字串轉換或轉換成數數值型別

指定如何處理 `CONVERT` `CAST` 數位類型為 datatype 引數的或運算式內的空白或空白字串。 下列選項可用於此設定：

- 選取 [ **簡單轉換** ] 以轉換運算式，而不進行任何更正。
- 如果選取了 **空字串作為零數值** ，則會將字串參數 `{s}` 取代為 `CASE ltrim(rtrim({s})) WHEN "" THEN 0 else {s} END` expression。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|簡單轉換|
|開放式|簡單轉換|
|完整|空字串為零數值|

### <a name="concatenation-of-null"></a>Null 的串連

此設定會指定如何轉換字串串連 `NULL` 。 您可以針對此特定設定設定下列選項：

- 如果選取 [ **換行] 與 [使用 ISNull 函數** ] 選項，串連中的每個非常數 `string_expression` 都會以 `ISNULL(string_expression)` 和取代，而且會以 `NULL` 空字串取代。
- **保留目前的語法** 將會維持原始語法。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|保留目前的語法|
|開放式|保留目前的語法|
|完整|使用 ISNull 函數換行|

### <a name="conversion-of-empty-strings"></a>空字串的轉換

此設定會指定如何轉換空字串。 您可以針對此特定設定設定下列選項：

- **將所有字串運算式取代為空格**
- **以空格取代空白字串常數**

若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 行為，請選取 [ **保留目前的語法**]。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|保留目前的語法|
|開放式|保留目前的語法|
|完整|將所有字串運算式取代為空格|

### <a name="convert-and-cast-binary-string-conversion"></a>轉換和轉換二進位字串轉換

將二進位值轉換成數位，可以在不同的平臺上傳回不同的值。 例如，在 x86 處理器上， `CONVERT(integer, 0x00000100)` 會 `65536` 在 ASE 中傳回，但是 `256` 在中則會傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 ASE 也會根據位元組順序傳回不同的值。

您可以使用此設定來控制 SSMA 轉換 `CONVERT` 的方式，以及 `CAST` 包含二進位值的運算式：

- 選取 [ **簡單轉換** ] 可轉換運算式，但不含任何警告或修正。 如果您知道 ASE 伺服器的位元組順序不需要任何二進位值的變更，請使用此設定。
- 選取 [ **轉換] 和 [更正** ]，讓 SSMA 轉換及更正要用於的運算式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 常值常數中的位元組順序將會反轉。 所有其他的二進位值 (例如二進位變數和資料行) 都會標記為錯誤。 如果您知道 ASE 伺服器的位元組順序需要變更二進位值，請使用此值。

選取 [ **轉換並標示警告** ] 以讓 SSMA 轉換及更正運算式，並使用警告註解標記所有已轉換的運算式。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|轉換並標示警告|
|開放式|簡單轉換|
|完整|轉換和修正|

### <a name="dynamic-sql"></a>動態 SQL

使用此設定可指定當 SSMA 在 ASE 程式碼中遇到動態 SQL 時，出現在 [ **輸出** ] 或 [ **錯誤清單** ] 窗格中的訊息類型 (警告或錯誤) 。

- 如果您選取 [ **轉換並標示為警告**]，SSMA 會轉換動態 SQL，並將語句標記為警告批註。
- 如果您選取 [ **標記錯誤**]，SSMA 會略過轉換，並將語句標記為錯誤批註。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|轉換並標示警告|
|開放式|轉換並標示警告|
|完整|標記錯誤|

### <a name="equality-check-conversion"></a>相等檢查轉換

在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 中，如果 `ANSI_NULLS` 設定為 on， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `UNKNOWN` 當任何等號比較包含值時，/Azure SQL 就會傳回 `NULL` 。 如果 `ANSI_NULLS` 是 off， `NULL` 當比較的資料行和運算式或兩個運算式都是時，包含值的相等比較就會傳回 true `NULL` 。 根據預設 (`ANSINULL OFF`) SAP ASE 相等比較的行為就像是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL `ANSI_NULLS OFF` 。

- 如果您選取 **簡單轉換**，SSMA 會將 ASE 程式碼轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL 語法，而不需要額外檢查 `NULL` 值。 如果 `ANSI_NULLS` `OFF` 在/Azure SQL 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或您想要根據每個案例修訂相等比較，請使用此設定。
- 如果您選取 [ **考慮 Null 值**]，SSMA 就會 `NULL` 使用和子句來新增值的檢查 `IS NULL` `IS NOT NULL` 。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|簡單轉換|
|開放式|簡單轉換|
|完整|考慮 Null 值|

### <a name="format-strings"></a>格式字串

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL 不再支援 `format_string` 和語句中的引數 `PRINT` `RAISERROR` 。 `format_string`允許將可替換參數直接放在字串中，然後在執行時間取代參數的引數。 相反地，您 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須使用字串常值或使用變數所建立的字串，來要求使用完整字串。 如需詳細資訊，請參閱 [PRINT ([!INCLUDE[tsql](../../includes/tsql-md.md)]) ](../../t-sql/language-elements/print-transact-sql.md) 主題。

當 SSMA 遇到引數時 `format_string` ，可以使用變數來建立字串常值，或建立新的變數，並使用該變數建立字串。

- 若要使用和函數的字串常值 `PRINT` `RAISERROR` ，請選取 [ **建立新字串**]。

    在此模式中，如果 PRINT 或 RAISERROR 語句不使用預留位置和區域變數，則語句會維持不變。 雙百分比字元 (%% ) 在列印字串常值中變更為單一百分比字元%。

    如果 PRINT 或 RAISERROR 語句使用預留位置和一或多個本機變數，如下列範例所示：

    ```sql
    PRINT 'Total: %1!%%', @percent
    ```

    SSMA 會將它轉換成下列語法：

    ```sql
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'
    ```

    如果 `format_string` 是變數，例如在下列語句中：  

    ```sql
    PRINT @fmt, @arg1, @arg2
    ```

    SSMA 無法執行簡單的字串轉換，而且必須建立新的變數：

    ```sql
    DECLARE @print_format_1 varchar(max)
    SET @print_format_1 =
        REPLACE (@fmt, '%%', '%')
    SET @print_format_1 =
        REPLACE (@print_format_1, '%1!',
        CAST (@arg1 AS varchar(max)))
    SET @print_format_1 =
        REPLACE (@print_format_1, '%2!',
        CAST (@arg2 AS varchar(max)))
    PRINT @print_format_1
    ```

    當它使用 **建立新的字串** 模式時，SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會假設 `CONCAT_NULL_YIELDS_NULL` 選項為 `OFF` 。 因此，SSMA 不會檢查是否有 null 引數。

- 若要讓 SSMA 為每個和語句建立新的變數 `PRINT` `RAISERROR` ，然後使用該變數作為字串值，請選取 [ **建立新變數**]。

    在此模式中，如果 `PRINT` 或 `RAISERROR` 語句不使用預留位置和區域變數，SSMA 會以單一百分比字元取代 () 的所有雙百分比字元， `%%` 以符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL 語法。

    如果 `PRINT` 或 `RAISERROR` 語句使用預留位置和一或多個本機變數，如下列範例所示：

    ```sql
    PRINT 'Total: %1!%%', @percent
    ```

    SSMA 會將它轉換成下列語法：

    ```sql
    DECLARE @print_format_1 varchar(max)
    SET @print_format_1 = 'Total: %1!%'
    SET @print_format_1 =
        REPLACE (@print_format_1, '%1!',
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))
    PRINT @print_format_1
    ```

    如果 `format_string` 是變數，例如在下列語句中：

    ```sql
    PRINT @fmt, @arg1, @arg2
    ```

    SSMA 會建立新的變數，如下所示，檢查每個引數中的 null 值：

    ```sql
    DECLARE @print_format_1 varchar(max)
    SET @print_format_1 =
        REPLACE (@fmt, '%%', '%')
    SET @print_format_1 =
        REPLACE (@print_format_1, '%1!',
        ISNULL(CAST (@arg1 AS varchar(max)),''))
    SET @print_format_1 =
        REPLACE (@print_format_1, '%2!',
        ISNULL(CAST (@arg2 AS varchar(max)),''))
    PRINT @print_format_1
    ```

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|建立新字串|
|開放式|建立新字串|
|完整|建立新變數|

### <a name="insert-an-explicit-value-into-a-timestamp-column"></a>將明確值插入時間戳記資料行

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL 不支援將明確值插入時間戳記資料行。

- 若要從語句中排除時間戳記資料行 `INSERT` ，請選取 [ **排除資料行**]。
- 若要在每次時間戳記資料行在語句中時列印錯誤訊息 `INSERT` ，請選取 [ **標記錯誤**]。 在此模式中， `INSERT` 將不會轉換語句，而且將會以錯誤註解標記。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|排除資料行|
|開放式|排除資料行|
|完整|標記錯誤|

### <a name="store-temporary-objects-defined-in-procedures"></a>儲存程式中定義的暫存物件

這項設定會指定是否應該在轉換期間，將出現在程式中的暫存物件定義儲存在來源中繼資料中。

- 選取 **[是]** 以儲存到中繼資料。
- 如果不需要儲存物件，請選取 [ **否** ]。

|[模式]|值|
|-|-|
|預設|是|
|開放式|是|
|完整|否|

### <a name="proxy-table-conversion"></a>Proxy 資料表轉換

指定 ASE proxy 資料表是否轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 資料表，或是不會轉換，而且程式碼會標示錯誤批註。

- 選取 [ **轉換** ] 將 proxy 資料表轉換為一般資料表。
- 選取 [ **標記錯誤** ]，直接以錯誤註解標記 proxy 資料表程式碼。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|標記錯誤|
|開放式|標記錯誤|
|完整|標記錯誤|

### <a name="raiserror-base-message-number"></a>RAISERROR 基本訊息編號

ASE 使用者訊息會儲存在每個資料庫中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者訊息會集中儲存，並可透過 `sys.messages` 目錄查看取得。 此外，ASE 使用者訊息會從開始 `20000` ，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤訊息會從開始 `50001` 。

此設定會指定要新增至 ASE 使用者訊息編號的數位，以將其轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者訊息。 如果您 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目錄檢視中有使用者訊息 `sys.messages` ，您可能必須將此數位變更為較高的值。 這是因為轉換的訊息編號不會與現有的訊息編號衝突。

請注意：
  
- 範圍中的 ASE 訊息 `17000` - `19999` 是來自 `sysmessages` 系統資料表，且不會進行轉換。
- 如果語句中參考的訊息編號 `RAISERROR` 是常數，SSMA 會將基底訊息編號新增至常數，以決定新的使用者訊息編號。
- 如果所參考的訊息編號是變數或運算式，SSMA 將會建立中繼區域變數。
- 在 **開放式模式**中，SSMA 會假設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 選項 `CONCAT_NULL_YIELDS_NULL` 為 `OFF` ，且不會檢查 `NULL` 引數。
- 在 **完整模式**中，SSMA 會檢查 `NULL` 引數。
- `RAISERROR` with `arg-list` 引數不會轉換。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|30001|
|開放式|30001|
|完整|30001|

### <a name="system-objects"></a>系統物件

使用此設定可指定 SSMA 在 [ **輸出** ] 或 [ **錯誤清單** ] 窗格中所顯示的訊息類型 (警告或) 錯誤，並在遇到使用 ASE 系統物件時出現的錯誤。

- 如果您選取 [ **轉換] 和 [標記為警告**]，SSMA 將會轉換系統物件的參考，並將語句標記為警告批註。
- 如果您選取 [ **標記但有錯誤**]，SSMA 將不會轉換系統物件的參考，而且會以錯誤註解標記語句。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|轉換並標示警告|
|開放式|轉換並標示警告|
|完整|標記錯誤|

### <a name="unresolved-identifiers"></a>未解析的識別碼

使用此設定可指定當 SSMA 在無法解析識別碼時，顯示在 [ **輸出** ] 或 [ **錯誤清單** ] 窗格中的訊息類型 (警告或錯誤) 。

- 如果您選取 [ **轉換] 和 [標記為警告**]，SSMA 會嘗試將參考轉換為無法解析的識別碼，並將語句標記為警告批註。
- 如果您選取 [ **標記錯誤**]，則 SSMA 不會將參考轉換為無法解析的識別碼，而且會將語句標記為錯誤批註。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|轉換並標示警告|
|開放式|轉換並標示警告|
|完整|標記錯誤|

## <a name="system-functions-section"></a>系統函數區段

### <a name="charindex-function"></a>CHARINDEX 函數

在 ASE 中 `CHARINDEX` ， `NULL` 只有當所有輸入運算式為時，才會傳回 `NULL` 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`NULL`如果任何輸入運算式為，/AZURE SQL 會傳回 `NULL` 。

- 若要使用 ASE 行為，請選取 [ **取代**函式]。 所有對函式的呼叫 `CHARINDEX` 會 `CHARINDEX_VARCHAR` 根據在  `CHARINDEX_NVARCHAR` 使用者資料庫中 (建立的參數類型，以在使用者) 資料庫中所傳遞的參數類型來取代， `s2ss` 以模擬 SAP ASE 行為。
- 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 行為，請選取 [ **保留目前的語法**]。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|保留目前的語法|
|開放式|保留目前的語法|
|完整|Replace 函式|
  
### <a name="datalength-function"></a>DATALENGTH 函數

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`DATALENGTH`當值為單一空格時，函式所傳回的值會有不同的/AZURE SQL 和 ASE。 在此情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 會傳回 `0` ，而且 ASE 會傳回 `1` 。

- 若要使用 ASE 行為，請選取 [ **取代**函式]。 `DATALENGTH`函數的所有呼叫都會以 `CASE` 運算式取代，以模擬 SAP ASE 行為。
- 若要使用預設的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 行為，請選取 [ **保留目前的語法**]。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|保留目前的語法|
|開放式|保留目前的語法|
|完整|Replace 函式|

### <a name="index_col-function"></a>INDEX_COL 函數

ASE 支援函式的選擇性 `user_id` 引數 `INDEX_COL` ; 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL 不支援這個引數。 如果您使用 `user_id` 引數，則無法將此函式轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Azure SQL 語法。

- 若要使用 ASE 行為，請選取 [ **轉換**函式]。 如果程式碼包含 `user_id` 引數，SSMA 將會顯示錯誤。
- 若要在每次發生時顯示錯誤訊息 `INDEX_COL` ，請選取 [ **標記錯誤**]。 SSMA 將不會轉換函式的參考，而且會將語句標記為錯誤批註。

|[模式]|值|
|-|-|
|預設|標記錯誤|
|開放式|標記錯誤|
|完整|標記錯誤|

### <a name="index_colorder-function"></a>INDEX_COLORDER 函式

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL 沒有 `INDEX_COLORDER` 系統函數。

- 若要使用 ASE 行為，請選取 [ **轉換**函式]。 對函式的所有呼叫都會以使用者 `INDEX_COLORDER` 資料庫中使用相同名稱的使用者定義函數的呼叫來取代， `INDEX_COLORDER` (在使用者資料庫中建立，而該名稱是 `s2ss` 模擬 SAP ASE 行為的架構名稱) 。
- 若要在每次發生時列印錯誤訊息 `INDEX_COLORDER` ，請選取 [ **標記錯誤**]。 SSMA 將不會轉換函式的參考，而且會將語句標記為錯誤批註。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|標記錯誤|
|開放式|標記錯誤|
|完整|標記錯誤|

### <a name="left-and-right-functions"></a>左邊和右邊函數

`LEFT``RIGHT`ASE 中的函式與負值長度參數的行為不同。

- 若要使用 ASE 行為，請選取 [ **取代**函式]。 然後，會將 length 參數取代為 `CASE` `NULL` 負數值的運算式。
- 若要使用 SQL Server 行為，請選取 [ **保留目前的語法**]。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|保留目前的語法|
|開放式|保留目前的語法|
|完整|Replace 函式|

> [!NOTE]
> 如果長度參數是常值而不是複雜運算式，則不論專案設定如何，一律會取代長度值 `NULL` 。

### <a name="next_identity-function"></a>NEXT_IDENTITY 函式

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Azure SQL 沒有 `NEXT_IDENTITY` 系統函數。

- 若要使用 ASE 行為，請選取 [ **轉換**函式]。 函式的所有呼叫 `NEXT_IDENTITY` 都會取代為 `(IDENT_CURRENT(parameter Value) + IDENT_INCR(parameter Value)` 模擬 SAP ASE 行為的運算式。
- 若要在每次發生時列印錯誤訊息 `NEXT_IDENTITY` ，請選取 [ **標記錯誤**]。 SSMA 將不會轉換函式的參考，而且會將語句標記為錯誤批註。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|標記錯誤|
|開放式|標記錯誤|
|完整|標記錯誤|

**預設/開放式/完整模式：** 標記錯誤

### <a name="patindex-function"></a>PATINDEX 函數

指定是否轉換函式 `PATINDEX` 以符合 SAP ASE 行為。 重點是 ASE 會在搜尋模式中修剪尾端空白。 解決方法是將值運算式轉換成具有最大精確度的固定長度資料類型，並將函式套用 `rtrim` 至搜尋模式。

- 若要使用 ASE 行為，請選取 [ **使用**]。  
- 若要使用預設的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 行為，請選取 [ **不使用**]。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|請勿使用|
|開放式|請勿使用|
|完整|使用|

### <a name="replicate-function"></a>REPLICATE 函數

`REPLICATE`函數會以指定的次數重複字串。 在 ASE 中，如果您指定重複字串零次，則結果為 `NULL` 。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 中，結果會是空字串。

- 若要使用 ASE 行為，請選取 [ **取代**函式]。 所有對函式的呼叫 `REPLICATE` 會 `REPLICATE_VARCHAR` 根據在 `REPLICATE_NVARCHAR` 使用者資料庫中 (建立的參數類型，以在使用者) 資料庫中所傳遞的參數類型來取代， `s2ss` 以模擬 SAP ASE 行為。
- 若要使用預設的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 行為，請選取 [ **取代**函式]。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|Replace 函式|
|開放式|Replace 函式|
|完整|Replace 函式|

### <a name="trim-ltrim-rtrim-function"></a>TRIM (LTRIM，RTRIM) 函數

這項設定會指定是否要 `TRIM` `LTRIM` 使用 SAP ASE 對等語法函式取代和函式的呼叫， `RTRIM` 或保留目前的語法。 此特定設定有下列選項：

- **Replace 函式**
- **保留目前的語法**

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|Replace 函式|
|開放式|Replace 函式|
|完整|Replace 函式|

### <a name="substring-function"></a>SUBSTRING 函數

在 ASE 中， `SUBSTRING(expression, start, length)` `NULL` 如果指定的起始值大於運算式中的字元數，或如果長度等於零，則此函數會傳回。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 中，對應的運算式會傳回空字串。

- 若要使用 ASE 行為，請選取 [ **取代**函式]。 對函式的所有呼叫 `SUBSTRING` 都會 `SUBSTRING_VARCHAR` 根據在 `SUBSTRING_NVARCHAR` `SUBSTRING_VARBINARY` 使用者資料庫中 (建立的參數類型，以使用者) 資料庫中所傳遞的參數類型來取代， `s2ss` 以模擬 SAP ASE 行為。
- 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /AZURE SQL 行為，請選取 [ **保留目前的語法**]。

當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：

|[模式]|值|
|-|-|
|預設|保留目前的語法|
|開放式|保留目前的語法|
|完整|Replace 函式|

## <a name="tables-section"></a>資料表區段

### <a name="add-primary-key"></a>新增主要金鑰

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果 SAP ASE 資料表沒有 primary key 或 unique 索引，則會在或 AZURE SQL 資料表中建立新的主要金鑰。

|[模式]|值|
|-|-|
|預設|否|
|開放式|否|
|完整|是|

> [!NOTE]
> 連接到 Azure SQL 時，預設為 **[是]** 。

## <a name="see-also"></a>另請參閱

[使用者介面參考 (SybaseToSQL)](../../ssma/sybase/user-interface-reference-sybasetosql.md)
