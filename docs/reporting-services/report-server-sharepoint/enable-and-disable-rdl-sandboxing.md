---
title: "啟用和停用 RDL 沙箱 |Microsoft 文件"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5619e9f-ec5b-4376-9b34-1f74de6fade7
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2a435c6f6b5dc2d9df676f504837393d448820a4
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="enable-and-disable-rdl-sandboxing"></a>啟用或停用 RDL 沙箱
  RDL (報表定義語言) 沙箱功能可在多個租用戶使用報表伺服器之單一 Web 伺服陣列的環境中，讓您偵測及限制個別租用戶使用特定資源類型的情形。 這種情形的一個範例是裝載服務案例，在此案例中，您可能要為由多個可能分屬不同公司的租用戶所使用的報表伺服器，維護單一 Web 伺服器陣列。 您身為報表伺服器管理員，可以啟用此功能來幫助您達成下列目標：  
  
-   限制外部資源的大小。 外部資源包括影像、.xslt 檔案和對應資料。  
  
-   在報表發行時間，限制用於運算式文字的型別和成員。  
  
-   在報表處理時間，限制運算式的文字長度和傳回值大小。  
  
 當啟用 RDL 沙箱功能時，將會停用下列功能：  
  
-   中的自訂程式碼**\<程式碼 >**報表定義的項目。  
  
-   RDL 對於 [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] 自訂報表項目的回溯相容性模式。  
  
-   運算式中的指名參數。  
  
 本主題說明中的每個項目\< **RDLSandboxing**> RSReportServer.Config 檔案中的項目。 如需如何編輯此檔案的詳細資訊，請參閱[Modify a Reporting Services Configuration File (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) (修改 Reporting Services 組態檔 (RSreportserver.config))。 伺服器追蹤記錄會記錄與 RDL 沙箱功能有關的活動。 如需追蹤紀錄的詳細資訊，請參閱 [報表伺服器服務追蹤記錄](../../reporting-services/report-server/report-server-service-trace-log.md)。  
  
## <a name="example-configuration"></a>範例組態  
 下列範例示範設定和範例值\< **RDLSandboxing**> RSReportServer.Config 檔案中的項目。  
  
```  
<RDLSandboxing>  
   <MaxExpressionLength>5000</MaxExpressionLength>  
   <MaxResourceSize>5000</MaxResourceSize>  
   <MaxStringResultLength>3000</MaxStringResultLength>  
   <MaxArrayResultLength>250</MaxArrayResultLength>  
   <Types>  
      <Allow Namespace=”System.Drawing” AllowNew=”True”>Bitmap</Allow>  
      <Allow Namespace=”TypeConverters.Custom” AllowNew=”True”>*</Allow>  
   </Types>  
   <Members>  
      <Deny>Format</Deny>  
      <Deny>StrDup</Deny>  
   </Members>  
</RDLSandboxing>  
```  
  
## <a name="configuration-settings"></a>組態設定  
 下表提供有關組態設定的資訊。 設定會依其出現在組態檔的順序顯示。  
  
|設定|說明|  
|-------------|-----------------|  
|**MaxExpressionLength**|RDL 運算式中允許的最大字元數。<br /><br /> 預設值：1000|  
|**MaxResourceSize**|外部資源允許的最大 KB 數。<br /><br /> 預設值：100|  
|**MaxStringResultLength**|RDL 運算式的傳回值中允許的最大字元數。<br /><br /> 預設值：1000|  
|**MaxArrayResultLength**|RDL 運算式的陣列傳回值中允許的最大項目數。<br /><br /> 預設值：100|  
|**類型**|RDL 運算式中允許的成員清單。|  
|**Allow**|RDL 運算式中允許的類型或類型集合。|  
|**命名空間**|**Allow** 的屬性，這是包含一或多個套用至 Value 之類型的命名空間。 這個屬性不區分大小寫。|  
|**AllowNew**|布林值屬性，如**允許**，控制是否允許類型的新執行個體建立 RDL 運算式或 RDL **\<類別 >**項目。<br /><br /> 注意：當啟用 **RDLSandboxing** 時，無論是否設定 [AllowNew]，都無法在 RDL 運算式中建立新的陣列。|  
|**值**|**Allow** 的值，這是 RDL 運算式中允許之類型的名稱。 **\*** 值表示允許命名空間中的所有類型。 這個屬性不區分大小寫。|  
|**成員**|如需中所包含之型別的清單**\<類型 >**元素中，不允許在 RDL 運算式中的成員名稱的清單。|  
|**拒絕**|RDL 運算式中不允許的成員名稱。 這個屬性不區分大小寫。<br /><br /> 注意： 當**拒絕**指定成員，不允許具有這個名稱的所有類型的所有成員。|  
  
## <a name="working-with-expressions-when-rdl-sandboxing-is-enabled"></a>在啟用 RDL 沙箱功能時使用運算式  
 您可以修改 RDL 沙箱功能，透過下列方式幫助管理運算式所使用的資源：  
  
-   限制用於運算式的字元數。  
  
-   限制運算式傳回之結果的大小。  
  
-   允許可用於運算式的特定類型清單。  
  
-   針對可用於運算式的允許類型清單，依名稱限制成員的清單。  
  
-   RDL 沙箱功能可讓您建立核准的類型清單以及遭到拒絕的成員清單。 核准的類型清單稱為允許清單， 遭到拒絕的成員清單則稱為封鎖清單。  
  
> [!NOTE]  
>  在報告定義中，電腦無法得知運算式參考的每個執行個體的類型。 當您將成員加入至封鎖清單時，您會在允許清單的所有類型中拒絕該名稱的所有成員。  
  
 RDL 運算式的結果會在執行階段驗證。 當發行報表時，便會在報表定義中驗證 RDL 運算式。 監視報表伺服器追蹤記錄，查看是否有違規情形。 如需詳細資訊，請參閱 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)。  
  
### <a name="working-with-types"></a>處理類型  
 當您將某個類型加入至允許清單時，您會控制存取 RDL 運算式的下列進入點：  
  
-   某個類型的靜態成員。  
  
-   [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **新** 方法。  
  
-   **\<類別 >**報表定義中的項目。  
  
-   您已經針對允許清單內的某個類型加入至封鎖清單中的成員。  
  
 允許清單不能控制下列進入點：  
  
-   報表資料集。 報表資料集中從查詢傳回的欄位可能會包含任何有效的 RDL 類型。  
  
-   報表參數。 使用者提供的參數值可能會包含任何有效的 RDL 類型。  
  
-   具備已啟用的類型而不在封鎖清單內的成員。 根據預設，將會啟用允許清單中所有類型的所有成員。 當您將成員名稱加入至封鎖清單時，您會在允許清單的所有類型中拒絕該名稱的所有成員。  
  
 若要啟用一個類型的成員，但是拒絕另一個類型的同名成員，您必須執行以下動作：  
  
-   新增**\<拒絕 >**成員名稱的項目。  
  
-   針對您想要啟用的成員，在自訂組件的某個類別上建立另一個名稱的 Proxy 成員。  
  
-   將這個新類別加入至允許清單。  
  
 若要將 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 函數加入允許清單，請將 Microsoft.VisualBasic 命名空間中的對應類型加入允許清單。  
  
 若要將 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 類型關鍵字加入至允許清單，請將對應的 CLR 類型加入至允許清單。 例如，若要使用[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].NET Framework 關鍵字**整數**，加入下列 XML 片段至 **\<RDLSandboxing >**項目：  
  
```  
<Allow Namespace="System">Int32</Allow>  
```  
  
 若要將一般或 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 可為 Null 的類型加入至允許清單，您必須執行以下動作：  
  
-   針對一般或 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 可為 Null 的類型建立 Proxy 類型。  
  
-   將 Proxy 類型加入至允許清單。  
  
 將自訂組件中的類型加入至允許清單並不會以隱含方式授與此組件的執行權限。 您必須特別修改程式碼存取安全性檔案，並提供組件的執行權限。 如需詳細資訊，請參閱 [Code Access Security in Reporting Services](../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)(Reporting Services 中的程式碼存取安全性)。  
  
#### <a name="maintaining-the-deny-list-of-members"></a>維護\<拒絕 > 清單中的成員  
 當您將新的類型加入至允許清單時，請使用下列清單來判斷何時可能需要更新成員的封鎖清單：  
  
-   當您使用導入新類型的版本來更新自訂組件時。  
  
-   當您將成員加入至允許清單中的類型時。  
  
-   當您在報表伺服器上更新 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 時。  
  
-   當您將報表伺服器升級到更新版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]時。  
  
-   當您因為新的成員可能已加入至 RDL 類型，而更新報表伺服器來處理較新的 RDL 結構描述時。  
  
### <a name="working-with-operators-and-new"></a>使用運算子及 New  
 依預設，一定會允許 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 語言運算子，但是 **New**除外。 **新增**運算子由**AllowNew**屬性**\<允許 >**項目。 其他語言運算子，例如預設集合存取子運算子 **!** 以及像是 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] CInt  .NET Framework 轉換巨集，都一律允許。  
  
 不支援將運算子加入至封鎖清單中，包括自訂運算子。 若要排除某個類型的運算子，您必須執行下列動作：  
  
-   建立 Proxy 類型，此類型不會實作您想要排除的運算子。  
  
-   將 Proxy 類型加入至允許清單。  
  
 若要在 RDL 運算式中建立新的陣列，請在您定義之類別上的方法中建立此陣列，並將該類別加入至允許清單。  
  
 若要在 RDL 運算式中建立新的陣列，您必須執行下列動作：  
  
-   定義新的類別，並在該類別上的方法中建立此陣列。  
  
-   將此類別加入至允許清單。  
  
## <a name="see-also"></a>請參閱＜  
 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [報表伺服器服務追蹤記錄](../../reporting-services/report-server/report-server-service-trace-log.md)  
  
  
