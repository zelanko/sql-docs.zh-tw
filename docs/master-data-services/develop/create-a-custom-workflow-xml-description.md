---
title: "自訂工作流程 XML 描述 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: develop
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: e267e5f4-38bb-466d-82e8-871eabeec07e
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d615319210bcedd0c22cd59c3dbe8c1a3f06daa
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="create-a-custom-workflow---xml-description"></a>建立自訂工作流程 - XML 描述
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 中，當工作流程啟動時，SQL Server MDS 工作流程整合服務會呼叫 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> 方法。 此方法會收到有關觸發工作流程商務規則之項目的中繼資料和資料，做為 XML 的區塊。 如需實作工作流程處理常式的範例程式碼，請參閱[自訂工作流程範例 &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)。  
  
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
|\<Type>|您在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 之 [工作流程類型] 文字方塊中輸入的文字，用以識別要載入的自訂工作流程組件。|  
|\<SendData>|在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 中，由 [訊息中包含成員資料] 核取方塊所控制的布林值。 值為 1 時，表示傳送 \<MemberData> 區段，否則，不傳送 \<MemberData> 區段。|  
|<Server_URL>|您在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 之 [工作流程網站] 文字方塊中輸入的文字。|  
|<Action_ID>|您在 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 之 [工作流程名稱] 文字方塊中輸入的文字。|  
|\<MemberData>|包含觸發工作流程動作之成員的資料。 只有在 \<SendData> 的值為 1 時，才包含這個標記。|  
|\<Enter*xxx*>|這組標記包含有關建立成員的中繼資料，例如建立成員的時間以及建立成員者。|  
|\<LastChg*xxx*>|這組標記包含有關上次對成員所進行之變更的中繼資料，例如進行變更的時間以及進行變更者。|  
|\<Name>|已變更之成員的第一個屬性。 此範例成員僅包含 Name 和 Code 屬性。|  
|\<Code>|已變更之成員的下一個屬性。 如果此範例成員包含更多屬性，則會緊接著此屬性之後。|  
  
## <a name="see-also"></a>另請參閱  
 [建立自訂工作流程 &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)   
 [自訂工作流程範例 &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)  
  
  
