---
title: 執行包含資料表值參數的命令 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, executing commands containing
ms.assetid: 7ecba6f6-fe7a-462a-9aa3-d5115b6d4529
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae08a79bcfe1e4befcad8559e82bdfba5b347fc2
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52417849"
---
# <a name="executing-commands-containing-table-valued-parameters"></a>執行包含資料表值參數的命令
  執行包含資料表值參數的命令需要兩個階段：  
  
1.  指定參數類型。  
  
2.  繫結參數資料。  
  
## <a name="table-valued-parameter-specification"></a>資料表值參數規格  
 取用者可以指定資料表值參數的類型。 此資訊包含資料表值參數類型名稱。 如果資料表值參數的使用者定義資料表類型不在用於連接的目前預設結構描述中，它也包含結構描述名稱。 根據伺服器支援，取用者也可以指定選擇性的中繼資料資訊，例如，資料行的順序，而且可以指定特定資料行的所有資料列都有預設值。  
  
 若要指定的資料表值參數，取用者會呼叫 ISSCommandWithParameter::SetParameterInfo，，並選擇性地呼叫 isscommandwithparameters:: Setparameterproperties。 如果是資料表值參數，DBPARAMBINDINFO 結構中的 *pwszDataSourceType* 欄位將會有 DBTYPE_TABLE 的值。 *ulParamSize* 欄位會設定為 ~0，表示長度未知。 對於資料表值參數，例如結構描述名稱、 型別名稱、 資料行順序和預設資料行的特定屬性可以透過 isscommandwithparameters:: Setparameterproperties 進行設定。  
  
## <a name="table-valued-parameter-binding"></a>資料表值參數繫結  
 資料表值參數可以是任何資料列集物件。 提供者會在執行期間將資料表值參數傳送到伺服器的同時，從此物件讀取。  
  
 若要繫結資料表值參數，取用者會呼叫 iaccessor:: Createaccessor。 如果是資料表值參數，DBBINDING 結構的 *wType* 欄位會設定為 DBTYPE_TABLE。 DBBINDING 結構的 *pObject* 成員不是 NULL，而且 *pObject* 的 *iid* 成員會設定為 IID_IRowset 或其他任何資料表值參數資料列集物件介面。 DBBINDING 結構中其餘欄位的設定方式應該與針對資料流 BLOB 設定欄位的方式相同。  
  
 如果是資料表值參數以及與資料表值參數相關聯之資料列集物件的繫結，則適用下列限制：  
  
-   資料表值參數資料列集資料行資料所允許的唯一狀態值為 DBSTATUS_S_ISNULL 和 DBSTATUS_S_OK。 DBSTATUS_S_DEFAULT 將會導致失敗，而繫結的狀態值將會設定為 DBSTATUS_E_BADSTATUS。  
  
-   資料表值參數可以使用 DBSTATUS_S_DEFAULT 狀態標示。 唯一的有效值為 DBSTATUS_S_DEFAULT 和 DBSTATUS_S_OK。 當狀態設定為 DBSTATUS_S_DEFAULT 時，資料表值參數的值會對應到一個空資料表。  
  
-   資料表值參數中的唯讀資料行 (識別或計算資料行) 必須使用 SSPROP_PARAM_TABLE_DEFAULT_COLUMNS 屬性標示為預設值。 有預設值的資料行也必須標示為預設會透過 SSPROP_PARAM_TABLE_DEFAULT_COLUMNS 屬性，以允許要用於特定的資料表值參數資料行的資料值的預設值。 提供者將會忽略針對標示為預設值之資料行所繫結的資料值。  
  
-   除非同時設定 SSPROP_PARAM_TABLE_DEFAULT，否則會將包含 DBPROP_COL_AUTOINCREMENT 或 SSPROP_COL_COMPUTED 之資料行的資料傳送到伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數 &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
