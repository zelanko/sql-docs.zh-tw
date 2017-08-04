---
title: "自訂工作流程 XML 描述 (Master Data Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: e267e5f4-38bb-466d-82e8-871eabeec07e
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ca6f208bab4ed0b7932d3bd5f7e9a911b8b2c8af
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-custom-workflow---xml-description"></a>建立自訂工作流程的 XML 描述
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 中，當工作流程啟動時，SQL Server MDS 工作流程整合服務會呼叫 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> 方法。 此方法會收到有關觸發工作流程商務規則之項目的中繼資料和資料，做為 XML 的區塊。 如需範例實作工作流程處理常式程式碼，請參閱[自訂工作流程的範例 &#40;Master Data services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md).  
  
 以下範例顯示傳送至工作流程處理常式之 XML 的可能外觀：  
  
```scr  
<ExternalAction>  
  <Type>TEST</Type>  
  <SendData>1</SendData>  
  <Server_URL>This is my test!</Server_URL>  
  <Action_ID>Test Workflow</Action_ID>  
  <Model_ID>5</Model_ID>  
  <Model_Name>Customer</Model_Name>  
  <Entity_ID>34</Entity_ID>  
  <Entity_Name>Customer</Entity_Name>  
  <Version_ID>8</Version_ID>  
  <MemberType_ID>1</MemberType_ID>  
  <Member_ID>12</Member_ID>  
  <MemberData>  
    <ID>12</ID>  
    <Version_ID>8</Version_ID>  
    <ValidationStatus_ID>3</ValidationStatus_ID>  
    <ChangeTrackingMask>0</ChangeTrackingMask>  
    <EnterDTM>2011-02-25T20:16:36.650</EnterDTM>  
    <EnterUserID>2</EnterUserID>  
    <EnterUserName>MyUserName</EnterUserName>  
    <EnterUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</EnterUserMuid>  
    <EnterVersionId>8</EnterVersionId>  
    <EnterVersionName>VERSION_1</EnterVersionName>  
    <EnterVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</EnterVersionMuid>  
    <LastChgDTM>2011-02-25T20:16:36.650</LastChgDTM>  
    <LastChgUserID>2</LastChgUserID>  
    <LastChgUserName>MyUserName</LastChgUserName>  
    <LastChgUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</LastChgUserMuid>  
    <LastChgVersionId>8</LastChgVersionId>  
    <LastChgVersionName>VERSION_1</LastChgVersionName>  
    <LastChgVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</LastChgVersionMuid>  
    <Name>Test Customer</Name>  
    <Code>TC</Code>  
  </MemberData>  
</ExternalAction>  
```  
  
 下表描述此 XML 中包含的某些標記：  
  
|標記|Description|  
|---------|-----------------|  
|\<類型 >|在您輸入的文字**工作流程類型**文字方塊中[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]來識別要載入的自訂工作流程組件。|  
|\<S >|布林值控制**訊息中包含成員資料**中的核取方塊[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。 值為 1 表示\<MemberData > 一節已傳送，否則\<MemberData > 不會傳送一節。|  
|< Server_URL >|在您輸入的文字**工作流程網站**文字方塊中[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。|  
|< Action_ID >|在您輸入的文字**工作流程名稱**文字方塊中[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。|  
|\<MemberData >|包含觸發工作流程動作之成員的資料。 才會包含的值\<s > 為 1。|  
|\<輸入*xxx*>|這組標記包含有關建立成員的中繼資料，例如建立成員的時間以及建立成員者。|  
|\<LastChg*xxx*>|這組標記包含有關上次對成員所進行之變更的中繼資料，例如進行變更的時間以及進行變更者。|  
|\<名稱 >|已變更之成員的第一個屬性。 此範例成員僅包含 Name 和 Code 屬性。|  
|\<程式碼 >|已變更之成員的下一個屬性。 如果此範例成員包含更多屬性，則會緊接著此屬性之後。|  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂工作流程 &#40;Master Data services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)   
 [自訂工作流程範例 &#40;Master Data services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)  
  
  
