---
title: 專案設定 (轉換)  (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1d2f1c02b9a9400236381cdd30fb3deb570500c1
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934647"
---
# <a name="project-settings-conversion-sybasetosql"></a>專案設定 (轉換) (SybaseToSQL)
[**專案設定**] 對話方塊的 [轉換] 頁面包含自訂 SSMA 如何將 Sybase 自動調整伺服器 ENTERPRISE (ASE) 語法轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 語法的設定。  
  
[轉換] 窗格可在 [**專案設定**] 和 [**預設專案設定**] 對話方塊中使用：  
  
-   如果您想要指定所有 SSMA 專案的設定，請在 [**工具**] 功能表上，選取 [**預設專案設定**]，按一下左窗格底部的 **[一般**]，然後按一下 [**轉換**]。  
  
-   若要指定目前專案的設定，請在 [**工具**] 功能表上，選取 [**專案設定**]，按一下左窗格底部的 **[一般**]，然後按一下 [**轉換**]。  
  
## <a name="miscellaneous-options"></a>其他選項  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 和 ASE 使用不同的錯誤碼。  
  
使用此設定可指定當 SSMA 在 ASE 程式碼中遇到 **@ @ERROR **的參考時，顯示在 [輸出] 或 [錯誤清單] 窗格中的訊息類型 (警告或錯誤) 。  
  
-   如果您選取 [**轉換] 和 [以警告標示**]，SSMA 會轉換語句，並以警告註解標記它們。  
  
-   如果您選取 [**標記錯誤**]，SSMA 將會略過轉換，並以錯誤註解標記語句。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 具有警告的 Convert 和 mark  
  
**完整模式：** 有錯誤的標記  
  
**LIKE 運算子的轉換**  
指定是否要轉換 LIKE 運算元，以符合 Sybase ASE 行為。 重點是，Sybase 會修剪類似模式中的尾端空白。 因應措施是將 right 運算式轉換成具有最大有效位數的固定長度資料類型。  
  
-   選取 [**簡單轉換**] 以轉換運算式，而不進行任何更正。  
  
-   若要使用 ASE 行為，請選取 [**轉換成固定長度]。**  
  
當您在 [模式] 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式**：簡單轉換  
  
**Full 模式**：轉換成固定長度  
  
**將空字串轉換或轉換為數數值型別**  
指定如何處理轉換或轉換運算式中的空白或空白字串，並以數數值型別做為資料類型引數。 此設定可使用下列選項：  
  
-   選取 [**簡單轉換**] 以轉換運算式，而不進行任何更正。  
  
-   如果選取**空字串做為零數值**，則字串參數 {s} 將會取代為案例 ltrim (rtrim ( {s} ) # A3 （當 "" then 0 else {s} 結束運算式時）  
  
當您在 [模式] 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式**：簡單轉換  
  
**Full 模式**：空字串為零數值  
  
**Null 的串連**  
此設定會指定如何將字串串連轉換成 Null。 您可以針對此特定設定來設定下列選項：  
  
-   **使用 ISNull 函數來包裝：** 如果設定此選項，串連中的每個非常數 ' string_expression ' 都會以 ISNull () string_expression 來包裝，而 Null 將會以空字串取代。  
  
-   **保留目前的語法**  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 保留目前的語法  
  
**完整模式：** 使用 ISNull 函數包裝  
  
**空字串的轉換**  
此設定會指定如何轉換空字串。 您可以針對此特定設定來設定下列選項：  
  
-   **以空格取代所有字串運算式**  
  
-   **以空格取代空字串常數**  
  
-   若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行為，請選取 [**保留目前的語法**]。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 保留目前的語法  
  
**完整模式：** 以空格取代所有字串運算式  
  
**轉換和轉換二進位字串轉換**  
將二進位值轉換成數位，可以在不同的平臺上傳回不同的值。 例如，在 x86 處理器上，CONVERT (integer，0x00000100) 會在 ASE 中傳回65536，而在中則會傳回 256 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 根據位元組順序，ASE 也會傳回不同的值。  
  
使用此設定來控制 SSMA 如何轉換包含二進位值的 CONVERT 和 CASE 運算式：  
  
-   選取 [**簡單轉換**] 以轉換運算式，而不會出現任何警告或修正。 如果您知道 ASE 伺服器的位元組順序不需要任何二進位值的變更，請使用此設定。  
  
-   選取 [**轉換] 和 [更正**] 以讓 SSMA 轉換，並更正運算式以用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 常值常數中的位元組順序將會反轉。 所有其他的二進位值 (例如二進位變數和資料行) 會標示錯誤。 如果您知道 ASE 伺服器具有需要變更二進位值的位元組順序，請使用此值。  
  
-   選取 [**轉換] 和 [標記為警告**]，讓 SSMA 轉換並更正運算式，並以警告註解標記所有已轉換的運算式。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設模式：** 具有警告的 Convert 和 mark  
  
**開放式模式：** 簡單轉換  
  
**完整模式：** 轉換和更正  
  
**動態 SQL**  
使用此設定可指定當 SSMA 在 ASE 程式碼中遇到動態 SQL 時，顯示在 [輸出] 或 [錯誤清單] 窗格中的訊息類型 (警告或錯誤) 。  
  
-   如果您選取 [**轉換] 和 [以警告標示**]，SSMA 會轉換動態 SQL 並將語句標記為警告批註。  
  
-   如果您選取 [**標記錯誤**]，SSMA 將會略過轉換，並以錯誤註解標記語句。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 具有警告的 Convert 和 mark  
  
**完整模式：** 有錯誤的標記  
  
**相等檢查轉換**  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Sql Azure 中，如果 ANSI_NullS 設定為 on， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當任何相等比較包含 null 值時，/sql azure 就會傳回 UNKNOWN。 如果 ANSI_NullS 為 off，則在比較的資料行和運算式或兩個運算式都是 null 時，包含 null 值的相等比較會傳回 true。 根據預設 (ANSINull OFF) Sybase ASE 相等比較的運作方式類似 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure，ANSI_NullS OFF。  
  
-   如果您選取 [**簡單轉換**]，SSMA 會將 ASE 程式碼轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 語法，而不需要額外檢查 null 值。 如果 ANSI_NullS 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 中關閉，或者您想要以每個案例為基礎修訂相等比較，請使用此設定。  
  
-   如果您選取 [**考慮 null 值**]，SSMA 會使用 is Null 和 IS NOT Null 子句來新增 Null 值的檢查。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 簡單轉換  
  
**完整模式：** 考慮 Null 值  
  
**格式字串**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 不再支援 PRINT 和 RAISERROR 語句中的*format_string*引數。 支援的*format_string*變數會將可取代的參數直接放在字串中，然後在執行時間取代參數。 相反地， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要使用字串常值或使用變數所建立的字串來要求完整字串。 如需詳細資訊，請參閱《線上叢書》中的「列印 ( [!INCLUDE[tsql](../../includes/tsql-md.md)]) 」主題 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
當 SSMA 遇到*format_string*引數時，可以使用變數建立字串常值，或建立新的變數，並使用該變數來建立字串。  
  
-   若要針對 PRINT 和 RAISERROR 函數使用字串常值，請選取 [**建立新字串**]。  
  
    在此模式中，如果 PRINT 或 RAISERROR 語句不使用預留位置和區域變數，則語句不會變更。 在列印字串常值中， (%% ) 的雙百分比字元變更為單一百分比字元%。  
  
    如果 PRINT 或 RAISERROR 語句使用預留位置和一或多個本機變數，如下列範例所示：  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA 會將它轉換成下列語法：  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    如果*format_string*為變數，如下列語句所示：  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA 無法執行簡單的字串轉換，而且必須建立新的變數：  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        CAST (@arg1 AS varchar(max)))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        CAST (@arg2 AS varchar(max)))  
    PRINT @print_format_1  
    ```  
    當它使用 [**建立新的字串**模式] 時，SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會假設 CONCAT_Null_YIELDS_Null 的選項為 OFF。 因此，SSMA 不會檢查是否有 null 引數。  
  
-   若要讓 SSMA 為每個 PRINT 和 RAISERROR 語句建立新的變數，然後使用該變數作為字串值，請選取 [**建立新變數**]。  
  
    在此模式中，如果 PRINT 或 RAISERROR 語句不使用預留位置和區域變數，SSMA 會以單一百分比字元取代所有的雙百分比字元 (%% ) ，以符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 語法。  
  
    如果 PRINT 或 RAISERROR 語句使用預留位置和一或多個本機變數，如下列範例所示：  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA 會將它轉換成下列語法：  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1 = 'Total: %1!%'  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))  
    PRINT @print_format_1  
    ```  
    如果*format_string*為變數，如下列語句所示：  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA 會建立新的變數，如下所示，在每個引數中檢查是否有 null 值：  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@arg1 AS varchar(max)),''))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        ISNULL(CAST (@arg2 AS varchar(max)),''))  
    PRINT @print_format_1  
    ```  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 建立新字串  
  
**完整模式：** 建立新變數  
  
**將明確的值插入 timestamp 資料行**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 不支援將明確的值插入時間戳記資料行。  
  
-   若要從 INSERT 語句中排除 timestamp 資料行，請選取 [**排除資料行**]。  
  
-   若要在每次時間戳記資料行位於 INSERT 語句時列印錯誤訊息，請選取 [**標記錯誤**]。 在此模式中，不會轉換 INSERT 語句，而且會以錯誤註解標記。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 排除資料行  
  
**完整模式：** 有錯誤的標記  
  
**儲存程式中定義的暫存物件**  
此設定會指定是否應該在轉換期間，將出現在程式中的暫存物件定義儲存在來源中繼資料中。  
  
-   選取 **[是]** 以儲存至中繼資料。  
  
-   如果不需要儲存物件，請選取 [**否**]。  
  
**預設/開放式模式：** 是的  
  
**完整模式：** 不  
  
**Proxy 資料表轉換**  
指定 ASE proxy 資料表是否轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 資料表，或不會轉換，而且程式碼會以錯誤註解標記。  
  
-   選取 [**轉換**]，將 proxy 資料表轉換成一般資料表。  
  
-   選取 [**標記錯誤**]，直接將 proxy 資料表程式碼標示為錯誤批註。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式/完整模式：** 有錯誤的標記  
  
**RAISERROR 基底訊息編號**  
ASE 使用者訊息會儲存在每個資料庫中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用者訊息會集中儲存，並可透過**sys.databases**目錄檢視取得。 此外，ASE 使用者訊息會從20000開始，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤訊息會從50001開始。  
  
此設定會指定要新增至 ASE 使用者訊息編號的數位，以將它轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者訊息。 如果您 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的使用者訊息位於**sys.databases**目錄檢視中，您可能必須將此數位變更為較高的值。 如此一來，轉換後的訊息編號就不會與現有的訊息號碼衝突。  
  
請注意：  
  
-   範圍17000-19999 中的 ASE 訊息來自于 sysmessages 系統資料表，而且不會轉換。  
  
-   如果 RAISERROR 語句中所參考的訊息編號是常數，SSMA 會將基底訊息編號加入至常數，以判斷新的使用者訊息編號。  
  
-   如果所參考的訊息編號是變數或運算式，則 SSMA 會建立中繼區域變數。  
  
-   在開放式模式中，SSMA 會假設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 選項 CONCAT_Null_YIELDS_Null 為關閉，且不會檢查 Null 引數。  
  
-   在完整模式中，SSMA 會檢查是否有 null 引數。  
  
-   未轉換具有 ERRORDATA*清單*的 RAISERROR。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式/完整模式：** 30001  
  
**系統物件**  
使用此設定可指定 SSMA 在遇到 ASE 系統物件的使用時，在 [輸出] 或 [錯誤清單] 窗格中顯示的訊息類型 (警告或錯誤) 。  
  
-   如果您選取 [**轉換] 和 [以警告標示**]，SSMA 會將參考轉換成系統物件，並將具有警告批註的語句標記為。  
  
-   如果您選取 [**標記錯誤**]，SSMA 將不會轉換系統物件的參考，而且會標示具有錯誤批註的語句。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 具有警告的 Convert 和 mark  
  
**完整模式：** 有錯誤的標記  
  
**無法解析的識別碼**  
使用此設定可指定當 SSMA 無法解析識別碼時，顯示在 [輸出] 或 [錯誤清單] 窗格中的訊息類型 (警告或錯誤) 。  
  
-   如果您選取 [**轉換] 和 [以警告標示**]，SSMA 會嘗試將參考轉換為無法解析的識別碼，並將具有警告批註的語句標記為。  
  
-   如果您選取 [**標記錯誤**]，SSMA 將不會將參考轉換為無法解析的識別碼，而且會將具有錯誤批註的語句標記為。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 具有警告的 Convert 和 mark  
  
**完整模式：** 有錯誤的標記  
  
## <a name="system-function-options"></a>系統函數選項  
**CHARINDEX 函數**  
在 ASE 中，只有在所有輸入運算式都是 Null 時，CHARINDEX 才會傳回 Null。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果任何輸入運算式為 Null，則 SQL Azure 會傳回 Null。  
  
-   若要使用 ASE 行為，請選取 [**取代**函式]。 所有對 CHARINDEX 函式的呼叫都會以 CHARINDEX_VARCHAR 或 CHARINDEX_NVARCHAR 使用者定義函式的呼叫來取代，這是根據 (在架構名稱的 2ss ' ) 的使用者資料庫中建立的參數類型來模擬 Sybase ASE 行為。  
  
-   若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行為，請選取 [**保留目前的語法**]。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 保留目前的語法  
  
**完整模式：** Replace 函式  
  
**DATALENGTH 函數**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當值為單一空格時，DATALENGTH 函數所傳回的值會有所不同/SQL Azure 和 ASE。 在此情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 會傳回0，而 ASE 會傳回1。  
  
-   若要使用 ASE 行為，請選取 [**取代**函式]。 所有對 DATALENGTH 函式的呼叫都會以 CASE 運算式來取代，以模擬 Sybase ASE 行為。  
  
-   若要使用預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行為，請選取 [**保留目前的語法**]。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 保留目前的語法  
  
**完整模式：** Replace 函式  
  
**INDEX_COL 函數**  
ASE 支援 INDEX_COL 函數的選擇性*user_id*引數;不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 不支援此引數。 如果您使用*user_id*引數，則此函式無法轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 語法。  
  
-   若要使用 ASE 行為，請選取 [**轉換函數**]。 如果程式碼包含*user_id*引數，SSMA 將會顯示錯誤。  
  
-   若要在每次遇到 INDEX_COL 時顯示錯誤訊息，請選取 [**標記錯誤**]。 SSMA 不會將參考轉換為函式，且會將具有錯誤批註的語句標記為。  
  
**預設/開放式/完整模式：** 有錯誤的標記  
  
**INDEX_COLORDER 函式**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 沒有 INDEX_COLORDER 的系統函數。  
  
-   若要使用 ASE 行為，請選取 [**轉換函數**]。 對 INDEX_COLORDER 函式的所有呼叫都會以 INDEX_COLORDER (在使用者資料庫中建立的使用者定義函式的呼叫來取代，該函式是在模擬 Sybase ASE 行為的架構名稱的 2ss ' ) 之下。  
  
-   若要在每次遇到 INDEX_COLORDER 時列印錯誤訊息，請選取 [**標記錯誤**]。 SSMA 不會將參考轉換為函式，且會將具有錯誤批註的語句標記為。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式/完整模式：** 有錯誤的標記  
  
**LEFT 和 RIGHT 函數**  
Sybase 中的 Left 和 Right 函式會以不同的方式來表示負值長度參數。  
  
-   若要使用 ASE 行為，請選取 [**取代**函式]。 然後，會以 CASE 運算式取代 length 參數，這會傳回負數值的 null。  
  
-   若要使用 SQL Server 行為，請選取 [**保留目前的語法**]  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 保留目前的語法  
  
**完整模式：** Replace 函式  
  
> [!NOTE]  
> 如果 length 參數是常值，而不是複雜運算式，則不論專案設定，長度值一律會以 null 取代。  
  
**NEXT_IDENTITY 函式**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 沒有 NEXT_IDENTITY 的系統函數。  
  
-   若要使用 ASE 行為，請選取 [**轉換函數**]。 NEXT_IDENTITY 函式的所有呼叫都會以運算式 (取代 IDENT_CURRENT (參數值) + IDENT_INCR (參數值) 模擬 Sybase ASE 行為。  
  
-   若要在每次遇到 NEXT_IDENTITY 時列印錯誤訊息，請選取 [**標記錯誤**]。 SSMA 不會將參考轉換為函式，且會將具有錯誤批註的語句標記為。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式/完整模式：** 有錯誤的標記  
  
**PATINDEX 函數**  
指定是否要轉換 PATINDEX 函式，以符合 Sybase ASE 行為。 重點是，Sybase 會修剪搜尋模式中的尾端空白。 因應措施是將值運算式轉換成具有最大精確度的固定長度資料類型，並將 rtrim 函數套用至搜尋模式。  
  
-   若要使用 ASE 行為，請選取 [**使用**]。  
  
-   若要使用預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行為，請選取 [**不使用**]。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 不要使用  
  
**完整模式：** 使用  
  
**REPLICATE 函數**  
複寫函數會以指定的次數重複字串。 在 ASE 中，如果您指定要重複字串零次，結果會是 null。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 中，結果是空字串。  
  
-   若要使用 ASE 行為，請選取 [**取代**函式]。 所有對複寫函式的呼叫都會以 REPLICATE_VARCHAR 或 REPLICATE_NVARCHAR 使用者定義函式的呼叫來取代，這是根據 (在架構名稱的 2ss ' ) 的使用者資料庫中建立的參數類型來模擬 Sybase ASE 行為。  
  
-   若要使用預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行為，請選取 [**取代函數**]。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式/完整模式：** Replace 函式  
  
**TRIM (LTRIM，RTRIM) 函數**  
此設定指定是否要使用 Sybase ASE 對等語法函式來取代 Trim (LTRIM、RTRIM) 函數的呼叫，或是保留目前的語法。 此特定設定有下列選項：  
  
-   **Replace 函式**  
  
-   **保留目前的語法**  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式/完整模式：** Replace 函式  
  
**SUBSTRING 函數**  
在 ASE 中， `SUBSTRING(expression, start, length)` 如果指定的起始值大於 expression 中的字元數，或長度等於零，此函數會傳回 Null。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 中，對等運算式會傳回空字串。  
  
-   若要使用 ASE 行為，請選取 [**取代**函式]。 所有對 SUBSTRING 函式的呼叫都會以 SUBSTRING_VARCHAR 或 SUBSTRING_NVARCHAR 或 SUBSTRING_VARBINARY 使用者定義函式的呼叫來取代，這是以架構名稱的 2ss ' ) 下的使用者資料庫中建立的 (參數類型為基礎，以模擬 Sybase ASE 行為。  
  
-   若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行為，請選取 [**保留目前的語法**]。  
  
當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 保留目前的語法  
  
**完整模式：** Replace 函式  
  
## <a name="tables"></a>TABLES  
**新增主要金鑰**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果 Access 資料表沒有主鍵或唯一索引，則在或 SQL Azure 資料表中建立新的主要金鑰。  
  
-   **預設模式**： False  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
> [!NOTE]  
> 連線到 SQL Azure 時，預設為 True。  
  
## <a name="see-also"></a>另請參閱  
[&#40;SybaseToSQL&#41;的使用者介面參考](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
