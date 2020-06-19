---
title: 一般檔案自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f2caeab-784c-4b0c-9b3e-6a88d1ccdbf9
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f83cf140b370783d21ee2254e7361a2ae3467424
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915538"
---
# <a name="flat-file-custom-properties"></a>一般檔案自訂屬性
  **來源自訂屬性**  
  
 一般檔案來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是一般檔案來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|FileNameColumnName|String|包含檔案名稱之輸出資料行的名稱。 如果沒有指定任何名稱，就不會產生包含檔案名稱的輸出資料行。<br /><br /> 注意：雖然您無法在 [一般檔案來源編輯器]  中使用這個屬性，但是可以使用 [進階編輯器]  來設定這個屬性。|  
|RetainNulls|Boolean|一個值，指定當「資料轉換管線」引擎處理資料時，是否要將來源檔案的 Null 值保留成 Null 值。 此屬性的預設值為 `False`。|  
  
 一般檔案來源的輸出沒有任何自訂屬性。  
  
 下表描述的是一般檔案來源之輸出資料行的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|FastParse|Boolean|一個值，指出資料行會使用 DTS 所提供之速度更快但不區分地區設定的快速剖析常式，還是區分地區設定的標準剖析常式。 如需詳細資訊，請參閱 [快速剖析](../fast-parse.md) 和 [標準剖析](../standard-parse.md)。 此屬性的預設值為 `False`。<br /><br /> 注意：雖然您無法在 [一般檔案來源編輯器]  中使用這個屬性，但是可以使用 [進階編輯器]  來設定這個屬性。|  
  
 如需詳細資訊，請參閱 [一般檔案來源](flat-file-source.md)。  
  
 **目的地自訂屬性**  
  
 一般檔案目的地同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是一般檔案目的地的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|描述|  
|-------------------|---------------|-----------------|  
|頁首|String|寫入任何資料之前插入檔案中的文字區塊。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
|Overwrite|Boolean|一個值，指定要覆寫或附加至具有相同名稱的現有目的地檔案。 此屬性的預設值為 `True`。|  
  
 一般檔案目的地的輸入和輸入資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [一般檔案目的地](flat-file-destination.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](../common-properties.md)  
  
  
