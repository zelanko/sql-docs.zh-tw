---
title: ISSCommandWithParameters (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4de7c6a99afcbd7db7c6e233fb737f129b536b8b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63209761"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
  **ISSCommandWithParameters**公開支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 和使用者定義型別 (UDT)。 這是選擇性的介面，繼承自核心的 OLE DB 介面**ICommandWithParameters**。 除了繼承自的三種方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，並**SetParameterInfo**;**ISSCommandWithParameters**提供用來處理伺服器特定資料類型的兩個新方法。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**使用服務元件，但本身不會使用這個介面時，可以使用介面。  
  
|方法|描述|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|針對傳遞至命令的每個 UDT 或 XML 參數以陣列傳回一個 **SSPARAMPROPS** 屬性集結構，但不會針對其他類型的參數傳回任何項目。|  
|[ISSCommandWithParameters::SetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|依照序數根據每個參數來設定參數的屬性，或指定 **SSPARAMPROPS** 結構的陣列來設定大量參數屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [使用 XML 資料類型](../native-client/features/using-xml-data-types.md)   
 [使用使用者定義型別](../native-client/features/using-user-defined-types.md)  
  
  
