---
title: "原始檔案自訂屬性 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b007bc2aa2f8e8a2b7f9b7d3dfbfbbeece4730cf
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="raw-file-custom-properties"></a>原始檔案自訂屬性
  **來源自訂屬性**  
  
 原始檔案來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是原始檔案來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|AccessMode|整數 (列舉)|用來存取原始資料的模式。 可能的值為 [檔案名稱] (0) 和 [來自變數的檔案名稱] (1)。 預設值是 [檔案名稱] (0)。|  
|FileName|String|來源檔案的路徑和檔案名稱。|  
  
 原始檔案來源的輸出和輸出資料行沒有任何自訂屬性。  
  
 如需相關資訊，請參閱 [Raw File Source](../../integration-services/data-flow/raw-file-source.md)。  
  
 **目的地自訂屬性**  
  
 原始檔案目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是原始檔案目的地的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|AccessMode|整數 (列舉)|一個值，指定 FileName 屬性包含檔案名稱，或包含檔案名稱之變數的名稱。 選項為 [檔案名稱] (0) 和 [來自變數的檔案名稱] (1)。|  
|FileName|String|原始檔案目的地寫入的檔案名稱。|  
|WriteOption|整數 (列舉)|一個值，指定原始檔案目的地是否會刪除具有相同名稱的現有檔案。 選項為 [永遠建立] (0)、[建立一次] (1)、[截斷與附加] (3) 和 [附加] (2)。 此屬性的預設值為 [永遠建立] (0)。|  
  
> [!NOTE]  
>  附加作業要求已附加資料的中繼資料與檔案中已有資料的中繼資料相符。  
  
 原始檔案目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需相關資訊，請參閱 [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
