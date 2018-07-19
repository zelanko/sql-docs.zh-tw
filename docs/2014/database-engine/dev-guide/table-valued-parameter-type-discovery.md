---
title: 資料表值參數類型探索 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
caps.latest.revision: 20
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 021109d32ceed7055348aea0bb0cb9ac32a4c7c8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231948"
---
# <a name="table-valued-parameter-type-discovery"></a>資料表值參數類型探索
  取用者 — 亦即，用戶端應用程式使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，可以探索每一個命令參數的類型，如果命令文字已經提供給 OLE DB 提供者。 在已知的資料表值參數的類型之後，取用者可以探索每個個別的資料行的資料表值參數的中繼資料資訊。  
  
 對於大部分的參數類型支援 icommandwithparameters:: Getparameterinfo 程序參數的型別資訊。 開頭[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，採用使用者定義型別和`xml`資料型別，GetParameterInfo 方法無法滿足此用途因為它不提供使用者定義型別資訊 (名稱、 結構描述，以及透過 ICommandWithParameters 目錄）。 新的介面，ISSCommandWithParameters，被定義為提供擴充的類型資訊。  
  
 資料表值參數，您也使用 ISSCommandWithParameters 介面來探索的詳細的資訊。 用戶端會呼叫 ISSCommandWithParameters::GetParameterInfo 準備命令物件之後。 資料表值參數，如*wType* DBPARAMINFO 結構的成員提供者，會設定為 DBTYPE_TABLE。 *UlParamSize* DBPARAMINFO 結構的欄位具有值為 ~ 0。  
  
 取用者會接著使用 ISSCommandWithParamters 要求其他屬性 （資料表值參數類型類別目錄名稱、 資料表值參數類型結構描述名稱、 資料表值參數的型別名稱、 資料行排序和預設資料行）：GetParameterProperties。  
  
 已知的型別名稱之後，若要擷取個別的資料行資訊的取用者必須呼叫 IOpenRowset::OpenRowsetor 取得 DBSCHEMA_TABLE_TYPE_COLUMNS 資料列集藉由指定資料表值參數類型名稱作為資料表名稱。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用資料表值參數&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
