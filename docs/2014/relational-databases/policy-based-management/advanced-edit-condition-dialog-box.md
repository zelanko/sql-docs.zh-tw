---
title: 進階編輯 (條件) 對話方塊 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.condition.advancededit.f1
ms.assetid: a0bbe501-78c5-45ad-9087-965d04855663
caps.latest.revision: 42
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2dc35e9080637129f69115a22e5f208be9ecad19
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37205408"
---
# <a name="advanced-edit-condition-dialog-box"></a>進階編輯 (條件) 對話方塊
  使用 [進階編輯] 對話方塊可針對以原則為基礎的管理條件建立複雜運算式。  
  
## <a name="options"></a>選項。  
 **資料格值**  
 顯示在您建立時將用於資料格值的函數或運算式。 當您按一下 **[確定]** 時，資料格值將會出現在 **[一般]** 頁面上 **[建立新條件]** 或 **[開啟條件]** 對話方塊之條件運算式方塊內的 **[欄位]** 或 **[值]** 資料格中。  
  
 **函數和屬性**  
 顯示可用的函數和屬性。  
  
 **詳細資料**  
 使用以下格式顯示有關函數和屬性的資訊：函數簽名碼、函數描述、傳回值和範例。  
  
## <a name="syntax"></a>語法  
 有效的運算式必須是下列格式：  
  
 `{property | function | constant}`  
  
 `{operator}`  
  
 `{property | function | constant}`  
  
## <a name="examples"></a>範例  
 某些有效運算式的範例如下：  
  
-   *Property1*> 5  
  
-   *Property1*=*Property2*  
  
-   Add(5, Multiply(.2,*Property1*))<*Property2*  
  
-   *Sometext* IN *Property1*  
  
-   *Property1* \< Fn (*Property2*)  
  
-   BitwiseAnd(*Property1*,*Property2*)= 0  
  
## <a name="additional-function-information"></a>其他函數資訊  
 下列章節提供詳細資訊，關於您可用於針對以原則為基礎的管理條件建立複雜運算式的函數。  
  
> [!IMPORTANT]  
>  您可用來建立以原則為基礎之管理條件的函數不一定會使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法。 請確定您有遵循範例語法。 例如，當您使用`DateAdd`或是`DatePart`函式中，您必須將*datepart*單引號括住的引數。  
  
|函數|描述|引數|傳回值|範例|  
|--------------|-----------------|---------------|------------------|-------------|  
|`Add()`|Numeric Add (Numeric *expression1*, Numeric *expression2*)<br /><br /> 兩個數字相加。|*expression1*並*expression2* -是任何有效的運算式，其中任 numeric 類別目錄中的資料類型除外`bit`資料型別。 可以是常數、屬性或傳回數值類型的函數。|**傳回值：** 傳回具有較高優先順序之引數的資料類型。|**範例** `Add(Property1, 5)`|  
|`Array()`|Array Array (VarArgs *expression*)<br /><br /> 從值清單建立陣列。 可以搭配彙總函式 (如 Sum() 和 Count()) 使用。|*expression* - 這是將要轉換成陣列的運算式。|陣列。|`Array(2,3,4,5,6)`|  
|`Avg()`|Numeric Avg (*VarArgs*)<br /><br /> 傳回引數清單中所有值的平均值。|*VarArgs* -是精確數值或近似數值資料類型類別目錄的 Variant 運算式清單，除了`bit`資料型別。|傳回類型取決於運算式評估結果的類型。<br /><br /> 如果運算式結果是`integer`， `decimal`，`money`並`smallmoney`，`float`和`real`類別目錄，傳回的型別是`int`， `decimal`， `money`，和`float`;分別。|`Avg(1.0, 2.0, 3.0, 4.0, 5.0)` 會傳回 `3.0` 。|  
|`BitwiseAnd()`|Numeric BitwiseAnd (Numeric *expression 1*, Numeric *expression2*)<br /><br /> 在兩個整數值之間，執行位元邏輯 AND 運算。|*expression1* 和 *expression2* - integer 資料類型類別目錄中任何一種資料類型的任何有效運算式。|傳回整數資料類型類別目錄的值。|`BitwiseAnd(Property1, Property2)`|  
|`BitwiseOr()`|Numeric BitwiseOr (Numeric *expression1*, Numeric *expression2*)<br /><br /> 執行兩個指定整數值之間的位元邏輯 OR 運算。|*expression1* 和 *expression2* - integer 資料類型類別目錄中任何一種資料類型的任何有效運算式。|傳回整數資料類型類別目錄的值。|`BitwiseOr(Property1, Property2)`|  
|`Concatenate()`|String Concatenate (String *string1*, String *string2*)<br /><br /> 串連兩個字串。|*string1* 和 *string2* - 這是您想要串連的兩個字串。 可以是任何有效的非 null 字串。|串連的字串， *string1* 後面接著 *string2*。|`Concatenate("Hello", " World` `")` 會傳回 "`Hello World`"。|  
|`Count()`|Numeric Count (*VarArgs*)<br /><br /> 傳回引數清單中的項目數。|*VarArgs* -這是以外的任何類型的運算式`text`， `image`，和`ntext`。|傳回整數資料類型類別目錄的值。|`Count(1.0, 2.0, 3.0, 4.0, 5.0)` 會傳回 `5` 。|  
|`DateAdd()`|DateTime DateAdd (String *datepart*, Numeric *number*, DateTime *date*)<br /><br /> 傳回新`datetime`根據將間隔加入指定日期的值。|*datepart* - 這是指定日期中哪一個部分要傳回新值的參數。 部分支援的類型如下：year(yy, yyyy)、month(mm, m) 和 dayofyear(dy, y)。 如需詳細資訊，請參閱 [DATEADD &#40;Transact-SQL&#41;](/sql/t-sql/functions/dateadd-transact-sql)。<br /><br /> *number* - 這是用來遞增 *datepart* 的值。<br /><br /> *日期*-是傳回的運算式`datetime`值或日期格式之字元字串。|新`datetime`根據將間隔加入指定日期的值。|`DateAdd('day', 21, DateTime('2007-08-06 14:21:50'))` 會傳回 `'2007-08-27 14:21:50'` 。<br /><br /> 下列清單*dateparts*和此函數所支援的縮寫組：<br /><br /> **year**：yy、yyyy<br /><br /> **month**：mm、m<br /><br /> **dayofyear**：dy、y<br /><br /> **day**：dd、d<br /><br /> **week**：wk、ww<br /><br /> **weekday**：dw、w<br /><br /> **hour**：hh<br /><br /> **minute**：mi、n<br /><br /> **second**：ss、s<br /><br /> **millisecond**：ms|  
|`DatePart()`|Numeric DatePart (String *datepart*, DateTime *date*)<br /><br /> 傳回代表指定日期之指定 *datepart* 的整數。|*datepart* - 這是指定要傳回之日期部分的參數。 支援的某些類型如下：year(yy, yyyy)、month(mm, m) 和 dayofyear(dy, y)。 如需詳細資訊，請參閱 [DATEPART &#40;Transact-SQL&#41;](/sql/t-sql/functions/datepart-transact-sql)。<br /><br /> *日期*-是傳回的運算式`datetime`值或日期格式之字元字串。|傳回代表指定日期之指定 *datepart* 的整數資料類型類別目錄的值。|`DatePart('month', DateTime('2007-08-06 14:21:50.620'))` 會傳回 `8` 。|  
|`DateTime()`|DateTime DateTime (String *dateString*)<br /><br /> 從字串建立日期時間值。|*dateString* - 這是字串形式的日期時間值。|傳回從輸入字串建立的日期時間值。|`DateTime('3/12/2006')`|  
|`Divide()`|Numeric Divide (Numeric *expression_dividend*, Numeric *expression_divisor*)<br /><br /> 兩個數字相除。|*expression_dividend* - 這是要除的數值運算式。 被除數可以是數值資料類型類別目錄中任何一個資料類型的任何有效運算式，但是 `datetime` 資料類型除外。<br /><br /> *expression_divisor* - 這是要除以被除數的數值運算式。 除數可以是數值資料類型類別目錄中任何一個資料類型的任何有效運算式，但是 `datetime` 資料類型除外。|傳回具有較高優先順序之引數的資料類型。|`Divide(Property1, 2)`<br /><br /> 注意：這將是雙精確度浮點數運算。 若要執行整數比較，您必須將結果與 `Round()`結合在一起。 例如： `Round(Divide(10, 3), 0) = 3`＞。|  
|`Enum()`|Numeric Enum (String *enumTypeName*, String *enumValueName*)<br /><br /> 從字串建立列舉值。|*enumTypeName* - 這是列舉類型的名稱。<br /><br /> *enumValueName* - 這是列舉的值。|以數值形式傳回列舉值。|`Enum('CompatibilityLevel','Version100')`|  
|`Escape()`|String Escape (String *replaceString*, String *stringToEscape*, String *escapeString*)<br /><br /> 使用指定的逸出字串來逸出輸入字串的子字串。|*replaceString* -- 為輸入字串。<br /><br /> *stringToEscape* -- 為 *replaceString*的子字串。 這是您想要將逸出字串加到其前面的字串。<br /><br /> *escapeString* -- 這是您想要加到每一個 *stringToEscape*執行個體前面的逸出字串。|傳回修改的 *replaceString* ，其中的每一個 *stringToEscape* 執行個體都是在 *escapeString*後面。|`Escape("Hello", "l", "[")` 會傳回 "`He[l[lo`"。|  
|`ExecuteSQL()`|Variant ExecuteSQL (String *returnType*, String *sqlQuery*)<br /><br /> 針對目標伺服器執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢。<br /><br /> 如需 ExecuteSql() 的詳細資訊，請參閱 [ExecuteSql() 函數](http://blogs.msdn.com/b/sqlpbm/archive/2008/07/03/executesql.aspx)。|*returnType* - 指定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式所傳回的傳回資料類型。 有效的常值，如*returnType*如下所示： `Numeric`， `String`， `Bool`， `DateTime`， `Array`，以及`Guid`。<br /><br /> *sqlQuery* - 這是包含要執行之查詢的字串。||`ExecuteSQL ('Numeric', 'SELECT COUNT(*) FROM msdb.dbo.sysjobs') <> 0`<br /><br /> 對目標 SQL Server 執行個體執行純量值的 Transact-SQL 查詢。 `SELECT` 陳述式中，只能指定一個資料行，會忽略第一個以外的其他資料行。 產生的查詢應該只傳回一個資料列，會忽略第一個以外的其他資料列。 如果查詢傳回空集合，依據 `ExecuteSQL` 建立的條件運算式會評估為 false。 `ExecuteSql` 支援 **視需要** 和 **按排程時間** 評估模式。<br /><br /> `@@ObjectName` -對應到中的 [名稱] 欄位[sys.objects](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql)。 將會以目前物件的名稱來取代此變數。<br /><br /> `@@SchemaName` -對應到中的 [名稱] 欄位[sys.schemas](/sql/relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas)。 將會以目前物件的結構描述名稱來取代此變數 (如果適用的話)。<br /><br /> <br /><br /> 注意：若要在 ExecuteSQL 陳述式中加入單引號，請以第二個單引號來逸出該單引號。 例如，若要包含名為 O'Brian 之使用者的參考，請輸入 O''Brian。|  
|`ExecuteWQL()`|Variant ExecuteWQL (string *returnType* , string *namespace*, string *wql*)<br /><br /> 針對提供的命名空間執行 WQL 指令碼。 Select 陳述式只能包含單一傳回資料行。 如果提供了一個以上的資料行，將會擲回錯誤。|*returnType* - 指定 WQL 所指定的傳回資料類型。 有效的常值是`Numeric`， `String`， `Bool`， `DateTime`， `Array`，和`Guid`。<br /><br /> *namespace* - 這是執行所要針對的 WMI 命名空間。<br /><br /> *wql* - 這是包含所要執行之 WQL 的字串。||`ExecuteWQL('Numeric', 'root\CIMV2', 'select NumberOfProcessors from win32_ComputerSystem') <> 0`|  
|`False()`|Bool False()<br /><br /> 傳回布林值 FALSE。||傳回布林值 FALSE。|`IsDatabaseMailEnabled = False()`|  
|`GetDate()`|DateTime GetDate()<br /><br /> 傳回系統日期。||以日期時間形式傳回系統日期。|`@DateLastModified = GetDate()`|  
|`Guid()`|Guid Guid(String *guidString*)<br /><br /> 從字串中傳回 GUID。|*guidString* - 這是要建立之 GUID 的字串表示法。|傳回從字串建立的 GUID。|`Guid('12340000-0000-3455-0000-000000000454')`|  
|`IsNull()`|Variant IsNull (Variant *check_expression*, Variant *replacement_value*)<br /><br /> 如果它不是 NULL，就會傳回 *check_expression* 的值，否則會傳回 *replacement_value* 。 如果類型不同， *replacement_value* 會隱含地轉換成 *check_expression*的類型。|*check_expression* - 這是要檢查 NULL 的運算式。 *check_expression* 可以是任何以原則為基礎之管理支援的類型：Numeric、String、Bool、DateTime、Array 和 Guid。<br /><br /> *replacement_value* - 這是 *check_expression* 為 NULL 時所傳回的運算式。 *replacement_value* 必須是能夠隱含地轉換成 *check_expression*類型的類型。|如果 *check_expression* 不是 NULL，則傳回類型是 *check_expression* 的類型，否則會傳回 *replacement_value* 的類型。||  
|`Len()`|Numeric Len (*string_expression*)<br /><br /> 傳回指定字串運算式的字元數，但不包括尾端空白。|*string_expression* - 這是要評估的字串運算式。|傳回整數資料類型類別目錄的值。|`Len('Hello')` 會傳回 `5` 。|  
|`Lower()`|String Lower (String *_expression*)<br /><br /> 傳回將所有大寫字元轉換成小寫後的字串。|*expression* - 這是來源字串運算式。|傳回將所有大寫字元轉換成小寫後，表示來源字串運算式的字串。|`Len('HeLlO')` 會傳回 `'hello'` 。|  
|`Mod()`|Numeric Mod (Numeric *expression_dividend*, Numeric *expression_divisor*)<br /><br /> 提供第一個數值運算式除以第二個數值運算式之後的整數餘數。|*expression_dividend* - 這是要除的數值運算式。 *expression_dividend* 必須是整數或數值資料類型類別目錄中，任何一個資料類型的有效運算式。<br /><br /> *expression_divisor* - 這是要除以被除數的數值運算式。 *expression_divisor* 必須是整數或數值資料類型類別目錄中，任何一個資料類型的有效運算式。|傳回整數資料類型類別目錄的值。|`Mod(Property1, 3)`|  
|`Multiply()`|Numeric Multiply (Numeric *expression1*, Numeric *expression2*)<br /><br /> 將兩個運算式相乘。|*expression1*並*expression2* -是任何有效的運算式，其中任 numeric 類別目錄中的資料類型除外`datetime`資料型別。|傳回具有較高優先順序之引數的資料類型。|`Multiply(Property1, .20)`|  
|`Power()`|Numeric Power (Numeric *numeric_expression*, Numeric *expression_power*)<br /><br /> 傳回指定乘冪之指定運算式的值。|*numeric_expression* - 這是精確數值或近似數值資料類型類別目錄的運算式，但是 bit 資料類型除外。<br /><br /> *expression_power* - 這是 *numeric_expression*相乘的乘冪。 *expression_power*可以是精確數值或近似數值資料類型類別目錄的運算式，除了`bit`資料型別。|傳回類型與 *numeric_expression*相同。|`Power(Property1, 3)`|  
|`Round()`|Numeric Round (Numeric *expression*, Numeric *expression_precision*)<br /><br /> 傳回已經進位到指定長度或有效位數的數值運算式。|*運算式*-是精確數值的運算式或近似數值資料類型類別目錄，除了`bit`資料型別。<br /><br /> *expression_precision* - 這是進位到的有效位數。 當 *expression_precision* 是正數時， *numeric_expression* 會捨入到長度所指定的十進位數。 當 *expression_precision* 是負數時， *numeric_expression* 會依照 *expression_precision*所指定的方式，在小數點左側捨入。|傳回與 *numeric_expression*相同的類型。|`Round(5.333, 0)`|  
|`String()`|String String (Variant *_expression*)<br /><br /> 將 variant 轉換成字串。|*expression* - 這是要轉換成字串的 variant 運算式。|傳回 variant 運算式的字串值。|`String(4)`|  
|`Sum()`|Numeric Sum (*VarArgs*)<br /><br /> 傳回引數清單中所有值的總和。 總和可以搭配數值使用。|*VarArgs*-是精確數值或近似數值資料類型類別目錄的 Variant 運算式清單，除了`bit`資料型別。|以最精確的運算式資料類型傳回所有運算式值的總和。<br /><br /> 如果運算式結果是`integer`， `numeric`，`money`並`small money`，`float`和`real`類別目錄，傳回的型別是`int`， `numeric`， `money`，和`float`;分別。|`Sum(1.0, 2.0, 3.0, 4.0, 5.0)` 會傳回 `15` 。|  
|`True()`|Bool TRUE()<br /><br /> 傳回布林值 TRUE。||傳回布林值 TRUE。|`IsDatabaseMailEnabled = True()`|  
|`Upper()`|String Upper (String *_expression*)<br /><br /> 傳回將所有小寫字元轉換成大寫後的字串。|*expression* - 這是來源字串運算式。|傳回將所有小寫字元轉換成大寫後，表示來源字串運算式的字串。|`Len('HeLlO')` 會傳回 `'HELLO'` 。|  
  
## <a name="see-also"></a>另請參閱  
 [建立新條件或開啟條件對話方塊，一般頁面](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [使用原則式管理來管理伺服器](administer-servers-by-using-policy-based-management.md)  
  
  
