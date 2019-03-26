---
title: XML 來源自訂屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a1bd4c6866f7090a00567240350f1355f5c7f5e6
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270341"
---
# <a name="xml-source-custom-properties"></a>XML 來源自訂屬性
  XML 來源同時具有自訂屬性以及所有資料流程元件通用的屬性。  
  
 下表描述的是 XML 來源的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|用來存取 XML 資料的模式。|  
|UseInlineSchema|布林|一個值，指出是否要使用 XML 來源中的內嵌結構描述定義。 此屬性的預設值為 **False**。|  
|XMLData|String|要從中擷取 XML 資料的檔案或變數。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
|XMLSchemaDefinition|String|結構描述定義檔 (.xsd) 的路徑和檔案名稱。<br /><br /> 此屬性的值可以使用屬性運算式指定。|  
  
 下表描述的是 XML 來源之輸出的自訂屬性。 所有屬性都是可讀寫的。  
  
|屬性名稱|資料類型|Description|  
|-------------------|---------------|-----------------|  
|RowsetID|String|一個值，可識別與輸出相關聯的資料列集。|  
  
 XML 來源的輸出資料行沒有任何自訂屬性。  
  
 如需詳細資訊，請參閱 [XML 來源](../../integration-services/data-flow/xml-source.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
