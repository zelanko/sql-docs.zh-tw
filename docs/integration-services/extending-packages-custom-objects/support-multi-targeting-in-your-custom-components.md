---
title: "在自訂元件中多目標支援 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016)
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 57ac95d7883ce47e1a39d4d50d3f60b968bccf21
ms.contentlocale: zh-tw
ms.lasthandoff: 09/21/2017

---
# <a name="support-multi-targeting-in-your-custom-components"></a>支援在自訂元件中多目標
 您現在可以使用 SSIS 設計師中 SQL Server Data Tools (SSDT) 來建立、 維護及執行封裝，該目標 SQL Server 2016、 SQL Server 2014 或 SQL Server 2012。 若要取得 SSDT for Visual Studio 2015，請參閱[下載最新 SQL Server Data Tools](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt)。 

 在方案總管中，在 Integration Services 專案上按一下滑鼠右鍵，然後選取 [屬性]  以開啟專案的屬性頁。 在 [組態屬性]  的 [一般] 索引標籤中，選取 [TargetServerVersion]  屬性，然後選擇 SQL Server 2016、SQL Server 2014 或 SQL Server 2012。  
   
 ![專案 [屬性] 對話方塊中的 TargetServerVersion 屬性](../../integration-services/media/targetserverversion2.png "TargetServerVersion 屬性中的專案屬性對話方塊")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>多個版本支援和自訂元件的多目標
 
五種 SSIS 自訂延伸模組支援多目標。
-   連接管理員
-   工作
-   列舉值
-   記錄提供者
-   資料流程元件

針對受管理的擴充功能，SSIS 設計工具會載入指定的目標版本的擴充功能版本。 例如：
-   SQL Server 2012 的目標版本時，設計工具載入延伸模組的 2012年版本。
-   SQL Server 2016 的目標版本時，設計工具載入延伸模組的 2016年版本。

COM 延伸模組不支援多目標。 SSIS 設計師永遠載入指定的目標版本不限目前版本的 SQL Server 的 COM 擴充功能。

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>新增基本支援多個版本和多目標

如需基本指引，請參閱[取得 SSIS 自訂擴充功能必須支援 SQL Server 2016 的多個版本支援的 SSDT 2015](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)。 這個部落格文章說明的下列步驟或需求。

-   將您的組件部署到適當的資料夾。

-   SQL Server 2014 和高的版本建立的延伸模組對應檔案。

## <a name="add-code-to-switch-versions"></a>將程式碼加入切換版本

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>切換中自訂連接管理員、 工作、 列舉值或記錄提供者版本

自訂連接管理員、 工作、 列舉值，或記錄提供者，將在降級邏輯加入**SaveToXML**方法。

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

### <a name="switch-versions-in-a-custom-data-flow-component"></a>自訂資料流程元件中的交換器版本

自訂連接管理員、 工作、 列舉值，或記錄提供者，請在新加入降級邏輯**PerformDowngrade**方法。

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

**錯誤訊息。** 無法將類型的 COM 物件轉換 'System.__ComObject' 介面類型 'Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100'。 這項作業失敗，因為具有 IID 為 '{BE8C48A3-155B-4810-BA5C-BDF68A659E9E}' 的介面之 COM 元件上的 QueryInterface 呼叫失敗，因為發生下列錯誤： 不支援這類介面 (來自 HRESULT 的例外狀況： 0x80004002 (E_NOINTERFACE))。 (Microsoft.SqlServer.DTSPipelineWrap)。

**方案。** 如果您的自訂擴充功能參考 SSIS interop 組件，例如 Microsoft.SqlServer.DTSPipelineWrap 或 Microsoft.SqlServer.DTSRuntimeWrap，設定的值**內嵌 Interop 類型**屬性 * * False"。

![內嵌 Interop 類型](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>無法載入某些類型，當目標版本是 SQL Server 2012

此問題會影響某些類型，例如 IErrorReportingService 或 IUserPromptService。

**錯誤訊息 （例如）。** 無法從組件載入類型 'Microsoft.DataWarehouse.Design.IErrorReportingService' ' Microsoft.DataWarehouse，Version = 13.0.0.0，Culture = neutral，PublicKeyToken = 89845dcd8080cc91'。

**因應措施。** SQL Server 2012 的目標版本時，請使用 MessageBox 而不是這些介面。


