---
description: 專案設定 (轉換) (SybaseToSQL)
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
ms.openlocfilehash: 61795be0d1f851792846f2ede8c38eca1f3801b0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468792"
---
# <a name="project-settings-conversion-sybasetosql"></a>專案設定 (轉換) (SybaseToSQL)
[ **專案設定** ] 對話方塊的 [轉換] 頁面包含的設定，可自訂 SSMA 如何將 Sybase 自我調整 Server ENTERPRISE (ASE) 語法轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Azure 語法。  
  
您可以在 [ **專案設定** ] 和 [ **預設專案設定** ] 對話方塊中使用 [轉換] 窗格：  
  
-   如果您想要指定所有 SSMA 專案的設定，請在 [ **工具** ] 功能表上選取 [ **預設專案設定**]，按一下左窗格底部的 **[一般** ]，然後按一下 [ **轉換**]。  
  
-   若要指定目前專案的設定，請在 [ **工具** ] 功能表上選取 [ **專案設定**]，按一下左窗格底部的 **[一般** ]，然後按一下 [ **轉換**]。  
  
## <a name="miscellaneous-options"></a>其他選項  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 和 ASE 使用不同的錯誤碼。  
  
使用此設定可指定當 SSMA 在 ASE 程式碼中遇到 **@ @ERROR **的參考時，出現在 [輸出] 或 [錯誤清單] 窗格中的訊息類型 (警告或錯誤) 。  
  
-   如果您選取 [ **轉換] 和 [標記為警告**]，SSMA 會轉換語句，並以警告註解標記這些語句。  
  
-   如果您選取 [ **標記錯誤**]，SSMA 會略過轉換，並將語句標記為錯誤批註。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 轉換並標示警告  
  
**完整模式：** 標記錯誤  
  
**LIKE 運算子的轉換**  
指定是否將 LIKE 運算元轉換成符合 Sybase ASE 行為。 重點是，Sybase 會修剪類似模式中的尾端空白。 因應措施是以最大有效位數將 right 運算式轉換成固定長度的資料類型。  
  
-   選取 [ **簡單轉換** ] 以轉換運算式，而不進行任何更正。  
  
-   若要使用 ASE 行為，請選取 [ **轉換成固定長度]。**  
  
當您在 [模式] 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式**：簡單轉換  
  
**Full 模式**：轉換成固定長度  
  
**將空字串轉換或轉換成數數值型別**  
指定如何處理以數數值型別作為 datatype 引數的 CONVERT 或 CAST 運算式內的空白或空白字串。 下列選項可用於此設定：  
  
-   選取 [ **簡單轉換** ] 以轉換運算式，而不進行任何更正。  
  
-   如果選取了 **空字串作為零** 值，則字串參數 {s} 將會以 case ltrim 取代 (rtrim ( {s} ) # A3 WHEN "" then 0 else {s} END 運算式  
  
當您在 [模式] 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式**：簡單轉換  
  
**Full 模式**：空字串為零數值  
  
**Null 的串連**  
此設定會指定如何使用 Null 來轉換字串串連。 您可以針對此特定設定設定下列選項：  
  
-   **使用 ISNull 函數包裝：** 如果設定此選項，串連中的每個非常數 ' string_expression ' 都會以 ISNull (string_expression) ，而 Null 將會取代為空字串。  
  
-   **保留目前的語法**  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 保留目前的語法  
  
**完整模式：** 使用 ISNull 函數換行  
  
**空字串的轉換**  
此設定會指定如何轉換空字串。 您可以針對此特定設定設定下列選項：  
  
-   **將所有字串運算式取代為空格**  
  
-   **以空格取代空白字串常數**  
  
-   若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行為，請選取 [ **保留目前的語法**]。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 保留目前的語法  
  
**完整模式：** 將所有字串運算式取代為空格  
  
**轉換和轉換二進位字串轉換**  
將二進位值轉換成數位，可以在不同的平臺上傳回不同的值。 例如，在 x86 處理器上，轉換 (整數，0x00000100) 會在中的 ASE 和256傳回 65536 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 ASE 也會根據位元組順序傳回不同的值。  
  
您可以使用此設定來控制 SSMA 如何轉換包含二進位值的 CONVERT 和 CASE 運算式：  
  
-   選取 [ **簡單轉換** ] 可轉換運算式，但不含任何警告或修正。 如果您知道 ASE 伺服器的位元組順序不需要任何二進位值的變更，請使用此設定。  
  
-   選取 [ **轉換] 和 [更正** ]，讓 SSMA 轉換及更正要用於的運算式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 常值常數中的位元組順序將會反轉。 所有其他的二進位值 (例如二進位變數和資料行) 都會標記為錯誤。 如果您知道 ASE 伺服器的位元組順序需要變更二進位值，請使用此值。  
  
-   選取 [ **轉換並標示警告** ] 以讓 SSMA 轉換及更正運算式，並使用警告註解標記所有已轉換的運算式。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設模式：** 轉換並標示警告  
  
**開放式模式：** 簡單轉換  
  
**完整模式：** 轉換和修正  
  
**動態 SQL**  
使用此設定可指定當 SSMA 在 ASE 程式碼中遇到動態 SQL 時，出現在 [輸出] 或 [錯誤清單] 窗格中的訊息類型 (警告或錯誤) 。  
  
-   如果您選取 [ **轉換並標示為警告**]，SSMA 會轉換動態 SQL，並將語句標記為警告批註。  
  
-   如果您選取 [ **標記錯誤**]，SSMA 會略過轉換，並將語句標記為錯誤批註。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 轉換並標示警告  
  
**完整模式：** 標記錯誤  
  
**相等檢查轉換**  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /Sql azure 中，如果 ANSI_NullS 設定是 on， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當任何相等比較包含 null 值時，SQL Azure 會傳回 UNKNOWN。 如果 ANSI_NullS 為 off，當比較的資料行和運算式或兩個運算式都是 null 時，包含 null 值的相等比較就會傳回 true。 根據預設 (ANSINull OFF) Sybase ASE 相等比較的行為類似于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 並 ANSI_NullS OFF。  
  
-   如果您選取 **簡單轉換**，SSMA 會將 ASE 程式碼轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 語法，而不需要額外檢查 null 值。 如果 ANSI_NullS 在/SQL Azure 中為 off， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或您想要針對每個案例修訂相等比較，請使用此設定。  
  
-   如果您選取 [ **考慮 null 值**]，SSMA 將會使用 [是 null] 和 [非 Null] 子句來加入 null 值的檢查。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 簡單轉換  
  
**完整模式：** 考慮 Null 值  
  
**格式字串**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 不再支援 PRINT 和 RAISERROR 語句中的 *format_string* 引數。 *Format_string*變數支援將可替換參數直接放在字串中，然後在執行時間取代參數。 相反地，您 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須使用字串常值或使用變數所建立的字串，來要求使用完整字串。 如需詳細資訊，請參閱《線上叢書》中的「列印 ( [!INCLUDE[tsql](../../includes/tsql-md.md)]) 」主題 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
當 SSMA 遇到 *format_string* 引數時，可以使用變數來建立字串常值，或建立新的變數，並使用該變數建立字串。  
  
-   若要針對 PRINT 和 RAISERROR 函數使用字串常值，請選取 [ **建立新字串**]。  
  
    在此模式中，如果 PRINT 或 RAISERROR 語句不使用預留位置和區域變數，則語句會維持不變。 雙百分比字元 (%% ) 在列印字串常值中變更為單一百分比字元%。  
  
    如果 PRINT 或 RAISERROR 語句使用預留位置和一或多個本機變數，如下列範例所示：  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA 會將它轉換成下列語法：  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    如果 *format_string* 是變數，如下列語句所示：  
  
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
    當它使用 **建立新的字串** 模式時，SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會假設選項 CONCAT_Null_YIELDS_Null 為 OFF。 因此，SSMA 不會檢查是否有 null 引數。  
  
-   若要讓 SSMA 為每一個 PRINT 和 RAISERROR 語句建立新的變數，然後使用該變數作為字串值，請選取 [ **建立新變數**]。  
  
    在此模式中，如果 PRINT 或 RAISERROR 語句未使用預留位置和區域變數，SSMA 會以單一百分比字元取代 (%% ) 的所有雙百分比字元，以符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 語法。  
  
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
    如果 *format_string* 是變數，如下列語句所示：  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA 會建立新的變數，如下所示，檢查每個引數中的 null 值：  
  
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
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 建立新字串  
  
**完整模式：** 建立新變數  
  
**將明確值插入時間戳記資料行**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 不支援將明確值插入時間戳記資料行。  
  
-   若要從 INSERT 語句中排除時間戳記資料行，請選取 [ **排除資料行**]。  
  
-   若要在每次將時間戳記資料行放在 INSERT 語句時列印錯誤訊息，請選取 [ **標記錯誤**]。 在此模式中，將不會轉換 INSERT 語句，而且會以錯誤註解標記。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 排除資料行  
  
**完整模式：** 標記錯誤  
  
**儲存程式中定義的暫存物件**  
這項設定會指定是否應該在轉換期間，將出現在程式中的暫存物件定義儲存在來源中繼資料中。  
  
-   選取 **[是]**  以儲存到中繼資料。  
  
-   如果不需要儲存物件，請選取 [ **否**  ]。  
  
**預設/開放式模式：** 是的  
  
**完整模式：** 不  
  
**Proxy 資料表轉換**  
指定 ASE proxy 資料表是否轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 資料表，或是不會轉換，而且程式碼會標示錯誤批註。  
  
-   選取 [ **轉換** ] 將 proxy 資料表轉換為一般資料表。  
  
-   選取 [ **標記錯誤** ]，直接以錯誤註解標記 proxy 資料表程式碼。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式/完整模式：** 標記錯誤  
  
**RAISERROR 基本訊息編號**  
ASE 使用者訊息會儲存在每個資料庫中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統會集中儲存使用者訊息，並透過 **sys. messages** 目錄檢視提供這些訊息。 此外，ASE 使用者訊息從20000開始，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤訊息從50001開始。  
  
此設定會指定要新增至 ASE 使用者訊息編號的數位，以將其轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者訊息。 如果您 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在 **sys. 訊息** 目錄檢視中有使用者訊息，您可能必須將此數位變更為較高的值。 這是因為轉換的訊息編號不會與現有的訊息編號衝突。  
  
請注意：  
  
-   範圍17000-19999 中的 ASE 訊息是來自 sysmessages 系統資料表，且不會進行轉換。  
  
-   如果 RAISERROR 語句中參考的訊息編號是常數，SSMA 會將基底訊息編號新增至常數，以判斷新的使用者訊息編號。  
  
-   如果所參考的訊息編號是變數或運算式，SSMA 將會建立中繼區域變數。  
  
-   在開放式模式中，SSMA 會假設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CONCAT_Null_YIELDS_Null 的選項是關閉的，而且不會檢查 Null 引數。  
  
-   在完整模式中，SSMA 會檢查是否有 null 引數。  
  
-   具有 ERRORDATA *清單* 的 RAISERROR 不會轉換。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式/完整模式：** 30001  
  
**系統物件**  
使用此設定可指定 SSMA 在 [輸出] 或 [錯誤清單] 窗格中所顯示的訊息類型 (警告或) 錯誤，並在遇到使用 ASE 系統物件時出現的錯誤。  
  
-   如果您選取 [ **轉換] 和 [標記為警告**]，SSMA 將會轉換系統物件的參考，並將語句標記為警告批註。  
  
-   如果您選取 [ **標記但有錯誤**]，SSMA 將不會轉換系統物件的參考，而且會以錯誤註解標記語句。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 轉換並標示警告  
  
**完整模式：** 標記錯誤  
  
**未解析的識別碼**  
使用此設定可指定當 SSMA 在無法解析識別碼時，顯示在 [輸出] 或 [錯誤清單] 窗格中的訊息類型 (警告或錯誤) 。  
  
-   如果您選取 [ **轉換] 和 [標記為警告**]，SSMA 會嘗試將參考轉換為無法解析的識別碼，並將語句標記為警告批註。  
  
-   如果您選取 [ **標記錯誤**]，則 SSMA 不會將參考轉換為無法解析的識別碼，而且會將語句標記為錯誤批註。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 轉換並標示警告  
  
**完整模式：** 標記錯誤  
  
## <a name="system-function-options"></a>系統函數選項  
**CHARINDEX 函數**  
在 ASE 中，只有當所有輸入運算式都是 Null 時，CHARINDEX 才會傳回 Null。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果任何輸入運算式為 Null，則 SQL Azure 會傳回 Null。  
  
-   若要使用 ASE 行為，請選取 [ **取代**函式]。 所有對 CHARINDEX 函式的呼叫都會根據在使用者資料庫中 (建立的參數類型（在架構名稱的 2ss ' ) 下）所傳遞的參數類型來取代 CHARINDEX_VARCHAR 或 CHARINDEX_NVARCHAR 使用者定義函數，以模擬 Sybase ASE 行為。  
  
-   若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行為，請選取 [ **保留目前的語法**]。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 保留目前的語法  
  
**完整模式：** Replace 函式  
  
**DATALENGTH 函數**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當值為單一空格時，DATALENGTH 函式所傳回的值會有/SQL Azure 和 ASE 不同的值。 在此情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 會傳回0，而 ASE 會傳回1。  
  
-   若要使用 ASE 行為，請選取 [ **取代**函式]。 所有對 DATALENGTH 函式的呼叫都會以 CASE 運算式替代，以模擬 Sybase ASE 行為。  
  
-   若要使用預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行為，請選取 [ **保留目前的語法**]。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 保留目前的語法  
  
**完整模式：** Replace 函式  
  
**INDEX_COL 函數**  
ASE 支援 INDEX_COL 函數的選擇性 *user_id* 引數;不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 不支援這個引數。 如果您使用 *user_id* 引數，此函式不能轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 語法。  
  
-   若要使用 ASE 行為，請選取 [ **轉換**函式]。 如果程式碼包含 *user_id* 引數，SSMA 將會顯示錯誤。  
  
-   若要在每次遇到 INDEX_COL 時顯示錯誤訊息，請選取 [ **標記錯誤**]。 SSMA 將不會轉換函式的參考，而且會將語句標記為錯誤批註。  
  
**預設/開放式/完整模式：** 標記錯誤  
  
**INDEX_COLORDER 函式**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 沒有 INDEX_COLORDER 系統函數。  
  
-   若要使用 ASE 行為，請選取 [ **轉換**函式]。 所有對 INDEX_COLORDER 函式的呼叫都會以名稱相同的使用者定義函數的呼叫來取代 INDEX_COLORDER (在使用者資料庫中建立的使用者 ) 資料庫，會模擬 Sybase ASE 行為。  
  
-   若要在每次遇到 INDEX_COLORDER 時列印錯誤訊息，請選取 [ **標記錯誤**]。 SSMA 將不會轉換函式的參考，而且會將語句標記為錯誤批註。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式/完整模式：** 標記錯誤  
  
**左邊和右邊函數**  
Sybase 中的 Left 和 Right 函式的行為與負數長度參數的行為不同。  
  
-   若要使用 ASE 行為，請選取 [ **取代**函式]。 然後，會將 length 參數取代為負數值的 CASE 運算式。  
  
-   若要使用 SQL Server 行為，請選取 [**保留目前的語法**]。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 保留目前的語法  
  
**完整模式：** Replace 函式  
  
> [!NOTE]  
> 如果長度參數是常值而不是複雜運算式，則不論專案設定是什麼，長度值一律會以 null 取代。  
  
**NEXT_IDENTITY 函式**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure 沒有 NEXT_IDENTITY 系統函數。  
  
-   若要使用 ASE 行為，請選取 [ **轉換**函式]。 NEXT_IDENTITY 函式的所有呼叫都會取代為運算式 (IDENT_CURRENT (參數值) + IDENT_INCR (參數值) 可模擬 Sybase ASE 行為。  
  
-   若要在每次遇到 NEXT_IDENTITY 時列印錯誤訊息，請選取 [ **標記錯誤**]。 SSMA 將不會轉換函式的參考，而且會將語句標記為錯誤批註。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式/完整模式：** 標記錯誤  
  
**PATINDEX 函數**  
指定是否轉換 PATINDEX 函式以符合 Sybase ASE 行為。 重點是，Sybase 會在搜尋模式中修剪尾端空白。 因應措施是將值運算式轉換成具有最大精確度的固定長度資料類型，並將 rtrim 函數套用至搜尋模式。  
  
-   若要使用 ASE 行為，請選取 [ **使用**]。  
  
-   若要使用預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行為，請選取 [ **不使用**]。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 請勿使用  
  
**完整模式：** 使用  
  
**REPLICATE 函數**  
複寫函數會以指定的次數重複字串。 在 ASE 中，如果您指定重複字串零次，則結果為 null。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 中，結果會是空字串。  
  
-   若要使用 ASE 行為，請選取 [ **取代**函式]。 所有對複寫函式的呼叫都會以 REPLICATE_VARCHAR 或 REPLICATE_NVARCHAR 使用者定義函式的呼叫來取代，並根據架構名稱 2ss ' ) 的使用者資料庫中 (建立的參數類型，來模擬 Sybase ASE 行為。  
  
-   若要使用預設 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行為，請選取 [ **取代**函式]。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式/完整模式：** Replace 函式  
  
**TRIM (LTRIM，RTRIM) 函數**  
這項設定會指定是否要使用 Sybase ASE 相等的語法函式來取代對 Trim (LTRIM、RTRIM) 函式的呼叫，或保留目前的語法。 此特定設定有下列選項：  
  
-   **Replace 函式**  
  
-   **保留目前的語法**  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式/完整模式：** Replace 函式  
  
**SUBSTRING 函數**  
在 ASE 中， `SUBSTRING(expression, start, length)` 如果指定的起始值大於運算式中的字元數，或如果長度等於零，則函數會傳回 Null。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 中，對應的運算式會傳回空字串。  
  
-   若要使用 ASE 行為，請選取 [ **取代**函式]。 對 SUBSTRING 函式的所有呼叫都會以 SUBSTRING_VARCHAR 或 SUBSTRING_NVARCHAR 或 SUBSTRING_VARBINARY 使用者定義函數的呼叫來取代，並根據架構名稱的 2ss ' ) 中 (在使用者資料庫中建立的參數類型，來模擬 Sybase ASE 行為。  
  
-   若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure 行為，請選取 [ **保留目前的語法**]。  
  
當您在 [ **模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：  
  
**預設/開放式模式：** 保留目前的語法  
  
**完整模式：** Replace 函式  
  
## <a name="tables"></a>TABLES  
**新增主要金鑰**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果 Access 資料表沒有 primary key 或 unique 索引，則在或 SQL Azure 資料表中建立新的主鍵。  
  
-   **預設模式**： False  
  
-   **開放式模式**： False  
  
-   **完整模式**： True  
  
> [!NOTE]  
> 連線到 SQL Azure 時，預設為 True。  
  
## <a name="see-also"></a>另請參閱  
[消費者介面參考 &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
