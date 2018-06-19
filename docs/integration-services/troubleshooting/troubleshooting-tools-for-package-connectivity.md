---
title: 封裝連線的疑難排解工具 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- connectivity [Integration Services], troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: 08a019f5-8ba7-4527-97c1-e9846d4022ff
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 003568e981236cc42d3c041ff52cacc20f376124
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35335372"
---
# <a name="troubleshooting-tools-for-package-connectivity"></a>疑難排解封裝連接的工具
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所含的功能及工具，可以讓您用於疑難排解封裝與封裝擷取及載入資料之資料來源之間的連接。  
  
## <a name="troubleshooting-issues-with-external-data-providers"></a>疑難排解外部資料提供者的問題  
 與外部資料提供者互動期間發生許多封裝失敗。 但是，這些提供者傳回 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的訊息經常未提供足夠的資訊，導致無法開始進行互動的疑難排解。 為了解決這個疑難排解需要， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包括新的記錄訊息，可供您用於針對封裝與外部資料來源之間的互動進行疑難排解。  
  
-   **啟用記錄並選取封裝的 [診斷] 事件以查看新的疑難排解訊息**。 下列 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 元件將能夠在每次呼叫外部資料提供者之前和之後，於記錄中寫入訊息：  
  
    -   OLE DB 連接管理員、OLE DB 來源和 OLE DB 目的地  
  
    -   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員和 ADO NET 來源  
  
    -   執行 SQL 工作  
  
    -   查閱轉換、OLE DB 命令轉換和緩時變維度轉換  
  
     記錄訊息包括所呼叫方法的名稱。 例如，這些記錄訊息可能包括 OLE DB **Open** 物件的 **Connection** 方法，或 **ExecuteNonQuery** 物件的 **Command** 方法。 訊息的格式如下，其中 '%1!s!' 是方法資訊的預留位置：  
  
    ```  
    ExternalRequest_pre: The object is ready to make the following external request: '%1!s!'.  
    ExternalRequest_post: '%1!s!'. The external request has completed.  
    ```  
  
     若要疑難排解與外部資料提供者之間的互動，請檢閱記錄，查看是不是每個「呼叫前」訊息 (`ExternalRequest_pre`) 都有一個對應的「呼叫後」訊息 (`ExternalRequest_post`)。 如果沒有對應的「呼叫後」訊息，您就知道外部資料提供者並未如預期方式回應。  
  
     下列範例顯示記錄中的一些範例資料列，其中包含這些記錄訊息：  
  
    ```  
    ExternalRequest_pre: The object is ready to make the following external request: 'ITransactionJoin::JoinTransaction'.  
    ExternalRequest_post: 'ITransactionJoin::JoinTransaction succeeded'. The external request has completed.  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.Open'.  
    ExternalRequest_post: 'IDbConnection.Open succeeded'. The external request has completed.  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.CreateCommand'.  
    ExternalRequest_post: 'IDbConnection.CreateCommand finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbCommand.ExecuteReader'.  
    ExternalRequest_post: 'IDbCommand.ExecuteReader finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDataReader.GetSchemaTable'.  
    ExternalRequest_post: 'IDataReader.GetSchemaTable finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDataReader.Close'.  
    ExternalRequest_post: 'IDataReader.Close finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.Close'.  
    ExternalRequest_post: 'IDbConnection.Close finished'. The external request has completed."  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [疑難排解封裝開發的工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)   
 [套件執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
