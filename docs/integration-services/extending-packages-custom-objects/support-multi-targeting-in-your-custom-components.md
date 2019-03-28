---
title: 支援自訂元件中的多目標 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 67005532329ebdda27f0c86985604fb8a63babe1
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58273546"
---
# <a name="support-multi-targeting-in-your-custom-components"></a>支援自訂元件中的多目標
 您現在可以在 SQL Server Data Tools (SSDT) 中使用 SSIS 設計工具，來建立、維護和執行目標為 SQL Server 2016、SQL Server 2014 或 SQL Server 2012 的套件。 若要取得 SSDT for Visual Studio 2015，請參閱[下載最新的 SQL Server Data Tools](../../ssdt/download-sql-server-data-tools-ssdt.md)。 

 在方案總管中，在 Integration Services 專案上按一下滑鼠右鍵，然後選取 [屬性]  以開啟專案的屬性頁。 在 [組態屬性]  的 [一般] 索引標籤中，選取 [TargetServerVersion]  屬性，然後選擇 SQL Server 2016、SQL Server 2014 或 SQL Server 2012。  
   
 ![專案屬性對話方塊中的 TargetServerVersion 屬性](../../integration-services/media/targetserverversion2.png "專案屬性對話方塊中的 TargetServerVersion 屬性")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>自訂元件的多版本支援和多目標
 
全五種 SSIS 自訂延伸模組支援多目標。
-   連接管理員
-   工作
-   列舉值
-   記錄提供者
-   資料流程元件

針對受控延伸模組，SSIS 設計工具會載入指定目標版本的延伸模組版本。 例如：
-   當目標版本為 SQL Server 2012 時，設計工具會載入延伸模組的 2012 版本。
-   當目標版本為 SQL Server 2016 時，設計工具會載入延伸模組的 2016 版本。

COM 延伸模組不支援多目標。 無論指定的目標版本為何，SSIS 設計工具一律載入目前 SQL Server 版本的 COM 延伸模組。

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>新增多版本和多目標的基本支援

如需基本指引，請參閱 [Getting your SSIS custom extensions to be supported by the multi-version support of SSDT 2015 for SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/) (使用 SQL Server 2016 的 SSDT 2015 多版本支援來支援 SSIS 自訂延伸模組)。 本部落格文章描述下列步驟或需求。

-   將您的組件部署到適當的資料夾。

-   建立 SQL Server 2014 和更新版本的延伸模組對應檔案。

## <a name="add-code-to-switch-versions"></a>新增程式碼以切換版本

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>在自訂連線管理員、工作、列舉值或記錄提供者中切換版本

若為自訂連線管理員、工作、列舉值或記錄提供者，請在 **SaveToXML** 方法中新增降級邏輯。

```csharp
public void SaveToXML(XmlDocument doc, IDTSInfoEvents events)
{
    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
    }

    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2012)
    {
         // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
    }
}
```

### <a name="switch-versions-in-a-custom-data-flow-component"></a>在自訂資料流程元件中切換版本

若為自訂連線管理員、工作、列舉值或記錄提供者，請在 **PerformDowngrade** 方法中新增降級邏輯。

```csharp
public override void PerformDowngrade(int pipelineVersion, DTSTargetServerVersion targetServerVersion)
{
    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
        ComponentMetaData.Version = 8;
    }

    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2012)
    {
          // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
        ComponentMetaData.Version = 6;
    }
}
```

## <a name="common-errors"></a>常見錯誤

### <a name="invalidcastexception"></a>InvalidCastException

**錯誤訊息。** 無法將 'System.__ComObject' 類型的 COM 物件轉換成 'Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100' 介面類型。 這項作業失敗，因為 IID 為 '{BE8C48A3-155B-4810-BA5C-BDF68A659E9E}' 的介面之 COM 元件上的 QueryInterface 呼叫，因為發生下列錯誤而失敗：不支援這類介面 (來自 HRESULT 的例外狀況：0x80004002 (E_NOINTERFACE))。 (Microsoft.SqlServer.DTSPipelineWrap)。

**解決方案。** 如果您的自訂延伸模組參考 SSIS interop 組件，例如 Microsoft.SqlServer.DTSPipelineWrap 或 Microsoft.SqlServer.DTSRuntimeWrap，請將 [內嵌 Interop 類型] 屬性的值設成 **False**。

![內嵌 Interop 類型](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>當目標版本是 SQL Server 2012 時無法載入某些類型

此問題會影響某些類型，例如 IErrorReportingService 或 IUserPromptService。

**錯誤訊息 (範例)。** 無法從組件 'Microsoft.DataWarehouse, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' 載入類型 'Microsoft.DataWarehouse.Design.IErrorReportingService'。

**因應措施。** 當目標版本為 SQL Server 2012 時，請使用 MessageBox 而不是這些介面。

