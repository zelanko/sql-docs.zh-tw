---
title: 建立自訂記錄提供者 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: extending-packages-custom-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom log providers [Integration Services], creating
ms.assetid: fc20af96-9eb8-4195-8d3f-8a4d7c753f24
caps.latest.revision: 58
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 440b855438bce7fedbcde3a9db8a0289c071263a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="creating-a-custom-log-provider"></a>建立自訂記錄提供者
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 執行階段環境具有廣泛的記錄功能。 用於擷取封裝執行期間所發生之事件的記錄檔。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包括各種記錄提供者，讓記錄可以多種格式，例如 XML、文字、資料庫或 Windows 事件記錄檔加以建立並儲存記錄檔。 如果這些提供者或輸出格式都不符合您的需求，可以建立自訂記錄提供者。  
  
 建立自訂記錄提供者所需的步驟類似於為 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 建立任何其他自訂物件的步驟：  
  
-   建立繼承自基底類別的新類別。 對於記錄提供者而言，基底類別是 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>。  
  
-   將可識別物件類型的屬性套用至類別。 對於記錄提供者而言，屬性是 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>。  
  
-   覆寫基底類別之方法與屬性的實作。 對於記錄提供者而言，這些包括 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 屬性以及 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>、<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 和 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> 方法。  
  
-   在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中並未實作自訂記錄提供者的自訂使用者介面。  
  
## <a name="getting-started-with-a-custom-log-provider"></a>開始使用自訂記錄提供者  
  
### <a name="creating-projects-and-classes"></a>建立專案和類別  
 因為所有的 Managed 記錄提供者都是從 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase> 基底類別衍生，所以在建立自訂記錄提供者時的第一個步驟是以慣用的 Managed 程式語言建立類別庫專案，然後建立繼承自基底類別的類別。 在此衍生的類別中，您將覆寫基底類別的方法與屬性，以實作自訂功能。  
  
 設定專案以使用強式名稱金鑰檔案來簽署將產生的組件。  
  
> [!NOTE]  
>  許多 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 記錄提供者都有自訂使用者介面，以實作 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI>，以及使用可用連線管理員的篩選下拉式清單，取代 [設定 SSIS 記錄] 對話方塊中的 [設定] 文字方塊。 不過，在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中並未實作自訂記錄提供者的自訂使用者介面。  
  
### <a name="applying-the-dtslogprovider-attribute"></a>套用 DtsLogProvider 屬性  
 將 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 屬性套用至您已建立的類別，以便將它識別為記錄提供者。 此屬性會提供記錄提供者的名稱和描述等設計階段資訊。 屬性 (Attribute) 的 **DisplayName** 和 **Description** 屬性 (Property) 會對應至顯示在 [設定 SSIS 記錄] 編輯器中的 [名稱] 和 [描述] 資料行，此編輯器會在為 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中的套件設定記錄時顯示。  
  
> [!IMPORTANT]  
>  未使用屬性 (Attribute) 的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.LogProviderType%2A> 屬性 (Property)。 不過，您必須為它輸入值，否則自訂記錄提供者將不會顯示在可用記錄提供者的清單中。  
  
> [!NOTE]  
>  既然在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中未實作自訂記錄提供者的自訂使用者介面，為 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 屬性指定值並沒有作用。  
  
```vb  
<DtsLogProvider(DisplayName:="MyLogProvider", Description:="A simple log provider.", LogProviderType:="Custom")> _  
Public Class MyLogProvider  
     Inherits LogProviderBase  
    ' TODO: Override the base class methods.  
End Class  
```  
  
```csharp  
[DtsLogProvider(DisplayName="MyLogProvider", Description="A simple log provider.", LogProviderType="Custom")]  
public class MyLogProvider : LogProviderBase  
{  
    // TODO: Override the base class methods.  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-log-provider"></a>建立、部署和偵錯自訂記錄提供者  
 在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中建立、部署和偵錯自訂記錄提供者的步驟，非常類似於其他類型的自訂物件所需的步驟。 如需詳細資訊，請參閱[建立、部署和偵錯自訂物件](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)。  
  
## <a name="see-also"></a>另請參閱  
 [撰寫自訂記錄提供者程式碼](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)   
 [開發自訂記錄提供者的使用者介面](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-user-interface-for-a-custom-log-provider.md)  
  
  
