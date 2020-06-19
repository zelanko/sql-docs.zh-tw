---
title: 原始檔案自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 83065ca2b878b51045d548d04e97b70d40716926
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84914768"
---
# <a name="raw-file-custom-properties"></a>原始檔案自訂屬性
  **來源自訂屬性**  
  
 原始檔案來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是原始檔案來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|AccessMode|整數 (列舉)|用來存取原始資料的模式。 可能的值為 `File name` (0) 和 `File name from variable` (1)。 預設值為 `File name` (0)。|  
|FileName|String|來源檔案的路徑和檔案名稱。|  
  
 原始檔案來源的輸出和輸出資料行沒有任何自訂屬性。  
  
 如需相關資訊，請參閱 [Raw File Source](raw-file-source.md)。  
  
 **目的地自訂屬性**  
  
 原始檔案目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是原始檔案目的地的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|AccessMode|整數 (列舉)|一個值，指定 FileName 屬性包含檔案名稱，或包含檔案名稱之變數的名稱。 這些選項包括 `File name` (0) 和 `File name from variable` (1)。|  
|FileName|String|原始檔案目的地寫入的檔案名稱。|  
|WriteOption|整數 (列舉)|一個值，指定原始檔案目的地是否會刪除具有相同名稱的現有檔案。 這些選項包括 `Create Always` (0)、`Create Once` (1)、`Truncate and Append` (3) 和 `Append` (2)。 此屬性的預設值為 `Create Always` (0)。|  
  
> [!NOTE]  
>  附加作業要求已附加資料的中繼資料與檔案中已有資料的中繼資料相符。  
  
 原始檔案目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需相關資訊，請參閱 [Raw File Destination](raw-file-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](../common-properties.md)  
  
  
