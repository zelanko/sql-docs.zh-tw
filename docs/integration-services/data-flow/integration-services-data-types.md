---
title: Integration Services 資料類型 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- modifying data types
- data types [Integration Services], listed
- data types [Integration Services]
- column data types [Integration Services]
- SSIS, data types
- Integration Services, data types
- SQL Server Integration Services, data types
ms.assetid: 896fc3e8-3aa6-4396-ba82-5d7741cffa56
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8fc0c1658ce051aa3e0fa494ef5c1b40d2db8881
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832518"
---
# <a name="integration-services-data-types"></a>Integration Services 資料類型
  當資料輸入封裝中的資料流程時，擷取資料的來源會將資料轉換為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型。 數值資料會指派為數值資料類型、字串資料指派為字元資料類型，而日期則是指派為日期資料類型。 其他資料，例如 GUID 和「二進位大型物件區塊 (BLOB)」也都會被指派適當的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型。 如果資料的資料類型不能轉換為 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型，則會發生錯誤。  
  
 部分資料流程元件會在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]的 Managed 資料類型之間轉換資料類型。 如需 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 Managed 資料類型間對應的詳細資訊，請參閱 [使用資料流程中的資料類型](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)。  
  
 下表列出 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型。 資料表中的某些資料類型具有適用的精確度和小數位數資訊。 如需有效位數和小數位數的詳細資訊，請參閱[有效位數、小數位數和長度 &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
|資料類型|Description|  
|---------------|-----------------|  
|DT_BOOL|布林值。|  
|DT_BYTES|二進位資料值。 長度是變數，且最大長度為 8,000 個位元組。|  
|DT_CY|貨幣值。 此資料類型是 8 位元且小數位數為 4 的帶正負號的整數，最大有效位數為 19。|  
|DT_DATE|包含年、月、日、小時、分鐘、秒和小數秒的日期結構。  小數秒的固定有效位數為 7 位數字。<br /><br /> DT_DATE 資料類型需使用 8 位元組的浮點數加以實作。 日期是以累進整數來表示，從 1899 年 12 月 30 日開始，並以午夜做為零時。 小時值則以小數點後數字部分的絕對值來表示。 不過，浮點值不能代表所有實數值；因此，DT_DATE 可以呈現的日期範圍便有所限制。<br /><br /> 另一方面，DT_DBTIMESTAMP 是以內部包含年、月、日、時、分、秒及毫秒等個別欄位的結構來表示， 而且這種資料類型所能呈現的日期範圍具有較寬的限制。|  
|DT_DBDATE|包含年、月和日的日期結構。|  
|DT_DBTIME|包含小時、分鐘和秒的時間結構。|  
|DT_DBTIME2|包含小時、分鐘、秒和小數秒的時間結構。 小數秒的最大小數位數為 7 位數。|  
|DT_DBTIMESTAMP|包含年、月、日、小時、分鐘、秒和小數秒的時間戳記結構。 小數秒的最大小數位數為 3 位數。|  
|DT_DBTIMESTAMP2|包含年、月、日、小時、分鐘、秒和小數秒的時間戳記結構。 小數秒的最大小數位數為 7 位數。|  
|DT_DBTIMESTAMPOFFSET|包含年、月、日、小時、分鐘、秒和小數秒的時間戳記結構。 小數秒的最大小數位數為 7 位數。<br /><br /> 與 DT_DBTIMESTAMP 和 DT_DBTIMESTAMP2 資料類型不同，DT_DBTIMESTAMPOFFSET 資料類型具有時區時差。 此時差指定時間從「國際標準時間」(Coordinated Universal Time，UTC) 位移的小時和分鐘數。 系統會使用時區時差來取得本地時間。<br /><br /> 時區時差必須包含正負號，以指出是對 UTC 加入或減去時差。 有效的小時時差數是在 -14 和 +14 之間。 分鐘時差的正負號則是依照小時時差的正負號而定。<br /><br /> 如果小時時差的正負號為負，則分鐘時差也必須為負或零。<br /><br /> 如果小時時差的正負號為正，則分鐘時差也必須為正或零。<br /><br /> 如果小時時差的正負號為零，則分鐘時差可以是負 0.59 到正 0.59 的任何值。|  
|DT_DECIMAL|具有固定有效位數和固定小數位數的精確數值。 此資料類型是具有單獨的符號，小數位數為 0 至 28，最大有效位數為 29 的 12 位元組不帶正負號的整數。|  
|DT_FILETIME|64 位元值，表示自 1601 年 1 月 1 日起 100 奈秒間隔的數目。 小數秒的最大小數位數為 3 位數。|  
|DT_GUID|全域唯一識別碼 (GUID)。|  
|DT_I1|一位元組帶正負號的整數。|  
|DT_I2|兩位元組帶正負號的整數。|  
|DT_I4|四位元組帶正負號的整數。|  
|DT_I8|八位元組帶正負號的整數。|  
|DT_NUMERIC|具有固定有效位數和小數位數的精確數值。 此資料類型是具有單獨的符號，小數位數為 0 至 38，最大有效位數為 38 的 16 位元組不帶正負號的整數。|  
|DT_R4|單精確度浮點值。|  
|DT_R8|雙精確度浮點值。|  
|DT_STR|最大長度為 8000 字元，以 NULL 終止的 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS 字元字串。 如果資料行值包含額外的 Null 結束字元，字串就會在第一個 Null 出現時被截斷。|  
|DT_UI1|一位元組不帶正負號的整數。|  
|DT_UI2|兩位元組不帶正負號的整數。|  
|DT_UI4|四位元組不帶正負號的整數。|  
|DT_UI8|八位元組不帶正負號的整數。|  
|DT_WSTR|最大長度為 4000 字元，以 Null 終止的 Unicode 字元字串。 如果資料行值包含額外的 Null 結束字元，字串就會在第一個 Null 出現時被截斷。|  
|DT_IMAGE|大小上限為 2^31-1 (2,147,483,647) 個位元組的二進位值。 的 Managed 資料類型之間轉換資料類型。|  
|DT_NTEXT|最大長度為 2^30 - 1 (1,073,741,823) 個字元的 Unicode 字元字串。|  
|DT_TEXT|最大長度為 2^31-1 (2,147,483,647) 個字元的 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS 字元字串。|  
  
## <a name="conversion-of-data-types"></a>資料類型的轉換  
 如果資料行中的資料不需要來源資料類型配置的全形字元，您可能需要變更該資料行的資料類型。 在傳送資料時，每個資料列愈窄愈有助於最佳化效能，因為每個資料列愈窄，資料從來源移動到目的地的速度就會愈快。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含完整的一組數值資料類型，以便您可以使資料類型與資料大小密切相符。 例如，如果資料類型為 DT_UI8 之資料列中的值始終是 0 至 3000 之間的整數，則您可以將資料類型變更為 DT_UI2。 同樣地，如果資料類型為 DT_CY 的資料行可以透過改用整數資料類型來滿足封裝資料需求，則您可以將資料類型變更為 DT_I4。  
  
 您可以透過下列方式變更資料行的資料類型：  
  
-   使用的運算式以隱含地轉換資料類型。 如需詳細資訊，請參閱[運算式中的 Integration Services 資料類型](../../integration-services/expressions/integration-services-data-types-in-expressions.md)、[運算式中的 Integration Services 資料類型](../../integration-services/expressions/integration-services-data-types-in-expressions.md)和 [Integration Services &#40;SSIS&#41; 運算式](../../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
-   使用轉換運算子來轉換資料類型。 如需詳細資訊，請參閱 [Cast &#40;SSIS 運算式&#41;](../../integration-services/expressions/cast-ssis-expression.md)。  
  
-   使用「資料轉換」轉換，將資料行的資料類型從一個資料類型轉換為不同的資料類型。 如需詳細資訊，請參閱 [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md)。  
  
-   使用衍生的資料行轉換，建立資料類型與原始資料行不同的資料行副本。 如需詳細資訊，請參閱 [衍生的資料行轉換](../../integration-services/data-flow/transformations/derived-column-transformation.md)。  
  
### <a name="converting-between-strings-and-datetime-data-types"></a>在字串與日期/時間資料類型之間轉換  
 下表列出在日期/時間資料類型與字串之間轉型或轉換的結果：  
  
-   當您使用轉換運算子或資料轉換時，日期或時間資料類型將會轉換成對應的字串格式。 例如，DT_DBTIME 資料類型將會轉換成格式為 "hh:mm:ss" 的字串。  
  
-   當您想要從字串轉換成日期或時間資料類型時，此字串必須使用會對應到適當日期或時間資料類型的字串格式。 例如，若要成功地將某些日期字串轉換成 DT_DBDATE 資料類型，這些日期字串必須使用 "yyyy-mm-dd" 格式。  
  
    |資料類型|字串格式|  
    |---------------|-------------------|  
    |DT_DBDATE|yyyy-mm-dd|  
    |DT_FILETIME|yyyy-mm-dd hh:mm:ss:fff|  
    |DT_DBTIME|hh:mm:ss|  
    |DT_DBTIME2|hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMP|yyyy-mm-dd hh:mm:ss[.fff]|  
    |DT_DBTIMESTAMP2|yyyy-mm-dd hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMPOFFSET|yyyy-mm-dd hh:mm:ss[.fffffff] [{+&#124;-} hh:mm]|  
  
 在 DT_FILETIME 和 DT_DBTIMESTAMP 的格式中，fff 是介於 0 和 999 之間的值，代表小數秒數。  
  
 在 DT_DBTIMESTAMP2、DT_DBTIME2 和 DT_DBTIMESTAMPOFFSET 的日期格式中，fffffff 是介於 0 和 9999999 之間的值，代表小數秒數。  
  
 DT_DBTIMESTAMPOFFSET 的日期格式也包含時區元素。 在時間元素和時區元素之間有一個空格。  
  
### <a name="converting-datetime-data-types"></a>轉換日期/時間資料類型  
 您也可以變更具有日期/時間資料之資料行的資料類型，以擷取該資料的日期或時間部分。 下表列出將日期/時間資料類型變更為其他日期/時間資料類型的結果。  
  
#### <a name="converting-from-dtfiletime"></a>從 DT_FILETIME 轉換  
  
|轉換 DT_FILETIME 到|結果|  
|-----------------------------|------------|  
|DT_FILETIME|無變更。|  
|DT_DATE|轉換資料類型。|  
|DT_DBDATE|移除時間值。|  
|DT_DBTIME|移除日期值。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIME 資料類型可包含的小數位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIME2|移除 DT_FILETIME 資料類型所代表的日期值。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIME2 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP|轉換資料類型。|  
|DT_DBTIMESTAMP2|當小數秒值的小數位數大於 DT_DBTIMESTAMP2 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMPOFFSET|將 DT_DBTIMESTAMPOFFSET 資料類型中的時區欄位設定為零。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIMESTAMPOFFSET 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
  
#### <a name="converting-from-dtdate"></a>從 DT_DATE 轉換  
  
|轉換 DT_DATE 到|結果|  
|-------------------------|------------|  
|DT_FILETIME|轉換資料類型。|  
|DT_DATE|無變更。|  
|DT_DBDATE|移除 DT_DATA 資料類型所代表的時間值。|  
|DT_DBTIME|移除 DT_DATE 資料類型所代表的日期值。|  
|DT_DBTIME2|移除 DT_DATE 資料類型所代表的日期值。|  
|DT_DBTIMESTAMP|轉換資料類型。|  
|DT_DBTIMESTAMP2|轉換資料類型。|  
|DT_DBTIMESTAMPOFFSET|將 DT_DBTIMESTAMPOFFSET 資料類型中的時區欄位設定為零。|  
  
#### <a name="converting-from-dtdbdate"></a>從 DT_DBDATE 轉換  
  
|轉換 DT_DBDATE 到|結果|  
|---------------------------|------------|  
|DT_FILETIME|將 DT_FILETIME 資料類型中的時間欄位設定為零。|  
|DT_DATE|將 DT_DATE 資料類型中的時間欄位設定為零。|  
|DT_DBDATE|無變更。|  
|DT_DBTIME|將 DT_DBTIME 資料類型中的時間欄位設定為零。|  
|DT_DBTIME2|將 DT_DBTIME2 資料類型中的時間欄位設定為零。|  
|DT_DBTIMESTAMP|將 DT_DBTIMESTAMP 資料類型中的時間欄位設定為零。|  
|DT_DBTIMESTAMP2|將 DT_DBTIMESTAMP 資料類型中的時間欄位設定為零。|  
|DT_DBTIMESTAMPOFFSET|將 DT_DBTIMESTAMPOFFSET 資料類型中的時間欄位和時區欄位設定為零。|  
  
#### <a name="converting-from-dtdbtime"></a>從 DT_DBTIME 轉換  
  
|轉換 DT_DBTIME 到|結果|  
|---------------------------|------------|  
|DT_FILETIME|將 DT_FILETIME 資料類型中的日期欄位設定為目前的日期。|  
|DT_DATE|將 DT_DATE 資料類型中的日期欄位設定為目前的日期。|  
|DT_DBDATE|將 DT_DBDATE 資料類型中的日期欄位設定為目前的日期。|  
|DT_DBTIME|無變更。|  
|DT_DBTIME2|轉換資料類型。|  
|DT_DBTIMESTAMP|將 DT_DBTIMESTAMP 資料類型中的日期欄位設定為目前的日期。|  
|DT_DBTIMESTAMP2|將 DT_DBTIMESTAMP2 資料類型中的日期欄位設定為目前的日期。|  
|DT_DBTIMESTAMPOFFSET|將 DT_DBTIMESTAMPOFFSET 資料類型中的日期欄位和時區欄位分別設定為目前的日期和零。|  
  
#### <a name="converting-from-dtdbtime2"></a>從 DT_DBTIME2 轉換  
  
|轉換 DT_DBTIME2 到|結果|  
|----------------------------|------------|  
|DT_FILETIME|將 DT_FILETIME 資料類型中的日期欄位設定為目前的日期。<br /><br /> 當小數秒值的小數位數大於 DT_FILETIME 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DATE|將 DT_DATE 資料類型的日期欄位設定為目前的日期。<br /><br /> 當小數秒值的小數位數大於 DT_DATE 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBDATE|將 DT_DBDATE 資料類型的日期欄位設定為目前的日期。|  
|DT_DBTIME|當小數秒值的小數位數大於 DT_DBTIME 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIME2|當小數秒值的小數位數大於目的地 DT_DBTIME2 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP|將 DT_DBTIMESTAMP 資料類型中的日期欄位設定為目前的日期。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIMESTAMP 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP2|將 DT_DBTIMESTAMP2 資料類型中的日期欄位設定為目前的日期。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIMESTAMP2 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMPOFFSET|將 DT_DBTIMESTAMPOFFSET 資料類型中的日期欄位和時區欄位分別設定為目前的日期和零。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIMESTAMPOFFSET 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
  
#### <a name="converting-from-dtdbtimestamp"></a>從 DT_DBTIMESTAMP 轉換  
  
|轉換 DT_DBTIMESTAMP 到|結果|  
|--------------------------------|------------|  
|DT_FILETIME|轉換資料類型。|  
|DT_DATE|如果 DT_DBTIMESTAMP 資料類型所代表的值造成 DT_DATE 資料類型的範圍溢位，則會傳回 DB_E_DATAOVERFLOW 錯誤。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBDATE|移除 DT_DBTIMESTAMP 資料類型所代表的時間值。|  
|DT_DBTIME|移除 DT_DBTIMESTAMP 資料類型所代表的日期值。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIME 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIME2|移除 DT_DBTIMESTAMP 資料類型所代表的日期值。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIME2 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP|無變更。|  
|DT_DBTIMESTAMP2|當小數秒值的小數位數大於 DT_DBTIMESTAMP2 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMPOFFSET|將 DT_DBTIMESTAMPOFFSET 資料類型中的時區欄位設定為零。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIMESTAMPOFFSET 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
  
#### <a name="converting-from-dtdbtimestamp2"></a>從 DT_DBTIMESTAMP2 轉換  
  
|轉換 DT_DBTIMESTAMP2 到|結果|  
|---------------------------------|------------|  
|DT_FILETIME|當小數秒值的小數位數大於 DT_FILETIME 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DATE|如果 DT_DBTIMESTAMP2 資料類型所代表的值造成 DT_DATE 資料類型的範圍溢位，則會傳回 DB_E_DATAOVERFLOW 錯誤。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。<br /><br /> 當小數秒值的小數位數大於 DT_DATE 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBDATE|移除 DT_DBTIMESTAMP2 資料類型所代表的時間值。|  
|DT_DBTIME|移除 DT_DBTIMESTAMP2 資料類型所代表的日期值。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIME 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIME2|移除 DT_DBTIMESTAMP2 資料類型所代表的日期值。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIME2 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP|如果 DT_DBTIMESTAMP2 資料類型所代表的值造成 DT_DBTIMESTAMP 資料類型的範圍溢位，則會傳回 DB_E_DATAOVERFLOW 錯誤。<br /><br /> DT_DBTIMESTAMP2 會對應到 SQL Server 資料類型 datetime2，範圍是西元元年 1 月 1 日 到 9999 年 12 月 31 日。 DT_DBTIMESTAMP 會對應到 SQL Server 資料類型 datetime，且使用西元 1753 年 1 月 1 日到 9999 年的 12 月 31 日的較小範圍。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIMESTAMP 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。<br /><br /> 如需錯誤的詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP2|當小數秒值的小數位數大於目的地 DT_DBTIMESTAMP2 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMPOFFSET|將 DT_DBTIMESTAMPOFFSET 資料類型中的時區欄位設定為零。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIMESTAMPOFFSET 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
  
#### <a name="converting-from-dtdbtimestampoffset"></a>從 DT_DBTIMESTAMPOFFSET 轉換  
  
|轉換 DT_DBTIMESTAMPOFFSET 到|結果|  
|--------------------------------------|------------|  
|DT_FILETIME|將 DT_DBTIMESTAMPOFFSET 資料類型所代表的時間值變更為「國際標準時間」(Coordinated Universal Time，UTC)。<br /><br /> 當小數秒值的小數位數大於 DT_FILETIME 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DATE|將 DT_DBTIMESTAMPOFFSET 資料類型所代表的時間值變更為 UTC。<br /><br /> 如果 DT_DBTIMESTAMPOFFSET 資料類型所代表的值造成 DT_DATE 資料類型的範圍溢位，則會傳回 DB_E_DATAOVERFLOW 錯誤。<br /><br /> 當小數秒值的小數位數大於 DT_DATE 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。<br /><br /> 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBDATE|將 DT_DBTIMESTAMPOFFSET 資料類型所代表的時間值變更為 UTC，這可能會影響日期值。 時間值則會移除。|  
|DT_DBTIME|將 DT_DBTIMESTAMPOFFSET 資料類型所代表的時間值變更為 UTC。<br /><br /> 移除 DT_DBTIMESTAMPEOFFSET 資料類型所代表的日期值。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIME 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIME2|將 DT_DBTIMESTAMPOFFSET 資料類型所代表的時間值變更為 UTC。<br /><br /> 移除 DT_DBTIMESTAMPOFFSET 資料類型所代表的日期值。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIME2 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP|將 DT_DBTIMESTAMPOFFSET 資料類型所代表的時間值變更為 UTC。<br /><br /> 如果 DT_DBTIMESTAMPOFFSET 資料類型所代表的值造成 DT_DBTIMESTAMP 資料類型的範圍溢位，則會傳回 DB_E_DATAOVERFLOW 錯誤。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIMESTAMP 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。<br /><br /> 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMP2|將 DT_DBTIMESTAMPOFFSET 資料類型所代表的時間值變更為 UTC。<br /><br /> 當小數秒值的小數位數大於 DT_DBTIMESTAMP2 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
|DT_DBTIMESTAMPOFFSET|當小數秒值的小數位數大於目的地 DT_DBTIMESTAMPOFFSET 資料類型可包含的小數秒位數時，將小數秒值移除。 在移除小數秒值之後，產生有關此資料截斷的報表。 如需詳細資訊，請參閱 [處理資料中的錯誤](../../integration-services/data-flow/error-handling-in-data.md)。|  
  
## <a name="mapping-of-integration-services-data-types-to-database-data-types"></a>將 Integration Services 資料類型對應到資料庫資料類型  
 下表提供將某些資料庫所使用的資料類型對應到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型的指南。 這些對應是摘錄自「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈」在匯入這些來源的資料時所使用的對應檔案。 如需這些對應檔的詳細資訊，請參閱 [SQL Server 匯入和匯出精靈](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)。  
  
> [!IMPORTANT]  
>  這些對應不是要用來嚴格限制相等的對應，而只是提供對應時的指南， 在某些情況下，您可能需要使用不同於這個表格所列的資料類型。  
  
> [!NOTE]  
>  您可以使用 SQL Server 資料類型來估計對應 Integration Services date 和 time 資料類型的大小。  
  
|資料類型|[SQL Server]<br /><br /> (SQLOLEDB; SQLNCLI10)|SQL Server (SqlClient)|Jet|Oracle<br /><br /> (OracleClient)|DB2<br /><br /> (DB2OLEDB)|DB2<br /><br /> (IBMDADB2)|  
|---------------|--------------------------------------------|------------------------------|---------|---------------------------------|--------------------------|--------------------------|  
|DT_BOOL|bit|bit|bit||||  
|DT_BYTES|binary, varbinary, timestamp|binary, varbinary, timestamp|BigBinary, VarBinary|RAW|||  
|DT_CY|smallmoney, money|smallmoney, money|CURRENCY||||  
|DT_DATE|||||||  
|DT_DBDATE|[日期 &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)|[日期 &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)||日期|日期|日期|  
|DT_DBTIME||||TIMESTAMP|time|time|  
|DT_DBTIME2|[時間 &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)(p)|[時間 &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md) (p)|||||  
|DT_DBTIMESTAMP|[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)、[smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)|[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)、[smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)|DateTime|TIMESTAMP, DATE, INTERVAL|TIME, TIMESTAMP, DATE|TIME, TIMESTAMP, DATE|  
|DT_DBTIMESTAMP2|[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)|[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)||TIMESTAMP|TIMESTAMP|TIMESTAMP|  
|DT_DBTIMESTAMPOFFSET|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)(p)|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md) (p)||timestampoffset|timestamp,<br /><br /> varchar|timestamp,<br /><br /> varchar|  
|DT_DECIMAL|||||||  
|DT_FILETIME|||||||  
|DT_GUID|UNIQUEIDENTIFIER|UNIQUEIDENTIFIER|GUID||||  
|DT_I1|||||||  
|DT_I2|SMALLINT|SMALLINT|Short||smallint|SMALLINT|  
|DT_I4|ssNoversion|ssNoversion|長整數||INTEGER|INTEGER|  
|DT_I8|BIGINT|BIGINT|||BIGINT|bigint|  
|DT_NUMERIC|decimal, numeric|decimal, numeric|Decimal|NUMBER, INT|decimal, numeric|decimal, numeric|  
|DT_R4|REAL|REAL|Single||real|real|  
|DT_R8|float|FLOAT|Double|FLOAT, REAL|FLOAT, DOUBLE|FLOAT, DOUBLE|  
|DT_STR|char, varchar||varchar||char, varchar|char, varchar|  
|DT_UI1|TINYINT|TINYINT|Byte||||  
|DT_UI2|||||||  
|DT_UI4|||||||  
|DT_UI8|||||||  
|DT_WSTR|nchar, nvarchar, sql_variant, xml|char, varchar, nchar, nvarchar, sql_variant, xml|LongText|CHAR, ROWID, VARCHAR2, NVARCHAR2, NCHAR|GRAPHIC, VARGRAPHIC|GRAPHIC, VARGRAPHIC|  
|DT_IMAGE|image|image|LongBinary|LONG RAW, BLOB, LOBLOCATOR, BFILE, VARGRAPHIC, LONG VARGRAPHIC, user-defined|CHAR () FOR BIT DATA, VARCHAR () FOR BIT DATA|CHAR () FOR BIT DATA, VARCHAR () FOR BIT DATA, BLOB|  
|DT_NTEXT|ntext|text, ntext||LONG, CLOB, NCLOB, NVARCHAR, TEXT|LONG VARCHAR, NCHAR, NVARCHAR, TEXT|LONG VARCHAR, DBCLOB, NCHAR, NVARCHAR, TEXT|  
|DT_TEXT|text||||LONG VARCHAR FOR BIT DATA|LONG VARCHAR FOR BIT DATA, CLOB|  
  
 如需資料流程中對應資料類型的資訊，請參閱 [使用資料流程中的資料類型](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)。  
  
## <a name="related-content"></a>相關內容  
 blogs.msdn.com 上的部落格文章： [SSIS 2008 中各種資料類型轉換技術的效能比較](http://go.microsoft.com/fwlink/?LinkId=220823)。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程中的資料](../../integration-services/data-flow/data-in-data-flows.md)  
  
  
