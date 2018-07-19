---
title: Azure Data Lake Analytics 工作 | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.prod_service: integration-services
ms.component: control-flow
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: yanancai
ms.author: yanacai
manager: craigg
ms.openlocfilehash: 395d790069294aed541f9756fa7caefbb62f9a7b
ms.sourcegitcommit: 44e9bf62f2c75449c17753ed66bf85c43928dbd5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2018
ms.locfileid: "37854408"
---
# <a name="azure-data-lake-analytics-task"></a>Azure Data Lake Analytics 工作

Azure Data Lake Analytics 工作可讓使用者將 U-SQL 作業提交至 Azure Data Lake Analytics 服務。 [Azure Data Lake Analytics (ADLA)](https://azure.microsoft.com/services/data-lake-analytics/)。

Azure Data Lake Analytics 工作是 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。

## <a name="configure-the-azure-data-lake-analytics-task"></a>設定 Azure Data Lake Analytics 工作

若要將 Azure Data Lake Analytics 工作新增至套件，請將它從 SSIS 工具箱拖曳至設計工具畫布。 接著，按兩下該工作，或以滑鼠右鍵按一下該工作並選取 [編輯]，以開啟 [Azure Data Lake Analytics 工作編輯器] 對話方塊。 您可以透過 SSIS 設計工具或以程式設計方式設定屬性。

## <a name="general-page-configuration"></a>一般頁面設定

使用 [一般] 頁面設定 Azure Data Lake Analytics 工作，並提供工作提交 U-SQL 指令碼。 若要深入了解 U-SQL 語言，請參閱 [U-SQL 語言參考](https://msdn.microsoft.com/azure/data-lake-analytics/u-sql/u-sql-language-reference) \(英文\)。

### <a name="basic-configuration"></a>基本設定

- **名稱：** 指定 Azure Data Lake Analytics 工作的名稱。
- **描述：** 指定 Azure Data Lake Analytics 工作的描述。

### <a name="u-sql-configuration"></a>U-SQL 設定

U-SQL 設定有兩個設定：**SourceType** 和根據 **SourceType** 值而定的動態選項。 

- **SourceType：** 指定 U-SQL 指令碼的來源。 指令碼會在 SSIS 套件執行期間提交至 Azure Data Lake Analytics 帳戶。 此屬性具有下表所列的 3 個選項。

|值|描述|  
|-----------|-----------------|  
|**DirectInput**|透過內嵌編輯器指定 U-SQL 指令碼。 選取此值會顯示動態選項 **USQLStatement**。|  
|**FileConnection**|指定本機的.usql 檔案，其中包含 U-SQL 指令碼。 選取此選項會顯示動態選項 **FileConnection**。|  
|**變數**|指定 SSIS 變數，其中包含 U-SQL 指令碼。 選取此值會顯示動態選項 [SourceVariable]。|

- **SourceType 動態選項：** 指定 U-SQL 查詢的指令碼內容。 

|SourceType|動態選項|  
|-----------|-----------------|  
|**SourceType = DirectInput**|直接在選項方塊輸入要提交的 U-SQL 查詢，或按一下瀏覽按鈕 (...)，在 [輸入 U-SQL 查詢] 對話方塊中輸入 U-SQL 查詢。|  
|**SourceType = FileConnection**|選取現有的檔案連線管理員，或按一下 [<新增連線>] 以建立新的檔案連線。 **相關文章：**[檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)、[檔案連線管理員編輯器](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
|**SourceType = Variable**|選取現有的變數，或按一下 [\<新增變數>] 以建立新的變數。 **相關文章：**[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[新增變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)|


### <a name="job-configuration"></a>作業設定
作業設定指定 U-SQL 作業提交屬性。

- **AzureDataLakeAnalyticsConnection：** 指定要提交 U-SQL 指令碼的 Azure Data Lake Analytics 帳戶。 從已定義的連接管理員清單中選擇連接。 若要建立新的連接，請選取 [<新增連接>]。 相關文章：[Azure Data Lake Analytics 連線管理員](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)。

- **JobName：** 指定 U-SQL 作業的名稱。 
- **AnalyticsUnits：** 指定 U-SQL 作業的分析單位計數。
- **優先順序：** 指定 U-SQL 作業的優先順序。 優先順序可設定為 0 到 1000，數字越低，優先順序越高。
- **RuntimeVersion：** 指定 U-SQL 作業的 Azure Data Lake Analytics 執行階段版本。 預設會設定為 "default"。 您通常不需要變更這個屬性。
- **Synchronous：** 布林值，指定工作是否要等候作業執行完成。 設定為 True，會在作業完成之後，將工作標示為成功。 設定為 False，會在作業通過準備階段之後，將工作標示為成功。

|值|描述|
|-----------|-----------------|
|True|工作結果是以 U-SQL 作業的執行結果為基礎。 作業成功 --> 工作成功；作業失敗 --> 工作失敗；工作成功或失敗 --> 工作完成。|
|False|工作結果是以 U-SQL 作業的提交與準備結果為基礎。 作業提交成功且通過準備階段 --> 工作成功；作業提交失敗，或作業在準備階段失敗 --> 工作失敗；工作成功或失敗 --> 工作完成。|

- **TimeOut：** 指定作業執行的逾時時間 (秒)。 作業逾時之後，會取消作業並將工作標示為失敗。如果將 Synchronous 設定為 False，即無法使用 TimeOut 屬性。 如果將 **Synchronous** 設定為 **false**，即無法使用 TimeOut 屬性。

## <a name="parameter-mapping-page-configuration"></a>參數對應頁面設定

使用 [Azure Data Lake Analytics 工作編輯器] 對話方塊的 [參數對應] 頁面，將變數對應至 U-SQL 指令碼中參數 (U-SQL 變數)。

- **變數名稱**：按一下 [新增] 新增參數對應之後，請從清單中選取系統或使用者定義變數，或按一下 [\<新增變數>] 以使用 [新增變數] 對話方塊新增新的變數。 **相關主題：**[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)  

- **參數名稱：** 提供 U-SQL 指令碼中的參數/變數名稱。 確定參數名稱都以 @ 符號開頭，例如 @Param1。 

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

在上述指令碼範例中，輸入和輸出路徑以 **@in** 與 **@out** 參數定義。 U-SQL 指令碼中 **@in** 與 **@out** 參數的值是透過「參數對應」設定來動態傳遞。

|變數名稱|參數名稱|
|-------------|--------------|
|User: Variable1|@in|
|User: Variable2|@out| 

## <a name="expression-page-configuration"></a>運算式頁面設定

一般頁面設定中的所有屬性都可指派為屬性運算式，以啟用執行階段的屬性動態更新。 **相關主題：** [在套件中使用屬性運算式](../../integration-services/expressions/use-property-expressions-in-packages.md)

## <a name="see-also"></a>另請參閱
- [Azure Data Lake Analytics Connection Manager](../../integration-services/connection-manager/azure-data-lake-analytics-connection-manager.md)
- [Azure Data Lake Store 檔案系統工作](../../integration-services/control-flow/azure-data-lake-store-file-system-task.md)
- [Azure Data Lake Store 連線管理員](../../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)

