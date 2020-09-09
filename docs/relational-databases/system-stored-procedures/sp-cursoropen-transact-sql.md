---
description: sp_cursoropen (Transact-SQL)
title: sp_cursoropen (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoropen
- sp_cursoropen_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoropen
ms.assetid: 16462ede-4393-4293-a598-ca88c48ca70b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2942c06e5d63c0be25a05cd34e871447a29e7d6d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543570"
---
# <a name="sp_cursoropen-transact-sql"></a>sp_cursoropen (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  開啟資料指標。 sp_cursoropen 定義與資料指標和資料指標選項相關聯的 SQL 語句，然後填入資料指標。 sp_cursoropen 相當於 [!INCLUDE[tsql](../../includes/tsql-md.md)] DECLARE_CURSOR 和 OPEN 語句的組合。 這個程序的叫用方式是在表格式資料流 (TDS) 封包中指定 ID = 2。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursoropen cursor OUTPUT, stmt  
    [, scrollopt[ OUTPUT ] [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,boundparam][,...n]]] ]]  
```  
  
## <a name="arguments"></a>引數  
 *cursor*  
 SQL Server 產生的資料指標識別碼。 資料*指標*是必須在牽涉到資料指標的所有後續程式上提供的*控制碼*值，例如 sp_cursorfetch。 *cursor* 是具有 **int** 傳回值的必要參數。  
  
 資料*指標*允許多個資料指標在單一資料庫連接上處於作用中狀態。  
  
 *stmt*  
 這是定義資料指標結果集的必要參數。 任何有效的查詢字串 (任何字串類型的語法和系結)  (無論 Unicode、大小等等，) 都可作為有效的 *stmt* 值型別。  
  
 *scrollopt*  
 捲動選項。 *scrollopt* 是選擇性參數，它需要下列其中一個 **int** 輸入值。  
  
|值|描述|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 由於要求的值可能不適合由 *stmt*定義的資料指標，所以這個參數會當做輸入和輸出。 在這類情況下，SQL Server 會指派適合的值。  
  
 *ccopt*  
 並行控制選項。 *ccopt* 是選擇性參數，它需要下列其中一個 **int** 輸入值。  
  
|值|描述|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (之前稱為 LOCKCC)|  
|0x0004|**開放式** (先前稱為 OPTCC) |  
|0x0008|OPTIMISTIC (之前稱為 OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 如同 *scrollopt*， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以覆寫要求的 *ccopt* 值。  
  
 *計數*  
 要搭配 AUTO_FETCH 使用的提取緩衝區資料列數目。 預設為 20 個資料列。 當指派為輸入值與傳回值時， *rowcount*的行為會有所不同。  
  
|當做輸入值|當做傳回值|  
|--------------------|---------------------|  
|當指定 AUTO_FETCH 的 *scrollopt* 值時， *rowcount* 代表要放入提取緩衝區中的資料列數目。<br /><br /> 注意：當指定 AUTO_FETCH 時，>0 是有效的值，否則會被忽略。|代表結果集中的資料列數目，但在指定 *scrollopt* AUTO_FETCH 值時除外。|  
  
-  
  
 *boundparam*  
 表示使用其他參數。 *boundparam* 是選擇性參數，如果 *scrollopt* PARAMETERIZED_STMT 值設定為 ON，則應該指定此參數。  
  
## <a name="return-code-values"></a>傳回碼值  
 如果引發了錯誤，sp_cursoropen 會傳回下列其中一個值。  
  
 0  
 已成功執行程序。  
  
 0x0001  
 執行期間發生錯誤 (不是太嚴重的錯誤，所以不會引發操作錯誤)。  
  
 0x0002  
 非同步作業進行中。  
  
 0x0002  
 FETCH 作業進行中。  
  
 A  
 這個資料指標已經由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 取消配置而且無法使用。  
  
 當引發錯誤時，傳回值可能會不一致，而且無法保證其精確度。  
  
 當 *rowcount* 參數指定為傳回值時，會發生下列結果集。  
  
 -1  
 當資料列數未知或不適用時傳回。  
  
 -n  
 當非同步擴展在作用中時傳回。 表示指定 *scrollopt* AUTO_FETCH 值時，放入提取緩衝區中的資料列數目。  
  
 如果 RPC 在使用中，傳回值如下。  
  
 0  
 程序成功。  
  
 1  
 程序失敗。  
  
 2  
 正在以非同步方式產生索引鍵集資料指標。  
  
 16  
 已經自動關閉向前快轉的資料指標。  
  
> [!NOTE]  
>  如果 sp_cursoropen 程式成功執行，則會傳送具有 TDS 資料行格式資訊 (0xa0 & 0xa1 訊息) 的 RPC 傳回參數和結果集。 如果不成功，則會傳送一個或多個 TDS 錯誤訊息。 無論是哪一種情況，都不會傳回任何資料列資料，而 *完成* 的訊息計數將會是零。 如果您正在使用早於 7.0 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本，則會傳回 0xa0、0xa1 (SELECT 陳述式的標準) 連同 0xa5 和 0xa4 Token 資料流。 如果您正在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0，則會傳回 0x81 (SELECT 陳述式的標準) 連同 0xa5 和 0xa4 Token 資料流。  
  
## <a name="remarks"></a>備註  
  
## <a name="stmt-parameter"></a>stmt 參數  
 如果 *stmt* 指定預存程式的執行，則可以將輸入參數定義為 *stmt* 字串的一部分常數，或指定為 *boundparam* 引數。 宣告的變數可依照這種方式傳遞為繫結參數。  
  
 所允許的 *stmt* 參數內容取決於 *ccopt* ALLOW_DIRECT 傳回值是否已連結或 *ccopt* 值的其餘部分，亦即：  
  
-   如果未指定 ALLOW_DIRECT，就 [!INCLUDE[tsql](../../includes/tsql-md.md)] 必須使用針對包含單一 SELECT 語句的預存程式所呼叫的 SELECT 或 EXECUTE 語句。 此外，SELECT 陳述式必須符合資料指標的資格，也就是說，它不得包含關鍵字 SELECT INTO 或 FOR BROWSE。  
  
-   如果指定了 ALLOW_DIRECT，這可能會產生一個或多個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，包括之後搭配多個陳述式執行其他預存程序的那些陳述式。 非 SELECT 陳述式或包含關鍵字 SELECT INTO 或 FOR BROWSE 的任何 SELECT 陳述式將只會執行，而不會建立資料指標。 包括在多個陳述式批次內的任何 SELECT 陳述式也是相同的情況。 如果 SELECT 陳述式包含只與資料指標有關的子句，將會忽略這些子句。 例如，當 *ccopt* 的值為0x2002 時，這就是的要求：  
  
    -   如果只有單一 SELECT 陳述式符合資料指標的資格，則為具有捲動鎖定的資料指標，或是  
  
    -   如果有多個陳述式、單一非 SELECT 陳述式或者不符合資料指標資格的 SELECT 陳述式，則為直接執行陳述式。  
  
## <a name="scrollopt-parameter"></a>scrollopt 參數  
 前五個 *scrollopt* 值 (KEYSEY、DYNAMIC、FORWARD_ONLY、STATIC 和 FAST_FORWARD) 彼此互斥。  
  
 PARAMETERIZED_STMT 和 CHECK_ACCEPTED_TYPES 可以透過 OR 連結到前五個值的任何一個。  
  
 AUTO_FETCH 和 AUTO_CLOSE 可以透過 OR 連結到 FAST_FORWARD。  
  
 如果 CHECK_ACCEPTED_TYPES 為 ON，則最後五個 *scrollopt* 值中至少一個 (KEYSET_ACCEPTABLE `,` DYNAMIC_ACCEPTABLE、FORWARD_ONLY_ACCEPTABLE、STATIC_ACCEPTABLE 或 FAST_FORWARD_ACCEPTABLE) 也必須是 on。  
  
 STATIC 資料指標永遠都會當做 READ_ONLY 開啟。 這表示基礎資料表無法透過這個資料指標來更新。  
  
## <a name="ccopt-parameter"></a>ccopt 參數  
 前四個 *ccopt* 值 (READ_ONLY、SCROLL_LOCKS，以及兩個開放式值) 彼此互斥。  
  
> [!NOTE]  
>  選擇前四個 *ccopt* 值的其中一個，以指定資料指標是否為唯讀，或者是否使用鎖定或開放式方法來防止更新遺失。 如果未指定 *ccopt* 值，預設值為開放式。  
  
 ALLOW_DIRECT 和 CHECK_ACCEPTED_TYPES 可以透過 OR 連結到前四個值的任何一個。  
  
 UPDT_IN_PLACE 可以透過 OR 連結到 READ_ONLY、SCROLL_LOCKS 或者 OPTIMISTIC 值的其中一個。  
  
 如果 CHECK_ACCEPTED_TYPES 為 ON，則最後四個 *ccopt* 值中至少一個 (READ_ONLY_ACCEPTABLE、SCROLL_LOCKS_ACCEPTABLE，以及 OPTIMISTIC_ACCEPTABLE 值的其中一個) 也必須是 on。  
  
 定點更新和刪除函式只能在提取緩衝區內執行，而且只有在 *ccopt* 值等於 SCROLL_LOCKS 或開放式時才會執行。 如果 SCROLL_LOCKS 是指定的值，則保證此作業一定成功。 如果 OPTIMISTIC 是指定的值，則當資料列在上一次提取之後已經變更時，作業將會失敗。  
  
 這個失敗的原因是因為當 OPTIMISTIC 是指定的值時，將會比較時間戳記或總和檢查碼的值來執行開放式並行控制函數，如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所決定。 如果這些資料列的任何一個都不符合，作業將會失敗。  
  
 指定 UPDT_IN_PLACE 當做傳回值會控制下列結果：  
  
-   如果未設定何時在具有唯一索引的資料表上執行定點更新，資料指標會從它的工作資料表刪除資料列，並將它插入資料指標所使用之任何索引鍵資料行的結尾，藉此變更這些資料行。  
  
-   如果設定 ON，資料指標只會更新工作資料表原始資料列中的索引鍵資料行。  
  
## <a name="bound_param-parameter"></a>bound_param 參數  
 根據程式碼中的錯誤訊息，指定 PARAMETERIZED_STMT 時，必須 *paramdef* 參數名稱。 如果未指定 PARAMETERIZED_STMT，錯誤訊息中不會指定任何名稱。  
  
## <a name="rpc-considerations"></a>RPC 考量  
 RPC RETURN_METADATA 輸入旗標可以設定為 0x0001，要求在 TDS 資料流中傳回資料指標選取清單中繼資料。  
  
## <a name="examples"></a>範例  
  
### <a name="bound_param-parameter"></a>bound_param 參數  
 第五個之後的任何參數都會當做輸入參數傳遞給陳述式計畫。 第一個參數必須是以下格式的字串：  
  
 *{區域變數名稱資料類型}[,...n-1*  
  
 後續的參數會用來傳遞要在語句中用來替代 *區域變數名稱* 的值。  
  
## <a name="see-also"></a>另請參閱  
 [sp_cursorfetch &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
