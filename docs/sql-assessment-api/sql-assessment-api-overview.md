---
title: SQL Server 評定 API
description: 描述什麼是 SQL Server 評定 API。
ms.prod: sql
ms.technology: tools-other
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 11/04/2019
ms.openlocfilehash: 76a6e99d06061ae581b753ce0edd96a5a82d0f95
ms.sourcegitcommit: fc99fdd586eabc2d60f33056123398f263d5913d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/10/2020
ms.locfileid: "78946714"
---
# <a name="sql-assessment-api"></a>SQL 評定 API

SQL 評定 API 會提供一種機制來評定您的 SQL Server 設定，以了解最佳作法。 此 API 會以包含 SQL Server 小組建議之最佳作法規則的規則集來傳遞。 這個規則集會隨著新版本的發行而增強，但同時也會建置 API，以提供高度可自訂且可擴充的解決方案。 因此，使用者可以調整預設規則，並建立自己的規則。

當您想要確保您的 SQL Server 設定符合建議的最佳作法時，SQL 評定 API 會很有用。 初始評定之後，可以透過定期排程的評定來追蹤設定穩定性。

API 可用來評定 Azure SQL Database 受控執行個體和 SQL Server 2012 版和更新版本。 支援 Linux 上的 SQL。

## <a name="rules"></a>規則

規則有時稱為「檢查」，定義於 JSON 格式的檔案中。 規則集格式需要指定規則集名稱和版本。 因此，當您使用自訂規則集時，您可以輕鬆地知道哪些規則集來自哪些建議。 

GitHub 上提供 Microsoft 隨附的規則集。 如需詳細資訊，您可以瀏覽[範例存放庫](https://aka.ms/sql-assessment-api)。

## <a name="sql-assessment-cmdlets-and-smo-extension"></a>SQL 評定 Cmdlet 和 SMO 延伸模組

SQL 評定 API 屬於 [SQL Server 管理物件 (SMO)](../relational-databases/server-management-objects-smo/installing-smo.md) 2019 年 7 月發行版本和更新版本，以及 [SQL Server PowerShell 模組](../powershell/download-sql-server-ps-module.md) 2019 年 7 月發行版本和更新版本。

* [安裝 SMO](../relational-databases/server-management-objects-smo/installing-smo.md)

* [安裝 SQL Server PowerShell 模組](../powershell/download-sql-server-ps-module.md)

SqlServer 模組將取得兩個新的 Cmdlet，可搭配 SQL 評定 API 使用：

* **Get-SqlAssessmentItem** – 提供 SQL Server 物件的可用評定檢查清單

* **Invoke-SqlAssessment** – 提供評定的結果

SMO 架構是由提供下列方法的 SQL 評定 API 延伸模組所補充：

* **GetAssessmentItems** – 傳回特定 SQL 物件的可用檢查 (IEnumerable<…>)

* **GetAssessmentResults** – 同步評估評定並傳回結果和錯誤 (如果有的話) (IEnumerable<…>)

* **GetAssessmentResultsList** – 非同步評估評定並傳回結果和錯誤 (如果有的話) (Task<…>)

## <a name="get-started-using-sql-assessment-cmdlets"></a>開始使用 SQL 評定 Cmdlet

系統會根據所選的 SQL Server 物件執行評定。 在預設規則集中，只有兩種物件的檢查：Server 和 Database (除此之外，API 還支援兩種類型：Filegroup 和 AvailabilityGroup)。 如果您想要評定 SQL 執行個體及其所有資料庫，應該分別針對每個物件執行 SQL 評定 Cmdlet。 或者，您可以將用於評定的物件傳遞至變數或管線中的 SQL 評定 Cmdlet。

SqlServer 和 RegisteredServer 物件是可互換的，因此您可以將這兩個物件中的任何物件傳遞至 SQL 評定 Cmdlet。

瀏覽下列範例以開始使用。

1. 取得本機預設執行個體的可用檢查清單，以熟悉檢查。 在此範例中，我們會將 Get-SqlInstance Cmdlet 的輸出輸送至 Get-SqlAssessmentItem Cmdlet，以便將執行個體物件傳遞至其中。

    ```powershell
    Get-SqlInstance -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

2. 取得執行個體之所有資料庫的可用檢查清單。 在這裡，我們將使用 Get-Item Cmdlet 和以 Windows Powershell SQL Server 提供者所實作的路徑來取得資料庫清單，然後將其輸送至 Get-SqlDatabase Cmdlet。

    ```powershell
    Get-Item SQLSERVER:\SQL\localhost\default | Get-SqlAssessmentItem
    ```

    此外，您也可以使用 Get-SqlDatabase Cmdlet 執行相同的動作。

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

3. 取得執行個體之所有資料庫的可用檢查清單。 在這裡，我們將使用 Get-Item Cmdlet 和以 Windows Powershell SQL Server 提供者所實作的路徑來取得資料庫清單，然後將其輸送至 Get-SqlDatabase Cmdlet。

    ```powershell
    Get-Item SQLSERVER:\SQL\localhost\default | Get-SqlAssessmentItem
    ```

    此外，您也可以使用 Get-SqlDatabase Cmdlet 執行相同的動作。

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' | Get-SqlAssessmentItem
    ```

4. 叫用執行個體的評定，並將結果儲存至 SQL 資料表。 在此範例中，我們會將 Get-SqlInstance Cmdlet 的輸出輸送至 Invoke-SqlAssessment Cmdlet，這會將結果輸送至 Write-SqlTableData Cmdlet。 在此範例中，Invoke-Assessment Cmdlet 是以 `-FlattenOutput` 參數執行的。 此參數可讓輸出適用於 Write-SqlTableData Cmdlet。 如果您省略此參數，後者會引發錯誤。

    ```powershell
    Get-SqlInstance -ServerInstance 'localhost' |
    Invoke-SqlAssessment -FlattenOutput |
    Write-SqlTableData -ServerInstance 'localhost' -DatabaseName SQLAssessmentDemo -SchemaName Assessment -TableName Results -Force
    ```

    現在讓我們叫用執行個體所有資料庫的評定，並將結果加入至相同的資料表。

    ```powershell
    Get-SqlDatabase -ServerInstance 'localhost' |
    Invoke-SqlAssessment -FlattenOutput |
    Write-SqlTableData -ServerInstance 'localhost' -DatabaseName SQLAssessmentDemo -SchemaName Assessment -TableName Results -Force
    ```

5. 依照資料表中的描述和連結，進一步了解建議。

6. 根據您的環境和組織需求，自訂規則 (請參閱下方)。

7. 排程工作或作業，定期或依需求執行評定以測量進度。

## <a name="customizing-rules"></a>自訂規則

規則的設計可自訂且可擴充。 Microsoft 的規則集設計為適用於大多數環境。 不過，不可能有一個適用於每個單一環境的規則集。 使用者可以撰寫自己的 JSON 檔案，並自訂現有的規則或加入新的規則。 [範例存放庫](https://aka.ms/sql-assessment-api)中提供自訂和完整 Microsoft 發行規則集的範例。 如需有關如何以自訂 JSON 檔案執行 SQL 評定 Cmdlet 的詳細資訊，請使用 Get-Help Cmdlet。

### <a name="options-available-with-rule-customization-feature"></a>規則自訂功能提供的選項

#### <a name="enablingdisabling-certain-rules-or-groups-of-rules-using-tags"></a>啟用/停用特定規則或規則群組 (使用標籤)

當特定規則未套用至您的環境，或在排定的工作完成以更正問題之前，您可以將它們解除鎖定。

#### <a name="changing-threshold-parameters"></a>變更閾值參數

特定規則的閾值會與計量的目前值進行比較，以找出問題。 如果預設閾值不符合，您可以變更它們。

#### <a name="adding-more-rules-written-by-you-or-third-parties"></a>新增您或協力廠商所撰寫的更多規則

您可以將一或多個 JSON 檔案當作參數，新增至 SQL 評定 API 呼叫，藉此將規則集合排在一起。 您的組織可能會撰寫這些檔案，或向協力廠商取得這些檔案。 例如，您可以讓 JSON 檔案停用 Microsoft 規則集的特定規則，而讓另一個 JSON 檔案由產業專家提供，其中包含您認為對環境有用的規則，然後是另一個 JSON 檔案，用於變更該 JSON 檔案中的一些閾值。

> [!IMPORTANT]  
> 我們強烈建議您，在徹底審查之前，不要使用來自不受信任來源的規則集，以確保它們安全無誤。

## <a name="next-steps"></a>後續步驟

查看 [SQL Server 管理物件 (SMO)](../relational-databases/server-management-objects-smo/overview-smo.md) 和 [PowerShell](../powershell/download-sql-server-ps-module.md)。
