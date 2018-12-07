---
title: 資料分析工作的設定 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], configuring
ms.assetid: fe050ca4-fe45-43d7-afa9-99478041f9a8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a03718844ee86f275664e83776ef9e75cff95bd4
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535027"
---
# <a name="setup-of-the-data-profiling-task"></a>資料分析工作的設定
  在您可以檢閱來源資料的設定檔前，第一個步驟是設定並執行「資料分析」工作。 您可以在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝內部建立這個工作。 若要設定「資料分析」工作，您可以使用「資料分析工作編輯器」。 此編輯器可讓您選取要輸出設定檔的位置以及要計算的設定檔。 設定工作後，您可以執行封裝以計算資料設定檔。  
  
## <a name="requirements-and-limitations"></a>需求與限制  
 資料分析工作僅用於儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的資料。 此工作不適用於協力廠商或以檔案為基礎的資料來源。  
  
 此外，若要執行包含資料分析工作的封裝，您所使用的帳戶必須具備 tempdb 資料庫的讀取/寫入權限，包括 CREATE TABLE 權限。  
  
## <a name="data-profiling-task-in-a-package"></a>封裝中的資料分析工作  
 「資料分析」工作僅會設定設定檔並建立包含計算設定檔的輸出檔。 若要檢閱這個輸出檔，您必須使用獨立的檢視器程式「資料設定檔檢視器」。 由於您必須個別檢視輸出，因此可能要在不包含其他任何工作的封裝中使用「資料分析」工作。  
  
 不過，您不需要將「資料分析」工作當做封裝中的唯一工作使用。 如果您想要在更複雜封裝的工作流程或資料流程中執行資料分析，就會有下列選項：  
  
-   若要實作以工作輸出檔為基礎的條件式邏輯，請在封裝的控制流程中，將「指令碼」工作放在「資料分析」工作後面。 然後，您就可以使用這個「指令碼」工作來查詢輸出檔。  
  
-   若要在已經載入並轉換資料流程中的資料之後分析這項資料，您必須暫時將變更的資料儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 然後，您就可以分析已儲存的資料。  
  
 如需詳細資訊，請參閱 [在封裝工作流程中納入資料分析工作](../../integration-services/control-flow/incorporate-a-data-profiling-task-in-package-workflow.md)。  
  
## <a name="setup-of-the-task-output"></a>設定工作輸出  
 在「資料分析」工作位於封裝之後，您必須針對此工作將計算的設定檔設定輸出。 若要設定設定檔的輸出，您可以使用 [資料分析工作編輯器] 的 [一般] 頁面。 除了指定輸出的目的地之外，[一般] 頁面還提供執行快速分析資料的功能。 當您選取 [快速分析] 時，「資料分析」工作會使用某些或所有預設的設定檔及其預設值，分析資料表或檢視表。  
  
 如需詳細資訊，請參閱[資料分析工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md) 和[單一資料表快速分析表單 &#40;資料分析工作&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)。  
  
> [!IMPORTANT]  
>  輸出檔可能包含您資料庫的相關敏感性資料，以及資料庫所包含的資料。 如需如何讓這個檔案更安全的相關建議，請參閱 [對封裝使用之檔案的存取權](../../integration-services/security/security-overview-integration-services.md#files)。  
  
## <a name="selection-and-configuration-of-the-profiles-to-be-computed"></a>選取與設定要計算的設定檔  
 設定輸出檔後，您必須選取要計算的資料設定檔。 資料分析工作可以計算八種不同的資料設定檔。 其中五種設定檔會分析個別的資料行，而剩餘的三種則會分析多個資料行或資料行和資料表之間的關聯性。 在單一「資料分析」工作中，您可以針對多個資料表或檢視表中的多個資料行或資料行組合計算多個設定檔。  
  
 下表描述這些每個設定檔所計算的報告，以及有效設定檔的資料類型。  
  
|計算|這有助於識別|使用這個設定檔|  
|----------------|-------------------------|----------------------|  
|選取之資料行中所有不同的字串值長度，以及該資料表中每個長度所代表之資料列的百分比。|**無效的字串值** - 例如，您分析了應該使用兩個字元之美國州名代碼的資料行，但發現長度大於兩個字元的值。|**資料行長度散發** - 適用於具有下列其中一種字元資料類型的資料行：<br /><br /> **char**<br /><br /> **nchar**<br /><br /> **varchar**<br /><br /> **nvarchar**|  
|一組規則運算式，其中涵蓋了字串資料行中值的指定百分比。<br /><br /> 同時可尋找未來可用於驗證新值的規則運算式|**無效或格式錯誤的字串值** - 例如，[郵遞區號] 資料行的模式設定檔可能會產生規則運算式：\d{5}-\d{4}、\d{5} 和 \d{9}。 如果輸出包含其他規則運算式，表示資料包含無效或格式錯誤的值。|**資料行模式設定檔** - 適用於具有下列其中一種字元資料類型的資料行：<br /><br /> **char**<br /><br /> **nchar**<br /><br /> **varchar**<br /><br /> **nvarchar**|  
|選取之資料行中 Null 值的百分比。|**某個資料行中 Null 值的比例過高** - 例如，您分析了應該包含美國郵遞區號的資料行，但發現遺漏郵遞區號的比例過高。|**資料行 Null 比例** - 適用於具有下列其中一種資料類型的資料行：<br /><br /> **image**<br /><br /> **text**<br /><br /> **xml**<br /><br /> 使用者定義型別<br /><br /> variant 類型|  
|數值資料行的最小值、最大值、平均值和標準差，以及 **datetime** 資料行的最小值和最大值等統計資料。|**無效的數值和日期** - 例如，您分析了過去日期的資料行，但發現屬於未來的最大日期。|**資料行統計資料設定檔** - 適用於具有下列其中一種資料類型的資料行。<br /><br /> 數值資料類型：<br /><br /> 整數類型 ( **bit**除外<br /><br /> **money**<br /><br /> **smallmoney**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **real**<br /><br /> **numeric**<br /><br /> 日期和時間資料類型：<br /><br /> **datetime**<br /><br /> **smalldatetime**<br /><br /> **timestamp**<br /><br /> **date**<br /><br /> **time**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**<br /><br /> 注意：若為具有日期和時間資料類型的資料行，此設定檔就只會計算最小值和最大值。|  
|選取之資料行中的所有相異值，以及該資料表中每個值所代表之資料列的百分比。 或者，代表超過資料表中指定之資料列百分比的值。|**某個資料行中相異值的數目不正確** - 例如，您分析了包含美國州名的資料行，但發現超過 50 個相異值。|**資料行值散發** - 適用於具有下列其中一種資料類型的資料行。<br /><br /> 數值資料類型：<br /><br /> 整數類型 ( **bit**除外<br /><br /> **money**<br /><br /> **smallmoney**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **real**<br /><br /> **numeric**<br /><br /> 字元資料類型：<br /><br /> **char**<br /><br /> **nchar**<br /><br /> **varchar**<br /><br /> **nvarchar**<br /><br /> 日期和時間資料類型：<br /><br /> **datetime**<br /><br /> **smalldatetime**<br /><br /> **timestamp**<br /><br /> **date**<br /><br /> **time**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**|  
|資料行或資料行集合為選取之資料表的索引鍵或近似索引鍵。|**潛在索引鍵資料行中重複的值** - 例如，您在 Customers 資料表中分析了 Name 和 Address 資料行，但發現名稱和地址組合應該是唯一的重複值。|**候選索引鍵** - 多個資料行設定檔，其中會報告資料行或資料行集合是否適合當做選取之資料表的索引鍵。 適用於具有下列其中一種資料類型的資料行。<br /><br /> 整數資料類型：<br /><br /> **bit**<br /><br /> **tinyint**<br /><br /> **smallint**<br /><br /> **int**<br /><br /> **bigint**<br /><br /> 字元資料類型：<br /><br /> **char**<br /><br /> **nchar**<br /><br /> **varchar**<br /><br /> **nvarchar**<br /><br /> 日期和時間資料類型：<br /><br /> **datetime**<br /><br /> **smalldatetime**<br /><br /> **timestamp**<br /><br /> **date**<br /><br /> **time**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**|  
|某個資料行 (相依資料行) 中的值相依於另一個資料行或資料行集合 (行列式資料行) 中之值的程度。|**不適用於相依資料行中的值** - 例如，您分析了包含「美國郵遞區號」之資料行與「美國州名」之資料行之間的相依性。 相同的郵遞區號應該永遠具有相同的州名。 不過，此設定檔發現了這個相依性的違規。|**功能相依性** - 適用於具有下列其中一種資料類型的資料行。<br /><br /> 整數資料類型：<br /><br /> **bit**<br /><br /> **tinyint**<br /><br /> **smallint**<br /><br /> **int**<br /><br /> **bigint**<br /><br /> 字元資料類型：<br /><br /> **char**<br /><br /> **nchar**<br /><br /> **varchar**<br /><br /> **nvarchar**<br /><br /> 日期和時間資料類型：<br /><br /> **datetime**<br /><br /> **smalldatetime**<br /><br /> **timestamp**<br /><br /> **date**<br /><br /> **time**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**|  
|資料行或資料行集合是否適合當做選取之資料表之間的外部索引鍵。<br /><br /> 也就是說，這個設定檔會報告兩個資料行或資料行集合之間值的重疊。|**無效的值** - 例如，您分析了 Sales 資料表的 ProductID 資料行。 此設定檔發現該資料行包含在 Products 資料表之 ProductID 資料行中找不到的值。|**值包含** - 適用於具有下列其中一種資料類型的資料行：<br /><br /> 整數資料類型：<br /><br /> **bit**<br /><br /> **tinyint**<br /><br /> **smallint**<br /><br /> **int**<br /><br /> **bigint**<br /><br /> 字元資料類型：<br /><br /> **char**<br /><br /> **nchar**<br /><br /> **varchar**<br /><br /> **nvarchar**<br /><br /> 日期和時間資料類型：<br /><br /> **datetime**<br /><br /> **smalldatetime**<br /><br /> **timestamp**<br /><br /> **date**<br /><br /> **time**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**|  
  
 若要選取要計算的設定檔，您可以使用 [資料分析工作編輯器] 的 [設定檔要求] 頁面。 如需詳細資訊，請參閱[資料分析工作編輯器 &#40;設定檔要求頁面&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)。  
  
 在 [設定檔要求] 頁面上，您也可以指定資料來源並設定資料設定檔。 當您設定工作時，請考慮下列資訊：  
  
-   若要簡化組態，並且更容易發現不熟悉之資料的特性，您可以使用萬用字元 **(\*)** 來取代個別的資料行名稱。 如果您使用這個萬用字元，此工作將會分析具有適當資料類型的每個資料行，而且可能會降低處理速度。  
  
-   當選取的資料表或檢視為空白時，資料分析工作不會計算任何設定檔。  
  
-   當選取之資料行中的所有值為 Null 時，資料分析工作僅會計算資料行 Null 比例設定檔。 此工作不會計算空白資料行的資料行長度散發設定檔、資料行模式設定檔、資料行統計資料設定檔或資料行值散發設定檔。  
  
 每個可用的資料設定檔都有自己的組態選項。 如需有關這些選項的詳細資訊，請參閱下列主題：  
  
-   [候選索引鍵設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [資料行長度散發設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [資料行 Null 比例設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [資料行模式設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [資料行統計資料設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [資料行值散發設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [功能相依性設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [值包含設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/value-inclusion-profile-request-options-data-profiling-task.md)  
  
## <a name="execution-of-the-package-that-contains-the-data-profiling-task"></a>執行包含資料分析工作的封裝  
 設定「資料分析」工作後，您可以執行該工作。 然後，此工作會計算資料設定檔，並將此資訊以 XML 格式輸出到檔案或封裝變數。 這個 XML 的結構會遵循 DataProfile.xsd 結構描述。 您可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 或其他結構描述編輯器、XML 編輯器，或是在 [記事本] 之類的文字編輯器中開啟結構描述。 此資料品質資訊的結構描述對於下列用途可能很實用：  
  
-   在組織內部與跨組織交換資料品質資訊。  
  
-   建立搭配資料品質資訊使用的自訂工具。  
  
 在結構描述中，將目標命名空間識別為 [https://schemas.microsoft.com/sqlserver/2008/DataDebugger/](https://schemas.microsoft.com/sqlserver/2008/DataDebugger/)。  
  
## <a name="next-step"></a>下一個步驟  
 [資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
  
