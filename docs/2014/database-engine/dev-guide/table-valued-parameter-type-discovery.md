---
title: 資料表值參數類型探索 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ab8d837e4ddf74256e4bae70f772557ec8ff67f7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933249"
---
# <a name="table-valued-parameter-type-discovery"></a>資料表值參數類型探索
  取用者（也就是使用 Native Client OLE DB 提供者的用戶端應用程式）， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果命令文字已提供給 OLE DB 提供者，就可以探索每個命令參數的型別。 知道了資料表值參數的類型之後，取用者就可以針對資料表值參數的每一個個別資料行來探索中繼資料資訊。  
  
 ICommandWithParameters::GetParameterInfo 可針對大多數的參數類型來支援程序參數的類型資訊。 從開始 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ，隨著使用者定義型別和資料型別的引進 `xml` ，GetParameterInfo 方法並不足以達成此目的，因為無法透過 ICommandWithParameters 提供使用者定義型別資訊（名稱、架構和目錄）。 因此定義了新的介面 ISSCommandWithParameters 來提供擴充類型資訊。  
  
 如果是資料表值參數，您也可以使用 ISSCommandWithParameters 介面來探索詳細資訊。 在準備命令物件之後，用戶端會呼叫 ISSCommandWithParameters::GetParameterInfo。 如果是資料表值參數，DBPARAMINFO 結構的 *wType* 成員會由提供者設定為 DBTYPE_TABLE。 DBPARAMINFO 結構的 *ulParamSize* 欄位具有 ~0 的值。  
  
 然後取用者會使用 ISSCommandWithParameters::GetParameterProperties 來要求其他屬性 (資料表值參數類型目錄名稱、資料表值參數類型結構描述名稱、資料表值參數類型名稱、資料行排序和預設資料行)。  
  
 如果在知道了類型名稱之後要擷取個別資料行資訊，取用者必須呼叫 IOpenRowset::OpenRowsetor 或取得 DBSCHEMA_TABLE_TYPE_COLUMNS 資料列集，其方式是將資料表值參數類型名稱指定為資料表名稱。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
