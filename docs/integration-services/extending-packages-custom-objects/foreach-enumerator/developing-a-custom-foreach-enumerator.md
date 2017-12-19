---
title: "開發自訂 ForEach 列舉值 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- custom foreach enumerators [Integration Services]
- custom foreach enumerators [Integration Services], about custom foreach enumerators
- foreach enumerators [Integration Services]
ms.assetid: bffe26e0-1b9a-47ad-bae6-6b708cb4cf4f
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 72173ef704d12154cffe3eabcbe09317f1c40c10
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="developing-a-custom-foreach-enumerator"></a>開發自訂 ForEach 列舉值
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 會使用 Foreach 列舉值在集合中反覆運算項目，並為每個元素執行相同的工作。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包括各種 Foreach 列舉值，可以支援最常使用的集合，例如在資料夾中的所有檔案、資料庫中的所有資料表，或是儲存在封裝變數中的清單之所有元素。 如果提供的 Foreach 列舉值與集合並未完全符合您的需求，可以建立自訂 Foreach 列舉值。  
  
 若要建立自訂 Foreach 列舉值，您必須建立繼承自 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator> 基底類別的類別、將 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> 屬性 (Attribute) 套用至新類別，以及覆寫基底類別的重要方法與屬性 (Property)，包括 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 方法。  
  
## <a name="in-this-section"></a>本節內容  
 本章節描述如何建立和設定自訂 Foreach 列舉值及其自訂使用者介面，以及如何撰寫它們的程式碼。  
  
 [建立自訂 Foreach 列舉程式](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)  
 描述如何為自訂 Foreach 列舉值專案建立類別。  
  
 [撰寫自訂 Foreach 列舉程式的程式碼](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)  
 描述如何透過覆寫基底類別的方法與屬性，來實作自訂 Foreach 列舉值。  
  
 [開發自訂 Foreach 列舉程式的使用者介面](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
 描述如何實作用以設定自訂 Foreach 列舉值的使用者介面類別與表單。  
  
## <a name="related-topics"></a>相關主題  
  
### <a name="information-common-to-all-custom-objects"></a>自訂物件的共通資訊  
 如需有關 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中可以建立之所有類型自訂物件適用的共通資訊，請參閱下列主題：  
  
 [開發 Integration Services 的自訂物件](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 描述為 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 實作所有類型的自訂物件之基本步驟。  
  
 [保存自訂物件](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 描述自訂的持續性並解釋必須實作它的時機。  
  
 [自訂物件的建立、部署和偵錯](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 描述建立、簽署、部署和偵錯自訂物件的技術。  
  
### <a name="information-about-other-custom-objects"></a>其他自訂物件的相關資訊  
 如需有關在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中可以建立之其他類型自訂物件的詳細資訊，請參閱下列主題：  
  
 [開發自訂工作](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 討論如何進行自訂工作的程式設計。  
  
 [開發自訂連線管理員](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 討論如何進行自訂連接管理員的程式設計。  
  
 [開發自訂記錄提供者](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 討論如何進行自訂記錄提供者的程式設計。  
  
 [開發自訂資料流程元件](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 討論如何進行自訂資料流程來源、轉換和目的地的程式設計。  
 
