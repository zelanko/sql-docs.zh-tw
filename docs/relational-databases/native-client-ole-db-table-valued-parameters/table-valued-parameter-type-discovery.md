---
title: 資料表值參數類型探索 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, type discovery
ms.assetid: f55818c2-ebb5-4cf6-8c0c-0da41f592560
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3fbc4e5f1ca395eb79539e8d670743bdf015b168
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698659"
---
# <a name="table-valued-parameter-type-discovery"></a>資料表值參數類型探索
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  取用者 — 也就用戶端應用程式使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，可以探索每一個命令參數的類型，如果命令文字已經提供給 OLE DB 提供者。 資料表值參數的型別已知之後，取用者可以探索每個個別資料行的資料表值參數的中繼資料資訊。  
  
 對於大部分的參數類型支援 icommandwithparameters:: Getparameterinfo 程序參數的型別資訊。 開頭為[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，利用使用者定義型別引入和**xml**資料型別，GetParameterInfo 方法不足以支撐這個用途因為它不提供使用者定義型別透過 ICommandWithParameters 的資訊 （名稱、 結構描述和目錄）。 新的介面，ISSCommandWithParameters，定義為提供擴充的類型資訊。  
  
 資料表值參數，您也使用 ISSCommandWithParameters 介面探索的詳細的資訊。 用戶端呼叫 ISSCommandWithParameters::GetParameterInfo 準備命令物件之後。 資料表值參數，如*wType* DBPARAMINFO 結構的成員提供者，會設定為 DBTYPE_TABLE。 *UlParamSize* DBPARAMINFO 結構的欄位具有值為 ~ 0。  
  
 取用者會使用 ISSCommandWithParamters 再要求其他屬性 （資料表值參數類型目錄名稱、 資料表值參數類型結構描述名稱、 資料表值參數類型名稱、 資料行排序和預設資料行）::GetParameterProperties。  
  
 已知的型別名稱後，若要擷取取用者必須呼叫個別的資料行資訊 IOpenRowset::OpenRowsetor 取得 DBSCHEMA_TABLE_TYPE_COLUMNS 資料列集指定資料表值參數類型名稱做為資料表名稱。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [您可以使用資料表值參數&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
