---
title: ISSCommandWithParameters (OLE DB) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSCommandWithParameters (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 90359b753baff55d70c00727b8230c41059ceaa3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037667"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
  **ISSCommandWithParameters**公開支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 和使用者定義型別 (UDT)。 這是選擇性的介面，繼承自核心的 OLE DB 介面**ICommandWithParameters**。 除了繼承自的三種方法**ICommandWithParameters**;**GetParameterInfo**， **MapParameterNames**，和**SetParameterInfo**;**ISSCommandWithParameters**提供兩種新方法，可用來處理伺服器特定資料類型。  
  
> [!NOTE]  
>  **ISSCommandWithParameters**時使用服務元件，但本身不會使用這個介面，可以使用介面。  
  
|方法|描述|  
|------------|-----------------|  
|[Getparameterinfo &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|傳回一個**SSPARAMPROPS**屬性設定為傳遞至命令，每個 UDT 或 XML 參數陣列中的結構，但對於其他類型的參數傳回 none。|  
|[Isscommandwithparameters:: &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|依序數，根據每個參數來設定參數屬性，或藉由指定的陣列中設定大量參數屬性**SSPARAMPROPS**結構。|  
  
## <a name="see-also"></a>另請參閱  
 [介面&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [使用 XML 資料類型](../native-client/features/using-xml-data-types.md)   
 [使用使用者定義型別](../native-client/features/using-user-defined-types.md)  
  
  