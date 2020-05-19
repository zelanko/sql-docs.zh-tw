---
title: ICommandWithParameters | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 281abeeb0a29ba697fe8c8b42027280377315e86
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704865"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
  從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，資料庫引擎的改進功能就允許 ICommandWithParameters::GetParameterInfo 針對預期的結果取得更精確的描述。 這些更精確的結果可能與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中 CommandWithParameters::GetParameterInfo 所傳回的值不同。 如需詳細資訊，請參閱[中繼資料探索](../native-client/features/metadata-discovery.md)。  
  
 此外，從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，當您呼叫 ICommandWithParameters::SetParameterInfo 時，傳遞給 *pwszName* 參數的值必須是有效的識別碼。 如需詳細資訊，請參閱＜ [Database Identifiers](../databases/database-identifiers.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
