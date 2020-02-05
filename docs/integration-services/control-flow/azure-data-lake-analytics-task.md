---
title: Azure Data Lake Analytics 工作 | Microsoft Docs
description: 您可以利用 Data Lake Analytics 工作，將 U-SQL 作業提交至 Azure Data Lake Analytics 服務。
ms.custom: ''
ms.date: 06/27/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: yanancai
ms.author: yanacai
ms.openlocfilehash: ab9a357e8215310b21fa2e401067f49176aeefd4
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67947350"
---
# <a name="azure-data-lake-analytics-task"></a>Azure Data Lake Analytics 工作

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



您可以利用 Data Lake Analytics 工作，將 U-SQL 作業提交至 Azure Data Lake Analytics 服務。 此工作是 [Azure SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。

如需了解一般背景，請參閱 [Azure Data Lake Analytics](https://azure.microsoft.com/services/data-lake-analytics/)。

## <a name="configure-the-task"></a>設定工作

若要將 Data Lake Analytics 工作新增至套件，請將該工作從 SSIS 工具箱拖曳至設計工具畫布。 接著，按兩下此工作，或以滑鼠右鍵按一下此工作，然後選取 [編輯]  。 [Azure Data Lake Analytics 工作編輯器]  對話方塊隨即開啟。 您可以透過 SSIS 設計工具或以程式設計方式來設定屬性。

## <a name="general-page-configuration"></a>一般頁面設定

使用 [一般]  頁面來設定工作，並提供工作提交的 U-SQL 指令碼。 若要深入了解 U-SQL 語言，請參閱 [U-SQL 語言參考](/u-sql/) \(英文\)。

### <a name="basic-configuration"></a>基本設定

您可以指定工作的名稱和描述。

### <a name="u-sql-configuration"></a>U-SQL 設定

U-SQL 設定有兩個設定：**SourceType** 和根據 **SourceType** 值而定的動態選項。 

**SourceType：** 指定 U-SQL 指令碼的來源。 指令碼會在 SSIS 套件執行期間，提交至 Data Lake Analytics 帳戶。 此屬性的選項包括：

|值|描述|  
|-----------|-----------------|  
|**DirectInput**|透過內嵌編輯器指定 U-SQL 指令碼。 選取此值會顯示動態選項 **USQLStatement**。|  
|**FileConnection**|指定本機的.usql 檔案，其中包含 U-SQL 指令碼。 選取此選項會顯示動態選項 **FileConnection**。|  
|**變數**|指定 SSIS 變數，其中包含 U-SQL 指令碼。 選取此值會顯示動態選項 [SourceVariable]  。|

**SourceType 動態選項：** 指定 U-SQL 查詢的指令碼內容。 

|SourceType|動態選項|  
|-----------|-----------------|  
|**SourceType = DirectInput**|直接在選項方塊輸入要提交的 U-SQL 查詢，或選取瀏覽按鈕 (...)，在 [輸入 U-SQL 查詢]  對話方塊中輸入 U-SQL 查詢。|  
|**SourceType = FileConnection**|選取現有的檔案連線管理員，或選取 [<新增連線>]  以建立新的檔案連線。 如需相關資訊，請參閱[檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)和[檔案連線管理員編輯器](../../integration-services/connection-manager/file-connection-manager-editor.md)。|  
|**SourceType = Variable**|選取現有的變數，或選取 [\<新增變數...>]  以建立新的變數。 如需相關資訊，請參閱[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[新增變數](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)。|


### <a name="job-configuration"></a>作業設定
作業設定指定 U-SQL 作業提交屬性。

- **AzureDataLakeAnalyticsConnection：** 指定要提交 U-SQL 指令碼的 Data Lake Analytics 帳戶。 從已定義的連接管理員清單中選擇連接。 若要建立新的連接，請選取 [<新增連接>]  。 如需相關資訊，請參閱 [Azure Data Lake Analytics 連線管理員](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)。

- **JobName：** 指定 U-SQL 作業的名稱。 
- **AnalyticsUnits：** 指定 U-SQL 作業的分析單位計數。
- **優先順序：** 指定 U-SQL 作業的優先順序。 此值的設定範圍為從 0 至 1000。 數字愈小，優先順序愈高。
- **RuntimeVersion：** 指定 U-SQL 作業的 Data Lake Analytics 執行階段版本。 預設會設定為 "default"。 您通常不需要變更這個屬性。
- **Synchronous：** 布林值，指定工作是否要等候作業執行完成。 如果值設為 true，在作業完成後，工作會標示為**成功**。 如果值設為 false，則在作業通過準備階段後，工作會標示為**成功**。

  |值|描述|
  |-----------|-----------------|
  |True|工作結果是以 U-SQL 作業的執行結果為基礎。 作業成功 > 工作成功。 作業失敗 > 工作失敗。 工作成功或失敗 > 工作完成。|
  |False|工作結果是以 U-SQL 作業的提交與準備結果為基礎。 作業提交成功，而且通過準備階段 > 工作成功。 作業提交失敗或作業在準備階段失敗 > 工作失敗。 工作成功或失敗 > 工作完成。|

- **TimeOut：** 指定作業執行的逾時時間 (秒)。 如果作業逾時，則會取消，並標示為失敗。 如果將 **Synchronous** 設定為 false，即無法使用此屬性。

## <a name="parameter-mapping-page-configuration"></a>參數對應頁面設定

使用 [Azure Data Lake Analytics 工作編輯器]  對話方塊的 [參數對應]  頁面，將變數對應至 U-SQL 指令碼中的參數 (U-SQL 變數)。

- **變數名稱：** 選取 [新增]  來新增參數對應之後，從清單中選取系統或使用者定義的變數。 或者，您可以選取 [<新增變數...>]  ，然後使用 [加入變數]  對話方塊來加入新的變數。 如需相關資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)。  

- **參數名稱：** 提供 U-SQL 指令碼中的參數/變數名稱。 確定參數名稱開頭都是 \@ 符號，例如 \@Param1。 

以下是如何將參數傳遞到 U-SQL 指令碼的範例。

**範例 U-SQL 指令碼**
```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    TO @out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

請注意，輸入和輸出路徑會定義在 **\@in** 與 **\@out** 參數之中。 在 U-SQL 指令碼中， **\@in** 與 **\@out** 參數的值是透過「參數對應」設定來動態傳遞。

|變數名稱|參數名稱|
|-------------|--------------|
|User: Variable1|\@in|
|User: Variable2|\@out| 

## <a name="expression-page-configuration"></a>運算式頁面設定

您可以將 [一般] 頁面設定中的所有屬性指派為屬性運算式，以啟用執行階段的屬性動態更新。 如需相關資訊，請參閱[在套件中使用屬性運算式](../../integration-services/expressions/use-property-expressions-in-packages.md)。

## <a name="see-also"></a>另請參閱
- [Azure Data Lake Analytics Connection Manager](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)
- [Azure Data Lake Store 檔案系統工作](../../integration-services/control-flow/azure-data-lake-store-file-system-task.md)
- [Azure Data Lake Store 連線管理員](../../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)

