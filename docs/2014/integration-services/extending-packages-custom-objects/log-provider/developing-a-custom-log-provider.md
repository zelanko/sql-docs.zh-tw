---
title: 開發自訂記錄提供者 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- SSIS packages, log providers
- custom log providers [Integration Services]
- SQL Server Integration Services packages, log providers
- log providers [Integration Services]
- packages [Integration Services], logs
- Integration Services packages, log providers
ms.assetid: 3f715b95-7074-4f5c-8ae2-246998052e78
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: af3478e254f01f7cf53d5a09b6febab3b1e85e8b
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176292"
---
# <a name="developing-a-custom-log-provider"></a>開發自訂記錄提供者
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 具有多種記錄功能，可以擷取在封裝執行期間所發生的事件。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包括各種記錄提供者，讓記錄可以 XML、文字、資料庫或 Windows 事件記錄檔格式加以建立並儲存記錄檔。 如果所提供的記錄提供者與輸出格式並未完全符合您的需求，可以建立自訂記錄提供者。

 若要建立自訂記錄提供者，您必須建立繼承自 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase> 基底類別的類別、將 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 屬性 (Attribute) 套用至新類別，以及覆寫基底類別的重要方法與屬性 (Property)，包括 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 屬性 (Property) 與 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 方法。

## <a name="in-this-section"></a>本節內容
 本節描述如何建立、設定和撰寫自訂記錄提供者的程式碼。

 [建立自訂記錄提供者](creating-a-custom-log-provider.md)描述如何建立自訂記錄提供者專案的類別。

 撰寫[自訂記錄提供者的程式碼](coding-a-custom-log-provider.md)描述如何藉由覆寫基類的方法和屬性，來執行自訂記錄提供者。

 [開發自訂記錄提供者的使用者介面](developing-a-user-interface-for-a-custom-log-provider.md)中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]不支援自訂記錄提供者的自訂使用者介面。

## <a name="related-topics"></a>相關主題

### <a name="information-common-to-all-custom-objects"></a>自訂物件的共通資訊
 如需有關 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中可以建立之所有類型自訂物件適用的共通資訊，請參閱下列主題：

 [開發 Integration Services 的自訂物件](../developing-custom-objects-for-integration-services.md)說明為[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]執行所有類型之自訂物件的基本步驟。

 [保存自訂物件](../persisting-custom-objects.md)描述自訂持續性，並在必要時加以說明。

 [建立、部署和調試自訂物件](../building-deploying-and-debugging-custom-objects.md)說明建立、簽署、部署和偵錯工具自訂物件的技術。

### <a name="information-about-other-custom-objects"></a>其他自訂物件的相關資訊
 如需有關在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中可以建立之其他類型自訂物件的詳細資訊，請參閱下列主題：

 [開發自訂工作](../task/developing-a-custom-task.md)討論如何編寫自訂工作的程式。

 [開發自訂連線管理員](../connection-manager/developing-a-custom-connection-manager.md)討論如何編寫自訂連接管理員的程式。

 [開發自訂 ForEach 列舉](../foreach-enumerator/developing-a-custom-foreach-enumerator.md)值討論如何編寫自訂枚舉器的程式。

 [開發自訂資料流程元件](../data-flow/developing-a-custom-data-flow-component.md)討論如何程式設計自訂資料流程來源、轉換和目的地。

![Integration Services 圖示（小型）](../../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。


