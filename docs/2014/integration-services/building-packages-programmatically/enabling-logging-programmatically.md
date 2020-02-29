---
title: 以程式設計的方式啟用記錄 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- Integration Services packages, logs
- SSIS logging
- log providers [Integration Services]
- logs [Integration Services], enabling
- LoggingMode property
- LogProvider object
- packages [Integration Services], logs
ms.assetid: 3222a1ed-83eb-421c-b299-a53b67bba740
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bff8df8004c4553d5fa07ebb5ca46863a998bd85
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176548"
---
# <a name="enabling-logging-programmatically"></a>以程式設計的方式啟用記錄
  執行階段引擎提供 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 物件的集合，允許在封裝驗證和執行期間擷取事件特定資訊。 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> 物件可供 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer> 物件使用，包括 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>、<xref:Microsoft.SqlServer.Dts.Runtime.Package>、<xref:Microsoft.SqlServer.Dts.Runtime.ForLoop> 和 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 物件。 在個別容器或是整個封裝上啟用記錄。

 有好幾種類型的記錄提供者可供容器使用。 這可提供以多種格式建立和儲存記錄資訊的彈性。 在記錄中編列容器物件是兩個步驟的程序：首先啟用記錄，然後選取記錄提供者。 該容器的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingOptions%2A> 與 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> 屬性是用以指定記錄的事件並選取記錄提供者。

## <a name="enabling-logging"></a>啟用記錄
 在每個可以執行記錄的容器中所找到的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> 屬性，可判斷容器的事件資訊是否記錄到事件記錄檔中。 將會從 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode> 結構指派值給這個屬性，而且預設會從容器的父系繼承。 如果容器是封裝，也因此沒有父系，則屬性會使用 <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode.UseParentSetting>，而其預設值為 `Disabled`。

### <a name="selecting-a-log-provider"></a>選取記錄提供者
 在將 <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> 屬性設定為 `Enabled` 之後，已將記錄提供者加入容器的 <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> 集合以完成該程序。 <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> 集合可在 <xref:Microsoft.SqlServer.Dts.Runtime.LoggingOptions> 物件上使用，而且包含為容器所選取的記錄提供者。 會呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders.Add%2A> 方法以建立提供者並將它加入集合中。 該方法接著會傳回加入集合的記錄提供者。 每個提供者都有該提供者唯一的組態設定，而且這些屬性是使用 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A> 屬性來設定。

 下列表格列出可用的記錄提供者、其說明及其 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A> 資訊。

|提供者|描述|ConfigString 屬性|
|--------------|-----------------|---------------------------|
|SQL Server Profiler|產生可能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler 中擷取和檢視的 SQL 追蹤。 此提供者的預設副檔名為 .trc。|不需要組態。|
|SQL Server|將事件記錄項目寫入任何 **資料庫中的**sysssislog[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供者需要指定連至資料庫的連接，還須指定目標資料庫名稱。|
|文字檔|將事件記錄項目以逗號分隔值 (CSV) 的格式寫入 ASCII 文字檔。 此提供者的預設副檔名為 .log。|檔案連接管理員的名稱。|
|Windows 事件記錄檔|記錄到本機電腦上「應用程式」記錄中的標準 Windows 事件記錄檔。|不需要組態。|
|XML 檔案|將事件記錄檔項目寫入 XML 格式化的檔案。 此提供者的預設副檔名為 .xml。|檔案連接管理員的名稱。|

 透過設定容器的 `EventFilterKind` 與 `EventFilter` 屬性，會將事件包括在事件記錄檔中或排除在外。 
  `EventFilterKind` 結構包含兩個值：`ExclusionFilter` 與 `InclusionFilter`，它們指出加入 `EventFilter` 的事件是否包括在事件記錄檔中。 接著會指派含有是篩選主旨之事件名稱的字串陣列給 `EventFilter` 屬性。

 下列程式碼允許在封裝上記錄、將文字檔的記錄提供者加入 <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> 集合，並指定將事件清單包括在記錄輸出中。

## <a name="sample"></a>範例

```csharp
using System;
using Microsoft.SqlServer.Dts.Runtime;

namespace Microsoft.SqlServer.Dts.Samples
{
  class Program
  {
    static void Main(string[] args)
    {
      Package p = new Package();

      ConnectionManager loggingConnection = p.Connections.Add("FILE");
      loggingConnection.ConnectionString = @"C:\SSISPackageLog.txt";

      LogProvider provider = p.LogProviders.Add("DTS.LogProviderTextFile.2");
      provider.ConfigString = loggingConnection.Name;
      p.LoggingOptions.SelectedLogProviders.Add(provider);
      p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion;
      p.LoggingOptions.EventFilter = new String[] { "OnPreExecute", 
         "OnPostExecute", "OnError", "OnWarning", "OnInformation" };
      p.LoggingMode = DTSLoggingMode.Enabled;

      // Add tasks and other objects to the package.

    }
  }
}
```

```vb
Imports Microsoft.SqlServer.Dts.Runtime

Module Module1

  Sub Main()

    Dim p As Package = New Package()

    Dim loggingConnection As ConnectionManager = p.Connections.Add("FILE")
    loggingConnection.ConnectionString = "C:\SSISPackageLog.txt"

    Dim provider As LogProvider = p.LogProviders.Add("DTS.LogProviderTextFile.2")
    provider.ConfigString = loggingConnection.Name
    p.LoggingOptions.SelectedLogProviders.Add(provider)
    p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion
    p.LoggingOptions.EventFilter = New String() {"OnPreExecute", _
       "OnPostExecute", "OnError", "OnWarning", "OnInformation"}
    p.LoggingMode = DTSLoggingMode.Enabled

    ' Add tasks and other objects to the package.

  End Sub

End Module
```

![Integration Services 圖示（小型）](../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。

## <a name="see-also"></a>另請參閱
 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)


